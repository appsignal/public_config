# Erlang magic dashboard

AppSignal tracks Erlang VM metrics.
It has graphs metrics on IO, schedulers, processes and memory, to give a high-level overview of what's happening on the VM.

## IO

This graph shows the amount of input and output you have cumulatively, expressed in kilobytes.

## Schedulers

This graph shows the total number of available schedulers and the number of online schedulers.
Erlang's schedulers schedule CPU time between your processes.
The number of schedulers defaults to the number of CPU cores on the machine.

## Processes

The number of processes and the limit are plotted here.
The limit is the maximum number of simultaneously existing processes at the local node.

## Memory

This shows the total amount of memory that is used as well as its usage, split into processes, system, binary, ets and code.
