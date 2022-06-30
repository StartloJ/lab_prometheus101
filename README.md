# All in one workshop for Prometheus stack

We're prepared `docker-compose` workshop to provision prometheus and grafana stack to proved of concept.
So, we can command `up` to provision lab and learn about them.

## Prerequisite

You should verify following:

- docker
- docker-compose
- web browser

## Support component

- Prometheus **v2.29.2**
- Node exporter **v1.2.2**
- Alertmanager **v0.23.0**
- Grafana **8.1.2**
- cAdvisor **v0.40.0**
- Blackbox exporter **v0.21.1**
- simple HTTP app

## Step to use workshop

1. Run `docker-compose`

    ```bash
    $ docker-compose up -d
    Creating lab_prometheus101_node-exporter_1 ... done
    Creating lab_prometheus101_simple_http1_1  ... done
    Creating lab_prometheus101_grafana_1       ... done
    Creating lab_prometheus101_cadvisor_1      ... done
    Creating lab_prometheus101_alertmanager_1  ... done
    Creating lab_prometheus101_blackbox_1      ... done
    Creating lab_prometheus101_prometheus_1    ... done
    ```

2. Change component configure in folder alertmanager, grafana, and prometheus. Then recreate docker-compose

    ```bash
    $ docker-compose up -d --force-recreate
    Recreating lab_prometheus101_node-exporter_1 ... done
    Recreating lab_prometheus101_simple_http1_1  ... done
    Recreating lab_prometheus101_grafana_1       ... done
    Recreating lab_prometheus101_cadvisor_1      ... done
    Recreating lab_prometheus101_alertmanager_1  ... done
    Recreating lab_prometheus101_blackbox_1      ... done
    Recreating lab_prometheus101_prometheus_1    ... done
    ```

3. Go to browser and see the result.
   1. For prometheus: `http://localhost:19090`
   2. For grafana: `http://localhost:3000`
   3. For alertmanager: `http://localhost:9093`

### Custom the Grafana resources

You can store owned grafana dashboard in JSON file format in path `grafana/provisioning/dashboards/temp`
Then, you can edit initial configure for grafana dashboard in `grafana/provisioning/dashboards/all.yaml`
See example:  

```yaml
apiVersion: 1
providers:
- name: 'Example'
  orgId: 1
  folder: ''
  type: file
  disableDeletion: false
  updateIntervalSeconds: 10
  options:
    path: /etc/grafana/provisioning/dashboards/temp/
```

Or customize data source in `grafana/provisioning/datasource/all.yaml`
See example:

```yaml
apiVersion: 1
datasources:
  - access: direct
    editable: true
    is_default: true
    name: Prometheus
    org_id: 1
    type: prometheus
    url: http://prometheus:9090
    version: 1
```
