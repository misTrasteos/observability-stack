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

## Alertmanager
### amtool
* [amtool](https://github.com/prometheus/alertmanager#amtool)
* [amtool Debian man pages](https://manpages.debian.org/unstable/prometheus-alertmanager/amtool.1.en.html)

#### Examples
**Find silences**

amtool --alertmanager.url=http://alertmanager silence query environment="DEVELOP" alertname="Something bad is happening"
ID  Matchers  Ends At  Created By  Comment


**Add a silence**

amtool --alertmanager.url=http://alertmanager silence add environment="DEVELOP" alertname="Something bad is happening" --author="me" --duration="1y" --comment="Do not bother me for a long time"
85369874-6g8h-12c5-abc3-0cajebad8743


**Silence has been created**

amtool --alertmanager.url=http://alertmanager silence query environment="DEVELOP" alertname="Something bad is happening"
ID                                    Matchers                                                Ends At                  Created By                           Comment
85369874-6g8h-12c5-abc3-0cajebad8743  environment="DEVELOP" alertname="Something bad is happening"  2023-11-07 08:54:03 UTC  me  Do not bother me for a long time
