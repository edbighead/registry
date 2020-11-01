![Lint Charts](https://github.com/edbighead/registry/workflows/Lint%20Charts/badge.svg?branch=main)
# Docker Registry Chart

## Usage
`helm upgrade --install --wait registry charts/registry`

## Description
Docker registry chart with following features:
* NGINX Ingress Controller with [automated certificate management](https://kubernetes.github.io/ingress-nginx/user-guide/tls/#automated-certificate-management-with-kube-lego) running on `https://registry.local`
* Basic authentication with following credentials `user:password`
* Possibility to run `n` replicas for redundancy
* [Garbage collection](https://docs.docker.com/registry/garbage-collection/) running as a [Kubernetes CronJob](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/)
* [Redis chart](https://github.com/bitnami/charts/tree/master/bitnami/redis) used for [blobdescriptor cache](https://docs.docker.com/registry/configuration/#cache)
* A local [Persistent Volume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) mounted on `/var/lib/registry`
* [S3 Storage Driver](https://docs.docker.com/registry/storage-drivers/s3/) configured with the following values:

|         Parameter        |      Description      |       Value      |
|:------------------------:|:---------------------:|:----------------:|
| `storage.type`           | storage type to use   | s3               |
| `storage.s3.s3AccessKey` | AWS_ACCESS_KEY_ID     | xxx              |
| `storage.s3.s3SecretKey` | AWS_SECRET_ACCESS_KEY | xxx              |
| `storage.s3.region`      | bucket region         | us-east-1        |
| `storage.s3.bucketName`  | bucket name           | your-bucket-name |

## Note
This is not a production ready chart and was made for demo purposes only.

Values are hardcoded in `values.yaml` file for demo purpose only. Please encrypt your secret values. For example, tools like [mozilla/sops](https://github.com/mozilla/sops) can be used.


## Demo
[![asciicast](https://asciinema.org/a/369570.svg)](https://asciinema.org/a/369570)

Recorded on `minikube` cluster
```
kubectl version
Client Version: version.Info{Major:"1", Minor:"19", GitVersion:"v1.19.3", GitCommit:"1e11e4a2108024935ecfcb2912226cedeafd99df", GitTreeState:"clean", BuildDate:"2020-10-14T12:50:19Z", GoVersion:"go1.15.2", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"19", GitVersion:"v1.19.2", GitCommit:"f5743093fd1c663cb0cbc89748f730662345d44d", GitTreeState:"clean", BuildDate:"2020-09-16T13:32:58Z", GoVersion:"go1.15", Compiler:"gc", Platform:"linux/amd64"}
```

## Issues
Issues encountered during chart development were recorded in [issues.md](issues.md)