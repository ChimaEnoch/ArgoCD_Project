# Wep App over HTTPS with ArgoCD

This repository contains the files used to deploy an Nginx web server to minikube and access it over HTTPS using TLS termination at the ingress level with cert-manager. The CD tool used is ArgoCD.


## Requirements:

Create the following environment:

Deploy any web application that can be accessed with HTTPS from the browser. The web app should be accessible from outside the cluster with TLS termination (at the Ingress level using Cert Manager) using this domain: app-127-0-0-1.nip.io

Using ArgoCD, the following deployment files are declarative yaml files:

- cert manager (https://github.com/cert-manager/cert-manager/releases/download/v1.10.1/cert-manager.yaml)
- secret
- nginx deployment
- service
- ingress



I created a self-signed certificate using openssl, which is managed by the cert-manager. 

The following entry was added in the /etc/hosts file: 192.168.49.2    app-127-0-0-1.nip.io
Note: 192.168.49.2 is the minikube ip

The argoCD was configured with source repo URL: https://github.com/ChimaEnoch/ArgoCD_Project.git and track files in the path app_files.

The folder (path) app_files contains the manifest files for the resources to be deployed.

## Accessing the Web App
To access the web app, open a browser and go to https://app-127-0-0-1.nip.io. The TLS termination at the ingress level using cert-manager automatically secure the connection and allow you to access the web app over HTTPS.


![nip io](https://user-images.githubusercontent.com/113892424/215744167-19f2aa17-80fc-4c1f-a872-2e97dd069e9b.PNG)

----------------------------------------------------------------------------------------------------------------------------

# Create a section on the README answering the following questions.

## Questions:
a.) Describe your approach to setup a CD solution for a Kubernetes environment, where there is a need to serve five teams of developers that can’thave direct kubectl access to the cluster and maintain their autonomy to deploy and see the production environment for debugging purposes.
b.) How would you manage secrets inside? What tooling would you use?
c.) Describe your approach for deploying and managing “Addons” applications that enable, automate or facilitate setups on Kubernetes.

## Answers:
a.) 
- I would create a separate namespace for each team of developers.
- Using role-based access control (RBAC) to grant each team access to their own namespace.
- Each team would push their code to a version control repository and the CD tool automatically deploy resoucres and applications to the appropriate namespace in the Kubernetes cluster. 
- To see the production environment for debugging purposes, monitoring tools would be configured for each team to provide visbility to their application and health metrics.



i.) To manage secrets inside the cluster, kubernetes-external-secrets (https://github.com/external-secrets/kubernetes-external-secrets) can be used. It allows the secrets to be stored externally and inject them into the cluster when required, this eliminates the need to store secrets directly in the manifest files. 
ii) 
- Argocd for CD deployment
- Git for version control
- GitHub for storing codes remotely and collaboration
- kubernetes-external-secrets for secret management 

b.) 
- Addons could be sidecar containers (for logging etc), certificate management tool, ingress controller etc and create a namespace specific to the addon for efficient resource management. A CD setup like argoCD could be used to facilitate setups on Kubernetes.




