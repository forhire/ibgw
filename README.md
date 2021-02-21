# Helm 3 charts to deploy Interactive Brokers Gateway and other IB related containers to Kubernets

HELM 3 chart to deploy IB Gateway running in Docker to a Kubernetes cluster. Currently has basic TCP port monitoring so Kubernetes will restart the instance, if it stops responding.

### Docker Hub image

This HELM chart deploys the following Docker container by default. This can be overridden in the values.yaml:

* https://hub.docker.com/r/forhire/ibgwdocker

### Deploying

* To deploy, create a values.yaml outside this repo with your IB Gateway credentials

```
IBAuth: true
TWSUSERID: "YOUR_IB_USERNAME_HERE"
TWSPASSWORD: "YOUR_IB_PASSWORD_HERE"
VNC_PASSWORD: "YOUR_VNC_PASSWORD_HERE"
```

and 

```export KUBECONFIG=/path/to/your/kubeconfig```

Then, deploy with:

```
helm3 repo add ibgw-forhire https://forhire.github.io/ibgw/ # to add this repo

helm3 install -n ibroker-paper ibgw ibgw-forhire/ibgw -f values.yaml 

helm install -n ibroker-paper backtrader ibgw-forhire/backtrader-helm # To install Backtrader Anaconda Jupyter Notebook in the ibroker-paper namespace

```

### Troubleshooting

Kubernetes kubectl commands can be used for troubleshooting. Typically:
```kubectl get all -n namespace```

to get the POD name.

```kubectl describe pod/ibgw-unique-values -n namespace```

to show details about the POD. 
