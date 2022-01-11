# gcloud

## Install

- Download zip
- Unzip and move to folder
- Add bin to PATH

### Debian / Ubuntu

````bash
echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] http://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -
sudo apt-get update && sudo apt-get install google-cloud-sdk
````

## Commands

Install kubectl

```
gcloud components install kubectl
```

Authenticate

````
gcloud auth login
````

Authenticate applications

```bash
gcloud auth application-default login
```

Configure docker

```
gcloud auth configure-docker
```

Show current user

````
gcloud auth list
````

Configure basic data

````
gcloud config set compute/zone us-central1-a
gcloud config set compute/region us-central1
gcloud config set project generated-area-284017
````

Show config

````
gcloud config list
````

Create cluster

````
gcloud container clusters create test-cluster --num-nodes 1
````

Resize cluster

````
gcloud container clusters resize test-cluster --num-nodes=0
````

Delete cluster

````
gcloud container clusters delete test-cluster
````

Upgrade cluster

````
gcloud container get-server-config
gcloud container clusters upgrade cluster-name --master --cluster-version cluster-version
````

Create disk

````
gcloud compute disks create --size=500GB --zone=us-central1-a my-data-disk
````

Show resources

````
gcloud compute instances list
gcloud container clusters list
gcloud compute disks list
````

Upload docker image

```
docker tag [SOURCE_IMAGE] [HOSTNAME]/[PROJECT-ID]/[IMAGE]:[TAG]
docker push [HOSTNAME]/[PROJECT-ID]/[IMAGE]:[TAG]
```

List docker iamges

```
gcloud container images list
gcloud container images list --repository eu.gcr.io/generated-area-284017
```

Delete docker image

````
gcloud container images delete <IMAGE_NAME> --force-delete-tags  --quiet
````















