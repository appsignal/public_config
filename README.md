# AppSignal Magic Dashboards

The `public_config` repository is a place for AppSignal's public configuration. This is currently used for the Magic Dashboards.

## Magic Dashboards

Magic Dashboards can be found in the `dashboards/` sub directory. Each directory is a different integration, like a language or package. Each dashboard is its own file in these sub-directories in the JSON format:

- [Action Mailer](/dashboards/action_mailer/)
- [Active Job](/dashboards/active_job/)
- [Erlang](/dashboards/erlang/)
- [Heroku](/dashboards/heroku/)
- [MongoDB](/dashboards/mongodb/)
- [Next.js](/dashboards/nextjs/) (deprecated)
- [NGINX](/dashboards/nginx/)
- [Node.js](/dashboards/nodejs/)
- [Oban](/dashboards/oban/)
- [Puma](/dashboards/puma/)
- [Ruby VM](/dashboards/ruby_vm/)
- [Sidekiq](/dashboards/sidekiq/)
- [Karafka](/dashboards/karafka/)
- [Web Vitals](/dashboard/web-vitals/) (deprecated)

### Validation

To validate all dashboards in this repository, run the following command. To pass the validation, fix any issues that are printed.

```
rake validate
```
