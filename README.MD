# Cloud Disk Performance

Inspired by [Disk performance on Azure Kubernetes Service (AKS) - Part 1: Benchmarking](http://stian.tech/disk-performance-on-aks-part-1/) by [Stian Øvrevåge](http://stian.tech/about/), the IO performance of Alicloud Container Service is measured and compared. The following configuration was done.

- 20GB, StorageClass alicloud-disk-ssd
- 128GB, StorageClass alicloud-disk-ssd
- 250GB, StorageClass alicloud-disk-ssd
- 20GB, StorageClass alicloud-disk-efficiency
- 20GB, StorageClass NFS

The create the testing environment, you need to create a namespace called disk your ACS env and the apply the yaml.

```
kubectl apply -n disk -f ./ubuntu-statefulset.yaml
```

This will create a statefulset call ```disk-test``` and then you can copy the script into the container

```
kubectl cp -n disk ./script/ disk-test-0:/script
```

Than create a remote shell to the container

```
kubectl exec -it -n disk disk-test-0 -- /bin/bash
```

After that, you need to install fio in the container

```
apt-get update %% apt-get --assume-yes install fio 
```

You can execute the test by

```
cd /script && ./start.sh
```


# Alicloud

[Official Performance Chart](https://www.alibabacloud.com/help/doc-detail/25382.htm?spm=a2c63.p38356.b99.198.418a3a9egGyQpS)

Logs files are taken [alicloud](./alicloud)


# Azure

Logs from Azure are downlaod from Stian Øvrevåge 

# Macbook Pro

A fio logs reference from a 2014 Macbook Pro [macbookpro](./macbookpro)