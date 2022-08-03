## Spark-On-K8s

=========================================================================================

### Pre-Requisites
</br>

Make sure kubectl and helm are installed.

1. Installing spark operator.

</br>

- Create namespaces for operator isc-minerva-swb-dscw-spark-operator and jobs isc-minerva-swb-dscw-spark-jobs. Also, label  both the ns as istio-injection=enabled

```bash
kubectl create ns isc-minerva-swb-dscw-spark-operator isc-minerva-swb-dscw-spark-jobs
```

</br>

```bash
helm install spark-operator spark-operator --namespace isc-minerva-swb-dscw-spark-operator
```

</br>

> The Spark driver pod uses a Kubernetes service account to access the Kubernetes API server to create and watch executor pods.

```bash
kubectl create serviceaccount spark
```
</br>

> To grant a service account a Role or ClusterRole, a RoleBinding or ClusterRoleBinding is needed.

```bash
kubectl create clusterrolebinding spark-role --clusterrole=edit --serviceaccount=default:spark --namespace=default
```

</br>

> Make sure we have spark image with us hosted in ECR.
### Now this can be tested with basic spark job 

</br>

```bash
--master k8s://https://<k8s-apiserver-host>:<k8s-apiserver-port> \
    --deploy-mode cluster \
    --name spark-pi \
    --class org.apache.spark.examples.SparkPi \
    --conf spark.executor.instances=5 \
    --conf spark.kubernetes.container.image=<spark-image> \
   local:///path/to/examples.jar
``` 
