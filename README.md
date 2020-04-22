# K8s-Fluentd
## Introduction

Example deployment files for Fluentd on Kubernetes shipping to [Humio](https://humio.com/)

## Install

You will need to build your own Docker image for Fluentd with the required plugins installed, see the `Dockerfile`.

```shell
$ docker build -t repo/fluentd .
$ docker push repo/fluentd
```

Edit `fluentd-daemon.yaml` to set the image to the one you just built or you can just use mine that's alreay in there.



Edit `fluentd-config-humio.yaml` to insert your own Humio API key and index space. The `user` is set to the index and the `password` is set to the API key. See the [Humio documentation](https://docs.humio.com/integrations/data-shippers/fluentd/)

```shell
$ kubectl create ns logging
$ kubectl apply -f fluentd-rbac.yaml
$ kubectl apply -f fluentd-config-humio.yaml
$ kubectl apply -f fluentd-daemon.yaml
```

That's all there is to it, give it a minute and check Humio to see the logs streaming in.