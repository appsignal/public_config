# Ruby VM magic dashboards

The Ruby Virtual Machine refers to the internals of the Ruby interpreter (sometimes referred to as MRI) which is the program that is used to execute applications written in the Ruby programming language.

> ⚠️ These magic dashboards will only appear when using the "mainline" or "official" Ruby interpreter, sometimes referred to as MRI (Matz's Ruby Interpreter) -- when using other Ruby interpreters, such as JRuby, this magic dashboard will not appear.

During the lifetime of the Ruby application, the Ruby VM will take care of managing the memory that the application needs, occassionally freeing memory that is no longer used, a process which is referred to as "Garbage Collection" (GC). During a garbage collection event, the application will essentially be put on pause. This can lead to increased latency and response times, for example, if the garbage collection event takes place while handling an user's request.

There are two magic dashboards for the Ruby virtual machine:

- [Virtual Machine](#virtual-machine-magic-dashboard)
- [Global VM Lock](#global-vm-lock-magic-dashboard)

## Virtual Machine magic dashboard

The "Ruby (VM) metrics" magic dashboard contains graphs for the metrics that are emitted by the AppSignal for Ruby integration's [MRI minutely probe](https://github.com/appsignal/appsignal-ruby/blob/main/lib/appsignal/probes/mri.rb). This probe is enabled by default since Ruby version 2.9.0, and can be disabled by [overriding the `:mri` probe](https://docs.appsignal.com/ruby/instrumentation/minutely-probes.html#overriding-default-probes). The minutely probe asks the Ruby VM about its state once per minute, and reports that data to AppSignal. All the measurements, therefore, are taken once per minute.

These stats correspond to information obtained from the [`GC.stat`](https://ruby-doc.org/core-2.7.0/GC.html#method-c-stat) and [`RubyVM.stat`](https://www.rubydoc.info/stdlib/core/RubyVM.stat) objects exposed by the Ruby virtual machine. Many explanations for the contents of this dashboard are derived from [this informative blog post on `GC.stat` by Nate Berkopec](https://www.speedshop.co/2017/03/09/a-guide-to-gc-stat.html).

The following graphs are displayed in this magic dashboard:

- [Allocated objects](#allocated-objects)
- [GC counts](#gc-counts)
- [Heap slots](#heap-slots)
- [Ruby VM](#ruby-vm)
- [Thread count](#thread-count)
- [GC time](#gc-time)

### Allocated objects

The "Allocated Objects" graph shows the amount of objects currently allocated in memory in the Ruby virtual machine. Here, "objects" refers to any complex Ruby value, anything other than primitive types such as strings, numbers, booleans and symbols. When a new Ruby object needs to be created, the virtual machine must allocate (think "assign" or "claim") memory for it. That memory will be taken up by that object until it is freed by a garbage collection event.

This graph displays values from the `allocated_objects` metric. This graph will show a line for each combination of values of the following metric tags:

- The **hostname** of the machine that emitted the metric. 

### GC counts

The "GC counts" graph shows the amount of garbage collection events (or "runs") that took place **during the last minute**, [split between minor and major events](https://github.com/appsignal/appsignal-ruby/blob/965fe4b731c3f9a992752448e54869957215f21a/lib/appsignal/probes/mri.rb#L69-L77). 

During a garbage collection event, the Ruby application is essentially put on pause. Knowing when a garbage collection event took place can be useful in understanding an increase in the application's latency, which might be reflected in increased response times.

Minor garbage collection events happen more frequently, but only consider whether to free recently created objects. Major garbage collection events happen less frequently, but they consider the entire object graph as candidates for deletion, which means that they take longer.

You can read more about this topic in [this informative blog post on Ruby's generational garbage collection by Jemma Issroff](https://jemma.dev/blog/gc-generational).

This graph displays values from the `gc_count` metric. This graph will show a line for each combination of values of the following metric tags:

- The **hostname** of the machine that emitted the metric.
- The **metric**, the kind of GC event that took place, which is either:
  - `"minor_gc_count"`
  - `"major_gc_count"`
  - `"gc_count"`, which counts both minor and major GC events indistinctly

### Heap slots

The "Heap slots" graph shows the amount of heap slots currently allocated by the Ruby virtual machine, [split between live slots and free slots](https://github.com/appsignal/appsignal-ruby/blob/965fe4b731c3f9a992752448e54869957215f21a/lib/appsignal/probes/mri.rb#L79-L82).

In the Ruby virtual machine, the "heap" refers to the data structure (and the memory space it occupies) where information about Ruby objects is stored. The heap is divided in pages, which each contain a number of slots, and each slot can contain information about a single Ruby object. A slot is said to be a live slot if it currently contains information about a Ruby object, and it is said to be a free slot if it doesn't.

When the Ruby virtual machine runs out of slots, it must allocate more pages to store information about newly created objects, which it does by requesting memory from the operating system. Large numbers of free slots can indicate issues where lots of objects are quickly allocated and then freed, causing more memory pages to be requested, and bloating the overall memory footprint of the Ruby process.

This graph displays values from the `heap_slots` metric. This graph will show a line for each combination of values of the following metric tags:

- The **hostname** of the machine that emitted the metric.
- The **metric**, the kind of heap slot that is being counted, which is either:
  - `"heap_live"`
  - `"heap_free"`

### Ruby VM

The "Ruby VM" graph shows some statistics obtained from the `RubyVM.stat` method about [the constant cache and the classes that are created](https://github.com/appsignal/appsignal-ruby/blob/965fe4b731c3f9a992752448e54869957215f21a/lib/appsignal/probes/mri.rb#L23-L52) in your application.

#### Constant cache

> ⚠️ When running versions earlier than 3.2.0 of the Ruby interpreter, the lines corresponding to the `"constant_cache_misses"` and `"constant_cache_invalidations"` metric tags will not be shown, as these metrics are not available in older Ruby versions.

The Ruby virtual machine caches values in globally defined constants for easier access. This allows, amongst other things, for methods in constants to be accessed quicker:

```ruby
class Foo # `Foo` is a constant.
  def self.bar
    "hi!"
  end
end

# This will not require a property lookup on `Foo` each time,
# because the Ruby VM caches the values of constants.
100.times do { puts Foo.bar }
```

However, in Ruby, classes can be opened, and their properties and methods can be redefined:

```ruby
class Foo # Here we are reopening the `Foo` class that we defined earlier...
  def self.bar # ... and redefining the `.bar` method, invalidating the cache.
    "bye!"
  end
end

# The next time `Foo.bar` is called, there will be a cache miss.
puts Foo.bar
```

The metrics on RubyVM.stat keep track of the status of the cache of constant values. The `"global_constant_state"` metric keeps track of how many invalidations of the constant cache have been performed. Increases to this number at run-time would indicate that your application's code is redefining constants "on the fly". This could affect the performance of your application, as invalidating this cache causes it to need to be rebuilt on the next lookup, which can be slow.

In Ruby version 3.2.0 and above, it may be more useful to look at the `"constant_cache_invalidations"` and `"constant_cache_misses"` keys, which show the amount of times that a constant cache entry was invalidated, and the amount of times that an entry could not be accessed from the cache. These keys are not available in earlier Ruby versions.

#### Classes

The `"class_serial"` metric for this graph will show a monotonically increasing counter of the classes that are created in your application. Each time a new class is defined in your application, this value will increase by one.

#### Metric tags

This graph displays values from the `ruby_vm` metric. This graph will show a line for each combination of values of the following metric tags:

- The **hostname** of the machine that emitted the metric.
- The **metric**, the value from the Ruby VM that is being measured, which is either:
  - `"global_constant_state"`
  - `"constant_cache_invalidations"`
  - `"constant_cache_misses"`
  - `"class_serial"`

### Thread count

The "Thread count" graph shows [the amount of threads that are currently executing](https://github.com/appsignal/appsignal-ruby/blob/965fe4b731c3f9a992752448e54869957215f21a/lib/appsignal/probes/mri.rb#L54) in your application. During the course of your Ruby application, it can spawn different execution threads, which will execute different code paths concurrently. Because the Ruby VM can only run one thread at a time, having too many threads active at the same time can slow down your application due to the necessary switching between them.

This graph displays values from the `thread_count` metric. This graph will show a line for each combination of values of the following metric tags:

- The **hostname** of the machine that emitted the metric.

### GC time

The "GC time" graph shows [the amount of time spent in garbage collection runs](https://github.com/appsignal/appsignal-ruby/blob/965fe4b731c3f9a992752448e54869957215f21a/lib/appsignal/probes/mri.rb#L55-L59).

> ⚠️ This graph will be empty unless the `gc_time` metric is reported. For this metric to be reported, users must [manually enable garbage collection profiling](https://docs.appsignal.com/ruby/integrations/garbage-collection.html). This is not enabled by default, as it has a performance impact in the application.

During a garbage collection event, your application is paused, meaning it is not responding to requests, processing data, or otherwise doing useful work. Measuring the amount of time spent doing garbage collection runs can be useful to understand the impact it has in your application's latency and response times.

This graph displays values from the `gc_time` metric. This graph will show a line for each combination of values of the following metric tags:

- The **hostname** of the machine that emitted the metric.

## Global VM Lock magic dashboard

The "Ruby GVL" magic dashboard contains graphs for the metrics that are emitted by the AppSignal for Ruby integration's [GVL minutely probe](https://github.com/appsignal/appsignal-ruby/blob/main/lib/appsignal/probes/gvl.rb).

> ⚠️ This probe is only enabled if the user is using AppSignal for Ruby version 3.3.9 or higher, Ruby version 3.2 or higher, and the `gvltools` gem version 0.2 or higher is installed.

The Global VM Lock (GVL) is the mechanism within the Ruby VM that schedules the execution of threads. In Ruby, threads are executed concurrently, but not in parallel. This means that only one thread can be executing at a given time, and the threads have "take turns" to make progress in their work. This thread switching is coordinated through the global VM lock.

When the above conditions are met, the measurement of global VM lock waiting threads and global VM lock timings is enabled by default. Measuring these values, however, incurs a performance cost in itself. To avoid this performance cost throughout the application, it is possible for the user to set the `enable_gvl_waiting_threads` and `enable_gvl_global_timer` AppSignal configuration options to `false`, and then manually control when these metrics are activated through the use of GVLTools itself, [as described in our documentation](https://docs.appsignal.com/ruby/integrations/global-vm-lock.html).

The following graphs are displayed in this magic dashboard:

- [Global timer](#global-timer)
- [Waiting threads](#waiting-threads)

### Global timer

The "Global timer" graph shows the amount of time that threads spent waiting to be resumed **during the last minute**, that is, waiting for their code to be executed again. Note that each thread reports its waiting time individually -- that is, if three different threads spent the whole of the last minute waiting to be reported, the time reported in this graph will be three minutes.

As your application spawns more and more threads, each of those threads will spend more time waiting for the scheduler to allow it to do work, and less time actually doing useful work, which could result in an overall slowdown.

This graph displays values from the `gvl_global_timer` metric. This graph will show a line for each combination of values of the following metric tags:

- The **hostname** of the machine that emitted the metric.

### Waiting threads

The "Waiting threads" graph shows the number of threads that are waiting to be resumed at any given point in time. This does not include threads that are not ready to be resumed, such as threads that are sleeping or awaiting on an I/O event.

As your application spawns more and more threads, more threads will be waiting at any given point in time, and less threads will be actually doing useful work, which could result in an overall slowdown.

This graph displays values from the `gvl_waiting_threads` metric. This graph will show a line for each combination of values of the following metric tags:

- The **hostname** of the machine that emitted the metric.
