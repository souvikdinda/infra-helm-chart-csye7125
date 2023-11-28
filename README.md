# Infra Helm Chart

This Helm chart is designed to simplify the deployment of Kafka enabling kraft on Kubernetes cluster. It uses Bitnami's Kafka Helm chart to set up a highly reliable and available Kafka cluster.

## Prerequisites

Before deploying the Infrastructure Helm Chart, ensure you have the following prerequisites:

- [Helm](https://helm.sh/docs/intro/install/) installed on your local machine.
- A running Kubernetes cluster.
- GKE (Google Kubernetes Engine) cluster for deploying Kafka on GKE.

## Configuration

- The Helm chart provides several configuration options in the `values.yaml` file.
- This Helm chart includes a healthcheck Kafka topic with 3 partitions.

## Consumer Application Deployment

The consumer application, which consumes messages from the Kafka topic and stores them in a PostgreSQL database, is included in this Helm chart. It is deployed as part of the entire infrastructure.

## Database

The PostgreSQL database is deployed using a StatefulSet with persistent storage.

## CI/CD Pipeline with Semantic Release for Helm Charts
 
- A continuous deployment pipeline has been set up in Jenkins to create new releases of the Helm chart.
- This Helm chart leverages semantic versioning and integrates with [Semantic Release](https://semantic-release.gitbook.io/semantic-release/) for automatic versioning and changelog generation. 
 
## Usage
 
Here are the steps to deploy the web application using the Helm chart:
 
1. Clone this repository:
    ```
     git clone
    ```
  - https://github.com/csye7125-fall2023-group07/webapp-helm-chart

Customize the Helm chart values in values.yaml as needed.
 
2. Deploy the Helm chart on your Kubernetes cluster:
    ```
     helm install chart-name .
    ```
 
3.  Verify the deployment
  - To verify that the release was successfully deployed,
    ```
      helm list
    ```
 
4. Uninstall the Chart
    ```
     helm uninstall chart-name .
    ```


Author: Naga Vaishnavi Puppala, Souvik Dinda