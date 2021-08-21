# Context
Observability Stack
* Prometheus
* Alertmanager
* Grafana

# Components
## Docker-compose
* [Environment variables in Compose](https://docs.docker.com/compose/environment-variables/)

## Grafana
### Environemnt variables
* [Configure with environment variables](https://grafana.com/docs/grafana/latest/administration/configuration/#configure-with-environment-variables)

All options in the configuration file can be overridden using environment variables using the syntax:

```
GF_<SectionName>_<KeyName>
```

Where the section name is the text within the brackets. Everything should be uppercase, . and - should be replaced by _. For example, if you have these configuration settings:

```
# default section
instance_name = ${HOSTNAME}

[security]
admin_user = admin

[auth.google]
client_secret = 0ldS3cretKey

[plugin.grafana-image-renderer]
rendering_ignore_https_errors = true
```

You can override them on Linux machines with:

```
export GF_DEFAULT_INSTANCE_NAME=my-instance
export GF_SECURITY_ADMIN_USER=owner
export GF_AUTH_GOOGLE_CLIENT_SECRET=newS3cretKey
export GF_PLUGIN_GRAFANA_IMAGE_RENDERER_RENDERING_IGNORE_HTTPS_ERRORS=true
```