
# 🚀 Production ELK Stack on AKS

[![terraform](https://img.shields.io/badge/Terraform-Production-blue)](https://www.terraform.io/)
[![eck](https://img.shields.io/badge/ECK-2.16.0-green)](https://www.elastic.co/guide/en/cloud-on-k8s/current/)
[![aks](https://img.shields.io/badge/AKS-Private_VNet-orange)](https://azure.microsoft.com/services/kubernetes-service/)

**Scalable, secure logging infrastructure** for enterprise AKS deployments using Elastic Cloud on Kubernetes (ECK), Azure Key Vault CSI secrets, and cost-optimized B-series nodes.


This repository contains Terraform modules, Helm charts, and Kubernetes manifests that automate the deployment of a production-ready ELK Stack (Elasticsearch, Logstash, Kibana) on Azure Kubernetes Service (AKS).

Designed for DevOps and SRE teams building centralized logging pipelines across multi-region AKS clusters, featuring:
- Private VNet integration with Azure CNI networking
- ECK Operator (Elastic Cloud on Kubernetes) for managed Elasticsearch
- Azure Key Vault CSI driver for secrets management
- Cost-optimized Standard_B-series node pools
- Ingress-based LoadBalancer consolidation (1 IP)
- Persistent storage with managed-csi-premium disks

Includes production hardening with NetworkPolicies, PodSecurityStandards, observability stack (Prometheus/Grafana), and comprehensive CI/CD pipelines for your enterprise logging infrastructure.


# INSTALL ECK as Helm charts

**STEP1: Add Elastic Helm repo** 
```
helm repo add elastic https://helm.elastic.co 
helm repo update 
```
**STEP2: Install ECK Operator WITH CRDs**

```
kubectl create namespace elastic-system 

helm install eck-operator elastic/eck-operator \
  --namespace elastic-system \
  --set installCRDs=true
  ```
> This is the ONLY correct Helm-based CRD install.

**STEP3: VERIFY CRDs & API REGISTRATION**
```
kubectl get crds | grep elastic
kubectl api-resources | grep -i elastic
```
