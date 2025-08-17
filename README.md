# basic-argoCD-acm-demo

This example show how to integrate RedHat Openshift Gitops with Advanced Cluster Management(ACM).

### Pre-Reqs:

1. Running Openshift cluster, and oc cli.
2. Install ODF, ACM, and Gitops Operators.
_Note: ODF is optional, one of the app=busybox is using cbd storageclass. You can switch to any other compatible storage class in teh yaml file._

### Create Gitops-ACM integration, and necessary RBACs

```
oc create -f gitops-acm-integration.yaml
oc create -f gitops-rbac.yaml
```

### To create application using ApplicationSet from CLI. This should create parksmap, and busybox applications in the default "local-cluster", when using ACM. They each will be deployed in their own project "busybox", and "parksmap"
```
oc create -f appset/demo-appset.yaml
```

### To create full stack application with frontend, backend, and a mariadb database in an ACM clusterset = "managedset" 
This should create three components, quotesweb(frontend), quotd-python(backend), quotessql(mariadb) all in the "mariadb-{{cluster}}" namespace.

```
oc create if appset/mariadb-appset.yaml
```
You can refer to below git repos for source code, and sql scripts to polulate database.
https://github.com/bharathi-tenneti/qotd-python
https://github.com/bharathi-tenneti/quotemysql
https://github.com/bharathi-tenneti/quotesweb


