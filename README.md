# drupal-demo-application
This repository will store the code to run the drupal application using helm

# Deploy Ingress Controller on GKE

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.43.0/deploy/static/provider/cloud/deploy.yaml

```

# Deploy drupal using Helm chart

```
 helm install druapltest bitnami/drupal -f values.yaml 

```
You can customize the values.yaml file as per your need

# Deploy using Ingress

In `values.yaml` file - update the below tag
You can provide the hostname which you want to use. 
```
ingress:
  ## Set to true to enable ingress record generation
  ##
  enabled: true
  hostname: drupal.local
  path: /

```

If you are doing the local testing then 
update the `/etc/hosts` file with the below content. You can get the ingressIp using `kubectl get ingress'

```
ingressIp     drupal.local
```
# Login to drupal

```
http://drupal.local/
Click on Login at the top right corner

Username : user
password : Run this command : echo echo Password: $(kubectl get secret --namespace default druapltest-drupal -o jsonpath="{.data.drupal-password}" | base64 --decode)
```

# References

1. https://github.com/bitnami/charts/tree/master/bitnami/drupal/#installing-the-chart
