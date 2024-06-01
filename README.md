# Synology SNMP Exporter for Prometheus

Most complete settings for Synology DSM 7.2 and snmp_exporter 0.26

* Install docker image - https://registry.hub.docker.com/r/ricardbejarano/snmp_exporter/
* Mount your configuration at /snmp.yml


## Prometheus config example:

```
  - job_name: 'synology_snmp_exporter'
    static_configs:
      - targets: ['synology_device_ip_1', 'synology_device_ip_2']
    metrics_path: /snmp
    params:
      module: [synology, if_mib, hrStorage]
    relabel_configs:
      - source_labels: [__address__]
        target_label: __param_target
      - source_labels: [__param_target]
        target_label: instance
      - source_labels: [__param_target]
        regex: (.*)
        replacement: snmp_docker_host:9116
        target_label: __address__
```

* synology_device_ip_1 and synology_device_ip_2 - IP address for Synology devices
* snmp_docker_host - IP address where runnging snmp_exporter

## Grafana dashboards:

* https://grafana.com/grafana/dashboards/14284-synology-nas-details/
* https://grafana.com/grafana/dashboards/14364-synology-nas-overview/
* https://grafana.com/grafana/dashboards/18643-synology-snmp/
* https://grafana.com/grafana/dashboards/18349-synology-router-overview/


## Sources:

* https://github.com/clralab/boilerplates/blob/main/docker-compose/snmp_exporter/config/snmp.yml
* https://github.com/prometheus/snmp_exporter/blob/main/snmp.yml
* https://github.com/ddiiwoong/synology-prometheus/blob/master/snmp-synology/snmp.yml
