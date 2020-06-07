# Kubernetes SSL

## Yaml File Description

`Note: I used kubectl through out the process`

## app-deployment.yaml

This file will be having the detils for the application components 
(deployment) and its related service.

* Service - Configure the ports in which the application can be accessed
* Deployment - Ensure the container port is in line with the port given in Service.

Deploy the pod using below command

`kubectl apply -f app-deployment.yaml`

## nginx-ingress-controller.yaml

This file will deploy all the components related for nginx controller.

Deploy using below command and no changes required in the file

`kubectl apply -f nginx-ingress-controller.yaml`

## lb-service.yaml

This file will deploy load balancer for the app. Things to be noted are the ports which should be open to access the app. 

**This will take few minutes to see the LB in DO**

Deploy using below command after having the port configured

`kubectl apply -f lb-service.yaml`

## ingress-resource.yaml

This file will deploy ingress resource. Things to be noticed are class, cluster-issuer, hosts, host, serviceName and servicePort. 

Deploy using below command once have the correct details in yaml

`kubectl apply -f ingress-resource.yaml`

## cert-manager.yaml

This will create cert manager resources. For this namespace `cert-manager` to be created before deploying. Create namespace use the below command.

`kubectl create namespace cert-manager`

Then deploy using the below command and no change required for yaml

`kubectl apply --validate=false -f cert-manager.yaml`

## staging/prod_issuer.yaml

Create issuer using the files based on your environment. Thing to be noticed are email, privateKeySecretRef (should match cluster-issuer from ingress-resource.yaml) and class (should match class from ingress-resource.yaml)

Deploy using below command once have the correct details in yaml

`kubectl create -f staging_issuer.yaml/prod_issuer.yaml`
