# AppSignal Magic Dashboards

The `public_config` repository is a place for AppSignal's public configuration. This is currently used for the Magic Dashboards.

## Magic Dashboards

Magic Dashboards can be found in the `dashboards/` sub directory. Each directory is a different integration, like a language or package. Each dashboard is its own file in these sub-directories in the JSON format.

### Validation

To validate all dashboards in this repository, run the following command. To pass the validation, fix any issues that are printed.

```
rake validate
```
