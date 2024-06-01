# Synology SNMP Exporter for Prometheus

Most complete settings for Synology DSM 7.2 and snmp_exporter 0.26

* install docker image - https://registry.hub.docker.com/r/ricardbejarano/snmp_exporter/
* Mount your configuration at /snmp.yml


## Prometheus config example:

``
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
``

* synology_device_ip_1 and synology_device_ip_2 - IP address for Synology devices
* snmp_docker_host - IP address where runnging snmp_exporter
