---
title: "Elastic Search"
aliases:
  - /en/master/tools/elastic-search/
---


Add the `elasticsearch` service under the `services` section in `.docksal/docksal.yml`:

```yaml
  # Elastic Search
  elasticsearch:
    extends:
      file: ${HOME}/.docksal/stacks/services.yml
      service: elasticsearch
```

Apply new configuration with `fin project start` (`fin p start`).

Elastic Search will be exposed on a random port. Use `fin project status` to determine which port Elastic Search is exposed on, e.g.,

```
14:06:05 ~/Projects/drupal8
§ fin ps
         Name                        Command                  State                     Ports              
-----------------------------------------------------------------------------------------------------------
drupal8_cli_1             /opt/startup.sh supervisord      Up (healthy)   22/tcp, 3000/tcp, 9000/tcp       
drupal8_db_1              /entrypoint.sh mysqld            Up             0.0.0.0:32768->3306/tcp          
drupal8_elasticsearch_1   /usr/local/bin/docker-entr ...   Up             0.0.0.0:32770->9200/tcp, 9300/tcp
drupal8_web_1             httpd-foreground   
```

In the example above, Elastic Search port `9200` is exposed on the host as `32770` and can be accessed at `192.168.64.100:32770`.

## Assigning a Static Port

To have a static port assigned, override the `ELASTICSEARCH_PORT_MAPPING` variable in `.docksal/docksal-local.env`:

```
ELASTICSEARCH_PORT_MAPPING='9200:9200'
```
In this case, the current project elastic search will be accessible at `192.168.64.100:9200`.
