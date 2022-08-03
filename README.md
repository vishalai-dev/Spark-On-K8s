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

kubectl label ns isc-minerva-swb-dscw-spark-operator istio-injection=enabled
kubectl label ns isc-minerva-swb-dscw-spark-jobs istio-injection=enabled
```

</br>

```bash
helm install swb-dscw-oss-spark-operator spark-operator/ --namespace isc-minerva-swb-dscw-spark-operator
```
