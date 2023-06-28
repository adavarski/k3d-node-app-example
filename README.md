
<div align="center">
<a href="https://k3d.io/#quick-start" target="_blank">
  <img width="100" alt="k3s" src="https://k3d.io/static/img/k3d_logo_black_blue.svg" />
</a><br><br>
  <h2 align="center">
     Local stack using K3D
  </h2>
</div>

---

## Simple node app (for playgrounds & LABS)

To run the application, you will need to have:

- [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [k3d](https://k3d.io/#quick-start)
- [Helm (OPTIONAL)](https://helm.sh/docs/intro/install/) 


## Usage

```bash
# Build image
$ cd app && docker build -t davarski/api-produto:v1.0.0 .

# Push image
$ docker davarski/api-produto:v1.0.0

# Create cluster using k3d
$ k3d cluster create --servers 1 --agents 2 -p "8080:30000@loadbalancer" -p "8181:30001@loadbalancer" -p "8282:30002@loadbalancer"

# Apply kubernetes manifests for node app
$ kubectl apply -f ./kubernetes/

# Create ingress for api (Swagger)
$ kubectl apply -f ingresses/api-swagger.png
```

## Access Swagger (api)

Browser: http://api.192.168.1.99.nip.io:8080

Screenshot:

<img src="screenshots/api-swagger.png?raw=true" width="8000">


#############################
### MONITORING (OPTIONAL) ###
#############################
```
# Add repo helm prometheus
$ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
$ helm repo update

# Install prometheus on cluster
$ helm install prometheus prometheus-community/prometheus --values ./prometheus/values.yaml

# Dashboard grafana 
$ localhost:8181

# Add repo helm grafana
$ helm repo add grafana https://grafana.github.io/helm-charts
$ helm repo update

# Install grafana on cluster
$ helm install grafana grafana/grafana --values ./grafana/values.yaml

# Dashboard grafana 
$ localhost:8282
```


```

