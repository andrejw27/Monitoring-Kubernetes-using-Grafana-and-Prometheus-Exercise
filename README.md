# Monitoring-Kubernetes-using-Grafana-and-Prometheus-Exercise

This is an attempt of monitoring a server, managed by Kubernetes, using Grafana and Prometheus.

## Introduction
* Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available. [Kubernetes](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/)
* Prometheus is a software used for event monitoring and alerting. It records real-time metric in a time-series database. [Prometheus](https://en.wikipedia.org/wiki/Prometheus_(software))
* Grafana is a multi-platform open source analytics and interactive visualization web application. It provides charts, graphs, and alerts for the web when connected to supported data sources. [Grafana](https://en.wikipedia.org/wiki/Grafana)

## Prerequisites
* In order to see how Grafana and Prometheus work, first run a Kubernetes cluster. In this attempt, I will be using Minikube which runs a single-node Kubernetes cluster. The installation guide can be seen [here](https://kubernetes.io/docs/tasks/tools/install-minikube/). In my case, I use [Chocolatey](https://chocolatey.org/) to install minikube.
  ```
  $ choco install minikube
  ```
* The Kubernetes command-line tool, kubectl, allows to run commands against Kubernetes clusters. kubectl is used to deploy applications, inspect and manage cluster resources, and view logs. Install it using Chocolatey.
  ```
  $ choco install kubernetes-cli
  ```
* Helm is a package manager for Kubernetes, which is used to install Prometheus and Grafana. Use Chocolatey to install helm.
  ```
  $ choco install kubernetes-helm
  ```
 
 Once all the requirements are set, it is time to move into the next step.
 
## Install Prometheus

* It is recommended to install Prometheus in a separate namespace to be easier to manage. Create a namespace called monitor:

  ```
  $ kubectl create ns monitor
  ```
* Then, install Prometheus using helm.
  ```
  $ helm install prometheus-operator stable/prometheus-operator --namespace monitor
  ```
* Verify the Prometheus installation.
  ```
  $ kubectl get pods -n monitor
  ```
  ![](Images/verify_prometheus.PNG)
* Now that the pods are running, we have the option to use the Prometheus dashboard right from our local machine. This is done by using the following command:
  ```
  $ kubectl port-forward -n monitor prometheus-prometheus-operator-prometheus-0 9090
  ```
  ![](Images/post_forward_prom.PNG)
