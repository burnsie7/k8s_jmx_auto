# JMX Collection using Kubernetes Annotations for Autodiscovery

1. Clone this repository and cd into the directory

```
git clone https://github.com/burnsie7/k8s_jmx_auto.git
cd k8s_jmx_auto
```

2. Configure RBAC permissions if your K8s instance is using RBAC.  More information can be found [here](https://docs.datadoghq.com/integrations/faq/using-rbac-permission-with-your-kubernetes-integration/).

`kubectl create -f datadog-serviceaccount.yaml`

3. Update yaml files.

The configuration is slightly different if you define your kubernetes pods directly (i.e kind:Pod) or if you define them indirectly (i.e Deployments, Replication Controllers, etc).

If you use `kind:Pod` in your manifest refer to **my-java-app-pod.yaml**.  Otherwise, refer to **my-java-app-deployment.yaml**.  If you will be enabling APM/Tracing use the corresponding files in the **apm_enabled** directory.

Update `%%port%%` with the known port of jmxremote.port.

The `jmx_url` value is optional and should be removed if not set.  By default the agent will attempt to connect to:

`service:jmx:rmi:///jndi/rmi://%%host%%:%%port%%/jmxrmi`

If you are using a different url, please update this value.  If not, please omit.

4. Launch your application

`kubectl create -f my-java-app-<your_pod_def>.yaml`

5. Update `<YOUR_API_KEY>` in datadog-agent-jmx.yaml with a valid API key from [here](https://app.datadoghq.com/account/settings#api).  If you are enabling APM/Tracing use the corresponding file in the **apm_enabled** directory.

6. Deploy Datadog JMX Agent Daemonset

`kubectl create -f datadog-agent-jmx-<optional-apm>.yaml`

7. View containers from your kubernetes deployments on the Live Container page:

https://app.datadoghq.com/containers

8. View JVM metrics in the Datadog metric explorer:

https://app.datadoghq.com/metric/explorer?&exp_metric=jvm.cpu_load.process&exp_scope=&exp_agg=avg&exp_row_type=metric

See complete documentation [here](https://docs.datadoghq.com/agent/kubernetes/daemonset_setup/).
