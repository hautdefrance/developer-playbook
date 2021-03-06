# Plattform

## Platform & Infrastructure

The platform provides the tools to increase productivity it should abstract away the operations tasks to get fast feedback loops but it also should design for change as we should be prepared that we have to change in the future:

* Serverless \(great speed and plattform\) vs Istio \(great portability\) or Flask on Serverless for speed and platform but migratable? 
* SaaS Components for 
  * [Persistance - DBaaS \(DynamoDB\)](persistance-dbaas/) 
  * [IAM - IAMaaS ](iam-iamaas.md)
  * [Event Driven / Streaming aaS](event-driven-streaming-aas/)
  * [AI - AIaaS](ai-aiaas.md)
  * Reliability aaS - Logging
  * ... but don't forget ports and adapters

**Architecture Decisions**

1. [Select Application Runtime: Serverless over Istio for now](https://github.com/denseidel/developer-playbook/blob/master/adr/2018-02-18%20Select%20a%20application%20runtime%20for%20plattform.md)

## C_ontainers_ or _serverless_

Serverless increases the efficiency of your implementation. But at the same time you bind yourself very tightly to a special vendor like Amazon with AWS Lambda. Another Option is to use a multi cloud apporach and use Containers as your abstraction layer - Lambdas also use containers themselves. Downside you don't have the you pay only what you use and you miss the non functional features the platform provides like monitoring, routing ... This is where service meshs like Istio come into play.

* [https://serverless.com/blog/serverless-faas-vs-containers/](https://serverless.com/blog/serverless-faas-vs-containers/)
* [http://rancher.com/containers-vs-serverless-computing/](http://rancher.com/containers-vs-serverless-computing/)

**Can you integrate serverless with a service mesh and when to do it?**

* [https://medium.com/@jeffzzq/how-to-integrate-an-aws-lambda-function-into-your-kubernetes-service-mesh-5d665f351675](https://medium.com/@jeffzzq/how-to-integrate-an-aws-lambda-function-into-your-kubernetes-service-mesh-5d665f351675)

## Containers

### Infrastructure Automation with - Terraform

* [https://www.udemy.com/learn-devops-infrastructure-automation-with-terraform/](https://www.udemy.com/learn-devops-infrastructure-automation-with-terraform/)
* [https://github.com/wardviaene/terraform-course](https://github.com/wardviaene/terraform-course)
* [https://aws.amazon.com/blogs/apn/terraform-beyond-the-basics-with-aws/](https://aws.amazon.com/blogs/apn/terraform-beyond-the-basics-with-aws/)
* [https://github.com/shuaibiyy/awesome-terraform](https://github.com/shuaibiyy/awesome-terraform)
* [https://github.com/mcuadros/terraform-provider-helm](https://github.com/mcuadros/terraform-provider-helm)
* [https://www.terraform.io/docs/providers/aws/guides/eks-getting-started.html](https://www.terraform.io/docs/providers/aws/guides/eks-getting-started.html)
* [https://www.terraform.io/intro/getting-started/install.html](https://www.terraform.io/intro/getting-started/install.html)

### Setup Docker Environment

[Python Connexion Docker Tutorial](https://medium.com/@ssola/building-microservices-with-python-part-2-9f951199094a)

1. [Install Docker](https://docs.docker.com/docker-for-mac/install/)

Create Dockerfile

Build the dockerfile \([tagging](http://container-solutions.com/tagging-docker-images-the-right-way/)\).

```text
docker build -t products:1.0.0 .
```

### Setup Kubernetes

When you want to bring your docker containers into production - you need to orchestrate those containers. This is where [Kubernetes](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/) helps getting a reliable and reporducable, production read \( scalable ...\), "simple" \(routes, services, ...\), vendor independent \(compared to serverless\) and multi cloud ready solution.

[https://de.slideshare.net/InfoQ/building-a-microservices-platform-with-kubernetes](https://de.slideshare.net/InfoQ/building-a-microservices-platform-with-kubernetes)

#### Local Development Environment

Start minikube \[[Source](https://kubernetes.io/docs/getting-started-guides/minikube/)\]

```text
minikube start --memory 4096
```

Setup [Helm](https://docs.helm.sh/) and tiller \[[Source](https://docs.helm.sh/using_helm/#quickstart)\] and Istio \[[Source](https://istio.io/docs/setup/kubernetes/quick-start.html)\] / **helm install currently not working check back in a few weeks.**

```text
#find the locally configure cluster where tiller will be installed by helm
kubectl config current-context

#install helm on client / ci/cd pipeline
brew install kubernetes-helm

#https://github.com/istio/istio/tree/master/install/kubernetes/helm/istio
git clone https://github.com/istio/istio.git
cd istio
kubectl create -f install/kubernetes/helm/helm-service-account.yaml

# for production secure helm https://docs.helm.sh/using_helm/#securing-your-helm-installation
helm init \ 
--tiller-tls \ 
--tiller-tls-verify \ 
--tiller-tls-ca-cert=ca.pem \ 
--tiller-tls-cert=cert.pem \ 
--tiller-tls-key=key.pem \ 
--service-account=tiller

helm install install/kubernetes/helm/istio --name istio
```

To build images directly in minishift use minikube's built-in docker daemon:

```text
eval $(minikube docker-env)
docker ps
```

Create Env variables: [https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/](https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/)

Create secrets: [https://kubernetes.io/docs/concepts/configuration/secret/](https://kubernetes.io/docs/concepts/configuration/secret/)

```text
kubectl create secret generic gcloud-cred --from-file=/Users/den/.config/keys/marketplaceapp.json
```

#### Production Environment

In my experience maintaining and setting up a kuebrnetes cluster is hard - there are now many great fully manged offerings: Openshift, AWS EKS, IBM,  
Microsoft, Google GKE, Joyent Kubernetes

**TODO**

### Setup Service Mesh

#### What is Istio?

* Source:
  * [https://programmaticponderings.com/2017/12/22/deploying-and-configuring-istio-on-google-kubernetes-engine-gke/](https://programmaticponderings.com/2017/12/22/deploying-and-configuring-istio-on-google-kubernetes-engine-gke/) \(Udemy Course Istio\)
  * Istio Introduction: 
    * [https://www.youtube.com/watch?v=muoCgHkkPx](https://www.youtube.com/watch?v=muoCgHkkPxo)
    * [https://istio.io/docs/concepts/what-is-istio/overview.html](https://istio.io/docs/concepts/what-is-istio/overview.html)
* Improve development time \(library vs sidecar\)
* improve plattform \(tracing, a/b testing, dashboarding, service graph\)
* ... without changing the code!

### Tutorial

Setup a kubernetes cluster \(see chapter above\) then install Istio:

```text
curl -L https://git.io/getLatestIstio | sh -
export PATH="$PATH:/Users/den/repo/istio-0.5.0/bin"
cd istio-0.5.0
kubectl apply -f install/kubernetes/istio.yaml
kubectl apply -f install/kubernetes/istio-auth.yaml
kubectl apply \
  -f install/kubernetes/addons/prometheus.yaml \
  -f install/kubernetes/addons/grafana.yaml \
  -f install/kubernetes/addons/servicegraph.yaml \
  -f install/kubernetes/addons/zipkin.yaml

openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /tmp/tls.key -out /tmp/tls.crt -subj "/CN=d10l.de"
kubectl create -n istio-system secret tls istio-ingress-certs --key /tmp/tls.key --cert /tmp/tls.crt

#get external ip
kubectl get svc -n istio-system
minikube ip
export GATEWAY_URL=$(kubectl get po -l istio=ingress -n istio-system -o 'jsonpath={.items[0].status.hostIP}'):$(kubectl get svc istio-ingress -n istio-system -o 'jsonpath={.spec.ports[0].nodePort}')
Deploy app
kubectl apply -f <(istioctl kube-inject -f samples/bookinfo/kube/bookinfo.yaml)
kubectl get services
```

Deploy

```text
kubectl apply -f <(istioctl kube-inject -f ./deployment.yaml)
```

Set it up \(you should do this with [DevSecOps ](https://github.com/denseidel/developer-playbook/tree/0de27ab0d5cf97c58fdeec5a26159b0fa55f0ef2/devsecops.md)in Mind \(Automation is everything!\):

[https://www.joyent.com/blog/kubernetes-the-easy-way](https://www.joyent.com/blog/kubernetes-the-easy-way)

[https://www.terraform.io/docs/providers/kubernetes/guides/getting-started.html](https://www.terraform.io/docs/providers/kubernetes/guides/getting-started.html) ?

Register with [Google Cloud Platform](https://cloud.google.com/?hl=de)

Setup SDK locally and in Pipeline

Install Google Cloud SDK \(MacOS\)

[https://cloud.google.com/sdk/docs/quickstart-macos](https://cloud.google.com/sdk/docs/quickstart-macos)

```text
brew cask install google-cloud-sdk
```

Install Istio: [https://istio.io/docs/setup/kubernetes/quick-start.html](https://istio.io/docs/setup/kubernetes/quick-start.html)

```text
#Retrieve your credentials for kubectl (replace <cluster-name> with the name of the cluster you want to use, and <zone> with the zone where that cluster is located):
gcloud container clusters get-credentials <cluster-name> --zone <zone> --project <project-name>
Grant cluster admin permissions to the current user (admin permissions are required to create the necessary RBAC rules for Istio):
kubectl create clusterrolebinding cluster-admin-binding --clusterrole=cluster-admin --user=$(gcloud config get-value core/account)
#download istio
curl -L https://git.io/getLatestIstio | sh -
# go to folder
cd istio-0.5.0
# add istiocrl
export PATH=$PWD/bin:$PATH
#Install Istio and enable mutual TLS authentication between sidecars.:
kubectl apply -f install/kubernetes/istio-auth.yaml
# Optional: If your cluster has Kubernetes version 1.9 or greater, and you wish to enable automatic proxy injection, install the sidecar injector webhook using the instructions at (/docs/setup/kubernetes/sidecar-injection.html#automatic-sidecar-injection).

#Verify
kubectl get svc -n istio-system
kubectl get pods -n istio-system

#create/update the namespace for my application with istio enabled
kubectl label namespace <namespace> istio-injection=enabled
# isnstall BookInfo Sample https://istio.io/docs/guides/bookinfo.html
kubectl create -n <namspace> -f <your-app-spec>.yaml
```

Access the non exposed components:

```text
#login first
gcloud container clusters get-credentials marketplace-istio \
      --zone us-east1-b --project trusty-acre-156607

kubectl -n istio-system port-forward \
  $(kubectl -n istio-system get pod -l app=zipkin -o jsonpath='{.items[0].metadata.name}') \
  9411:9411 &

kubectl -n istio-system port-forward \
  $(kubectl -n istio-system get pod -l app=grafana -o jsonpath='{.items[0].metadata.name}') \
  3000:3000 &

kubectl -n istio-system port-forward \
  $(kubectl -n istio-system get pod -l app=servicegraph -o jsonpath='{.items[0].metadata.name}') \
  8088:8088 &

kubectl -n istio-system port-forward \
  $(kubectl -n istio-system get pod -l app=prometheus -o jsonpath='{.items[0].metadata.name}') \
  9090:9090 &

kubectl proxy (8080/ui -> management ui)
```

To enable TLS create certficate and deploy it as a secret and add the following to the ingress config \([https://istio.io/docs/tasks/traffic-management/ingress.html\](https://istio.io/docs/tasks/traffic-management/ingress.html%29\)

```text
---
###########################################################################
# Ingress resource (gateway)
##########################################################################
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  ...
spec:
  tls:
    - secretName: istio-ingress-certs # currently ignored
  rules:
  - ...

---
```

Add your own domain to the static ip address of the cluster: [https://cloud.google.com/kubernetes-engine/docs/tutorials/configuring-domain-name-static-ip](https://cloud.google.com/kubernetes-engine/docs/tutorials/configuring-domain-name-static-ip)

Find your static IP address:

```text
kubectl get ingress -o wide
```

Setup your DNS \(with Route53\) [https://serverless-stack.com/chapters/setup-your-domain-with-cloudfront.html](https://serverless-stack.com/chapters/setup-your-domain-with-cloudfront.html)

Remove untagged images and stopped containers [http://jimhoskins.com/2013/07/27/remove-untagged-docker-images.html](http://jimhoskins.com/2013/07/27/remove-untagged-docker-images.html)

```text
docker rmi $(docker images | grep "^<none>" | awk "{print $3}")
```

Small images [https://nickjanetakis.com/blog/alpine-based-docker-images-make-a-difference-in-real-world-apps](https://nickjanetakis.com/blog/alpine-based-docker-images-make-a-difference-in-real-world-apps)

testing with postman and different environments: [https://www.getpostman.com/docs/postman/environments\_and\_globals/variables](https://www.getpostman.com/docs/postman/environments_and_globals/variables)

Egress Rules currently don't work well with HTTPS [https://istio.io/blog/2018/egress-https.html](https://istio.io/blog/2018/egress-https.html) so better enable direct connection: [https://istio.io/docs/tasks/traffic-management/egress.html](https://istio.io/docs/tasks/traffic-management/egress.html)

```text
# minikube
kubectl apply -f <(istioctl kube-inject -f ./deployment.yaml --includeIPRanges=10.0.0.1/24)
#for gke check https://istio.io/docs/tasks/traffic-management/egress.html
gcloud container clusters describe marketplace-istio --zone=us-east1-b | grep -e clusterIpv4Cidr -e servicesIpv4Cidr
kubectl apply -f <(istioctl kube-inject -f ./deployment.yaml --includeIPRanges=10.12.0.0/14,10.15.240.0/20)
```

Mount Containers locally: [https://docs.docker.com/storage/bind-mounts/\#start-a-container-with-a-bind-mount](https://docs.docker.com/storage/bind-mounts/#start-a-container-with-a-bind-mount)

Save docker image in docker hub to use it in kubernetes cluster

```text
docker login
docker tag products:1.2.0 dennisseidel/products:1.2.0
docker push dennisseidel/products:1.2.0
```

and add it to the deloyment config

create the secret with

```text
kubectl create secret generic gcloud-cred --from-file=/Users/den/.config/keys/marketplaceapp.json
```

### Service Discovery

Use Envoy on ECS: [https://blog.turbinelabs.io/replacing-aws-application-load-balancers-with-envoy-2a25c74bde9a](https://blog.turbinelabs.io/replacing-aws-application-load-balancers-with-envoy-2a25c74bde9a)

### Register your DOMAIN

[https://console.aws.amazon.com/route53](https://console.aws.amazon.com/route53)

## Encryption - how to use the public cloud securly? N26?

Other Serverless Assets:

* File based Maleware detection : [https://medium.com/airbnb-engineering/binaryalert-real-time-serverless-malware-detection-ca44370c1b90](https://medium.com/airbnb-engineering/binaryalert-real-time-serverless-malware-detection-ca44370c1b90)

Containers on AWS:

* [https://docs.aws.amazon.com/de\_de/AmazonECS/latest/developerguide/ECS\_CLI\_tutorial.html](https://docs.aws.amazon.com/de_de/AmazonECS/latest/developerguide/ECS_CLI_tutorial.html)
* [https://docs.aws.amazon.com/AmazonECS/latest/developerguide/cmd-ecs-cli-compose.html](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/cmd-ecs-cli-compose.html)
* [https://blog.valiantys.com/en/expert-tips/deploying-docker-containers-aws](https://blog.valiantys.com/en/expert-tips/deploying-docker-containers-aws)

