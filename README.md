# JMX Collection using Kubernetes Annotations for Autodiscovery

### Clone this repository and cd into the directory

```
git clone https://github.com/burnsie7/k8s_jmx_auto.git
cd k8s_jmx_auto
```

### Configure RBAC permissions if your K8s instance is using RBAC.  More information can be found [here](https://docs.datadoghq.com/integrations/faq/using-rbac-permission-with-your-kubernetes-integration/).

`kubectl create -f datadog-serviceaccount.yaml`

### Update the port and jmx_url values in the applications yaml file.

Please update %%port%% with the known port of jmxremote.port.

The `jmx_url` value is optional and should be removed if not set.  By default the agent will attempt to connect to:

`service:jmx:rmi:///jndi/rmi://%%host%%:%%port%%/jmxrmi`

If you are using a different url, please update this value.  If not, please remove.

### Launch your application

`kubectl create -f my-java-app.yaml`

### Update <YOUR_API_KEY> in datadog-agent-jmx.yaml with a valid API key from [here](https://app.datadoghq.com/account/settings#api).

### Deploy Datadog JMX Agent Daemonset

`kubectl create -f datadog-agent-jmx.yaml`

### View containers from your kubernetes deployments on the Live Container page:

https://app.datadoghq.com/containers

### View JVM metrics in the Datadog metric explorer:

https://app.datadoghq.com/metric/explorer?&exp_metric=jvm.cpu_load.process&exp_scope=&exp_agg=avg&exp_row_type=metric

See complete documentation here: https://docs.datadoghq.com/agent/kubernetes/daemonset_setup/
