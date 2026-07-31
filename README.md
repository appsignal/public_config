# AppSignal Automated Dashboards

The `public_config` repository is a place for AppSignal's public configuration. This is currently used for the Automated Dashboards.

## Automated Dashboards

Automated Dashboards can be found in the `dashboards/` sub directory. Each directory is a different integration, like a language or package. Each dashboard is its own file in these sub-directories in the JSON format.

Some integrations ship more than one dashboard, so there are more dashboards than directories.

- [Action Mailer](/dashboards/action_mailer/)
- [Active Job](/dashboards/active_job/)
- [AWS](/dashboards/aws/) (via AWS CloudWatch) — [generated, do not edit here](#generated-dashboards)
- [AWS CloudWatch Metric Streams](/dashboards/cloudwatch/)
- [Ecto](/dashboards/ecto/)
- [Erlang](/dashboards/erlang/)
- [Heroku](/dashboards/heroku/)
- [Karafka](/dashboards/karafka/)
- [Kubernetes](/dashboards/kubernetes/)
- [MongoDB](/dashboards/mongodb/) (via AppSignal for Ruby)
- [MongoDB](/dashboards/mongodb_vector/) (via Vector)
- [Next.js](/dashboards/nextjs/) (deprecated)
- [NGINX](/dashboards/nginx/)
- [Node.js](/dashboards/nodejs/) (the Postgres dashboard is deprecated)
- [Oban](/dashboards/oban/)
- [PostgreSQL](/dashboards/postgres/) (via Vector)
- [Process Memory](/dashboards/process_memory/)
- [Puma](/dashboards/puma/)
- [Render](/dashboards/render/)
- [Ruby VM](/dashboards/ruby_vm/)
- [Sidekiq](/dashboards/sidekiq/)
- [Web Vitals](/dashboards/web-vitals/)

### Generated dashboards

The dashboards in [`dashboards/aws/`](/dashboards/aws/) are not maintained in this repository. They are generated and published here by AppSignal's internal `cloudwatch-dashboards` repository, and any edit made to them here will be overwritten on the next publish.

Every other directory listed above is maintained in this repository and can be edited directly.

### Validation

To validate all dashboards in this repository, run the following command. To pass the validation, fix any issues that are printed.

```sh
rake validate
```
