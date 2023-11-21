# ActionMailer automated dashboard

[ActionMailer](https://guides.rubyonrails.org/action_mailer_basics.html) is the e-mail delivery system built for Ruby on Rails.

When using [the AppSignal for Ruby gem](https://docs.appsignal.com/ruby/integrations/mongodb.html) in an application that uses ActionMailer, the ActionMailer automated dashboard will appear.

The following graphs are displayed in this automated dashboard:

- [Deliveries](#deliveries)

## Deliveries

The "Deliveries" graphs show the amount of delivery actions that were invoked in your mailers. The first graph shows the total amount of deliveries, while the second one shows the relative percentage represented by each delivery type.

These graphs display values from the `action_mailer_process` metric. These graphs will show a line for each combination of values of the following metric tags:

- The **action** that was invoked on the mailer.
- The **mailer** on which the action was invoked. 
