# AppSignal Automated Dashboards

The `public_config` repository is a place for AppSignal's public configuration. This is currently used for the Automated Dashboards.

## Automated Dashboards

Automated Dashboards can be found in the `dashboards/` sub directory. Each directory is a different integration, like a language or package. Each dashboard is its own file in these sub-directories in the JSON format:

- [Action Mailer](/dashboards/action_mailer/)
- [Active Job](/dashboards/active_job/)
- [AWS](/dashboards/aws/) (via AWS CloudWatch)
- [AWS CloudWatch Metric Streams](/dashboards/cloudwatch/)
- [AWS Firehose](/dashboards/firehose/)
- [Ecto](/dashboards/ecto/)
- [Erlang](/dashboards/erlang/)
- [Heroku](/dashboards/heroku/)
- [Karafka](/dashboards/karafka/)
- [Kubernetes](/dashboards/kubernetes/)
- [MongoDB](/dashboards/mongodb/) (via AppSignal for Ruby)
- [MongoDB](/dashboards/mongodb_vector/) (via Vector)
- [Next.js](/dashboards/nextjs/) (deprecated)
- [NGINX](/dashboards/nginx/)
- [Node.js](/dashboards/nodejs/)
- [Oban](/dashboards/oban/)
- [PostgreSQL](/dashboards/postgres/) (via Vector)
- [Process Memory](/dashboards/process_memory/)
- [Puma](/dashboards/puma/)
- [Render](/dashboards/render/)
- [Ruby VM](/dashboards/ruby_vm/)
- [Sidekiq](/dashboards/sidekiq/)
- [Web Vitals](/dashboards/web-vitals/)

### Validation

To validate all dashboards in this repository, run the following command. To pass the validation, fix any issues that are printed.

```
rake validate
```
