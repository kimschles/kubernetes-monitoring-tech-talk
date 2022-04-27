Best Pratices in Monitoring a Kubernetes Cluster 

## Install kube-prometheus-stack
- create a monitoring namespace 
- add prometheus-community repo
`helm repo add prometheus-community https://prometheus-community.github.io/helm-charts`
`helm repo update prometheus-community`
- use helm to install the kube-prometheus-stack
`helm install kube-prometheus-stack prometheus-community/kube-prometheus-stack -n monitoring -f values.yaml` 


## Poke around prom, alertmanager grafana and alertmanager
Prometheus and Alertmanager Web Panel
`kubectl port-forward svc/kube-prometheus-stack-prometheus 9090:9090 -n monitoring` 

`kubectl port-forward alertmanager-kube-prometheus-stack-alertmanager-0 9093 -n monitoring`

Grafana Web Panel 
`kubectl port-forward svc/kube-prometheus-stack-grafana 3000:80 -n monitoring`

```
user: admin
pass: prom-operator
```

## Generate Slack Webhook
* Go to api.slack.com 
* Create an app 
* Turn on the 'Enable Incoming Webhooks' option 
* Generate a Webhook URL 
* Test with a POST request from cURL 

## Setup AlertManager and Alert Rules 

### Configure AlertManager 

`helm upgrade --reuse-values -f alertmanager-config.yaml kube-prometheus-stack prometheus-community/kube-prometheus-stack -n monitoring`


### Setup an alert using a default alert from AlertManager
`helm upgrade --reuse-values -f alert-rules.yaml kube-prometheus-stack prometheus-community/kube-prometheus-stack -n monitoring`

## Loki 






