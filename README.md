# JMX Collection using Kubernetes Annotations for Autodiscovery

1.  Configure RBAC permissions

`kubectl create -f datadog-serviceaccount.yaml`

2.  Deploy your application

`kubectl create -f my-java-app.yaml`

3.  Deploy Datadog JMX Agent Daemonset

`kubectl create -f datadog-agent-jmx.yaml`

4.  View containers from your kubernetes deployments on the Live Container page: 

https://app.datadoghq.com/containers

5.  View JVM metrics in the Datadog metric explorer:

https://app.datadoghq.com/metric/explorer?&exp_metric=jvm.cpu_load.process&exp_scope=&exp_agg=avg&exp_row_type=metric

See complete documentation here: https://docs.datadoghq.com/agent/kubernetes/daemonset_setup/
