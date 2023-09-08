# grafaml

Create Grafana Dashboards from YAML using Helm Chart templating.

Find the full documentation at [Github](https://github.com/erNail/grafaml).

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| annotations | object | `{"enabled":false,"list":[{"expr":"up","name":"My Annotation"}]}` | The dashboard annotations. Ref: [Grafana JSON Visualizations](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/annotate-visualizations/)  |
| annotations.list | list | `[{"expr":"up","name":"My Annotation"}]` | Grafana does not provide a full list with options. To find out about other options, create the desired annotations in the Grafana UI, inspect the JSON, and transform it to YAML. |
| editable | bool | `true` | Wether the dashboard is editable or not. Ref: [Grafana JSON Fields](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/view-dashboard-json-model/#json-fields)  |
| extraLabels | object | `{"created-with":"grafaml"}` | Additional labels to add to the ConfigMap. Ref: [Kubernetes Labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)  |
| graphTooltip | string | `"0"` | The tooltip behavior of the dashboard. 0 for no shared crosshair or tooltip (default), 1 for shared crosshair, 2 for shared crosshair and shared tooltip. Ref: [Grafana JSON Fields](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/view-dashboard-json-model/#json-fields)  |
| onlyRenderDashboardJson | bool | `false` | Wether to render only the dashboard JSON, or the entire ConfigMap. Set this to true if you are not interested in deploying the Dashboard in a Kubernetes Cluster. Use `helm template ./charts/grafaml --set onlyRenderDashboardJson=true | tail -n +3 > dashboard.json` to get the dashboard JSON model as a file.  |
| panels | object | `{"list":[{"targets":[{"expr":"up"}],"title":"Prometheus Targets Up","type":"stat"},{"description":"Memory and CPU Usage","targets":[{"expr":"(1 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes)) * 100","legendFormat":"Memory Usage"},{"expr":"sum by (instance, job)(avg by (mode, instance) (rate(node_cpu_seconds_total{mode!='idle'}[2m]))) * 100","legendFormat":"CPU Usage"}],"title":"Resource Usage in Percent","type":"stat"},{"targets":[{"expr":"(1 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes)) * 100"}],"title":"Memory Usage in Percent over Time","type":"timeseries"},{"targets":[{"expr":"sum by (instance, job) (avg by (mode, instance) (rate(node_cpu_seconds_total{mode!='idle'}[2m])))"}],"title":"CPU Usage in Percent over Time","type":"timeseries"}],"panelHeight":8,"panelWidth":12}` | The dashboard panels. The positioning will be handled automatically, so there is no need to define the "gridPos" Ref: [Grafana JSON Panels](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/view-dashboard-json-model/#panels)  |
| panels.list | list | `[{"targets":[{"expr":"up"}],"title":"Prometheus Targets Up","type":"stat"},{"description":"Memory and CPU Usage","targets":[{"expr":"(1 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes)) * 100","legendFormat":"Memory Usage"},{"expr":"sum by (instance, job)(avg by (mode, instance) (rate(node_cpu_seconds_total{mode!='idle'}[2m]))) * 100","legendFormat":"CPU Usage"}],"title":"Resource Usage in Percent","type":"stat"},{"targets":[{"expr":"(1 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes)) * 100"}],"title":"Memory Usage in Percent over Time","type":"timeseries"},{"targets":[{"expr":"sum by (instance, job) (avg by (mode, instance) (rate(node_cpu_seconds_total{mode!='idle'}[2m])))"}],"title":"CPU Usage in Percent over Time","type":"timeseries"}]` | Check [Grafana JSON Panels](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/view-dashboard-json-model/#panels) for more options. Grafana does not provide a full list with options. To find out about other options, create the desired panels in the Grafana UI, inspect the panel JSON, and transform it to YAML. For example dashboards created with grafaml, check out the [example charts](https://github.com/erNail/grafaml/tree/main/example-charts)  |
| panels.panelWidth | int | `12` | Grafana dashboards have a maximum width of 24. The panel width has to be a factor of 24.  |
| refresh | string | `"30s"` | The auto-refresh interval. Ref: [Grafana JSON Fields](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/view-dashboard-json-model/#json-fields)  |
| style | string | `"dark"` | The style of the dashboard, either "dark" or "light". Ref: [Grafana JSON Fields](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/view-dashboard-json-model/#json-fields)  |
| tags | list | `["grafaml"]` | The tags of the dashboard. Ref: [Grafana JSON Fields](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/view-dashboard-json-model/#json-fields)  |
| templating | object | `{"enabled":false,"list":[{"allFormat":"wildcard","current":{"text":"prod","value":"prod"},"includeAll":true,"multi":true,"name":"environment","query":"tag_values(cpu.utilization.average,env)","type":"query"}]}` | The dashboard template variables. Ref: [Grafana JSON Templating](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/view-dashboard-json-model/#templating)  |
| templating.list | list | `[{"allFormat":"wildcard","current":{"text":"prod","value":"prod"},"includeAll":true,"multi":true,"name":"environment","query":"tag_values(cpu.utilization.average,env)","type":"query"}]` | Check [Grafana JSON Templating](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/view-dashboard-json-model/#templating) for all possible options.  |
| time | object | `{"from":"now-6h","to":"now"}` | The time range for the dashboard. Ref: [Grafana JSON Fields](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/view-dashboard-json-model/#json-fields)  |
| timepicker | object | `{"collapse":false,"enable":true,"enabled":false,"notice":false,"now":true,"status":"Stable","type":"timepicker"}` | The configuration of the time picker. Check [Grafana JSON Timepicker](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/view-dashboard-json-model/#timepicker) for all possible options. Ref: [Grafana JSON Timepicker](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/view-dashboard-json-model/#timepicker)   |
| timepicker.enable | bool | `true` | Wether the timepicker is enabled or not.  |
| timepicker.enabled | bool | `false` | Wether the timepicker configuration is rendered or not.  |
| timezone | string | `"browser"` | The timezone of the dashboard, either "utc" or "browser". Ref: [Grafana JSON Fields](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/view-dashboard-json-model/#json-fields)  |
| title | string | `"Grafana Dashboard"` | The displayed title of the Dashboard. Ref: [Grafana JSON Fields](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/view-dashboard-json-model/#json-fields)  |