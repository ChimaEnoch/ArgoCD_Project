# Project: Wep App over HTTPS

This repository contains the files used to deploy an Nginx web server to minikube and access it over HTTPS using TLS termination at the ingress level with cert-manager. The CD tool used is ArgoCD.


## Requirements:

Create the following environment:

Deploy any web application that can be accessed with HTTPS from the browser. The web app should be accessible from outside the cluster with TLS termination (at the Ingress level using Cert Manager) using this domain: app-127-0-0-1.nip.io

Using ArgoCD, the following files are declarative:

- cert manager (https://github.com/cert-manager/cert-manager/releases/download/v1.10.1/cert-manager.yaml)
- secret
- nginx deployment
- service
- ingress

I created a self-signed certificate using openssl and the following entry in the /etc/hosts file: 192.168.49.2    app-127-0-0-1.nip.io

Note: 192.168.49.2 is the minikube ip


## Accessing the Web App
To access the web app, open a browser and go to https://app-127-0-0-1.nip.io. The TLS termination at the ingress level using cert-manager automatically secure the connection and allow you to access the web app over HTTPS.