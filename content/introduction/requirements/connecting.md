+++
title = "Connecting GCP"
date = 2018-12-09T16:52:57-05:00
weight = 53
draft = true
+++


* Set env var of Cluster name

```bash
CLUSTER_NAME=k8s-workshop
```

**OPTIONAL if using gcloud console**
* Set up the gcloud sdk

```bash
gcloud init
```


* Set gcloud project env var

```bash
PROJECT_ID=${1:-k8s-workshop};

gcloud config set project ${PROJECT_ID};
gcloud config set compute/region us-east1;
gcloud config set compute/zone us-east1-b;
```

* Check to make sure account can see 

```bash
gcloud container clusters list
```

* Get the cluster credentials 

```bash
gcloud container clusters get-credentials ${CLUSTER_NAME};
```

* Make kubectl can see the cluster

```bash
kubectl cluster-info
```

* Allow docker to push to GCR

```bash
gcloud auth configure-docker

The following settings will be added to your Docker config file
located at [/Users/contino/.docker/config.json]:
 {
  "credHelpers": {
    "gcr.io": "gcloud",
    "us.gcr.io": "gcloud",
    "eu.gcr.io": "gcloud",
    "asia.gcr.io": "gcloud",
    "staging-k8s.gcr.io": "gcloud",
    "marketplace.gcr.io": "gcloud"
  }
}

Do you want to continue (Y/n)?  Y

Docker configuration file updated.
```
 
* Test

```bash
docker pull nginx
docker tag nginx us.gcr.io/${PROJECT_ID}/nginx:your_name
docker push us.gcr.io/${PROJECT_ID}/nginx:your_name
```
