# openshift-vllm-monitor-dashboard

This project directly borrows from the [Grafana dashboard in AI On OpenShift](https://ai-on-openshift.io/odh-rhoai/kserve-uwm-dashboard-metrics/#install-the-rhoai-metrics-grafana-and-dashboards-for-single-serving-models) making use of the fact that OpenShift Observe Dashboards can parse Grafana dashboard JSON.

This is a starting point but there are definitely rough edges, so feel free to contribute!

## Kustomize

There are 3 Kustomize options with one overlay to give maximal options.

* cluster-monitoring: Enables user workload monitoring in OpenShift
* dashboard: Code for monitoring your vLLM workloads
* * There is a `base` option which only deploys the dashboard into the monitoring stack. The `overlays` option will wire up all of the necessary monitoring configurations for OpenShift (see the other two options here in the list) as well as the dashboard.
* istio-monitoring: Enables monitoring of Service Mesh workloads

## Non-admin users

This repo creates a ClusterRole with permissions to be able to see the dashboard. You will need to attach it to any non-admin user who needs viewing permissions. Note that as of this writing, this corresponds to the `cluster-monitoring-view` ClusterRole. You can do this imperatively through the following command:

```sh
oc adm policy add-cluster-role-to-user dashboard-viewer <user>
```