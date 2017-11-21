# Helm Client

### Container Details
[![](https://images.microbadger.com/badges/image/campbelldgunn/k8s-helm.svg)](http://microbadger.com/images/campbelldgunn/k8s-helm "Get your own image badge on microbadger.com")
[![](https://images.microbadger.com/badges/version/campbelldgunn/k8s-helm.svg)](http://microbadger.com/images/campbelldgunn/k8s-helm "Get your own version badge on microbadger.com")
[![](https://images.microbadger.com/badges/commit/campbelldgunn/k8s-helm.svg)](http://microbadger.com/images/campbelldgunn/k8s-helm "Get your own commit badge on microbadger.com")


# Supported tags and respective `Dockerfile` links
* `v2.7.7`, `latest`    [(v2.7.2/Dockerfile)](https://github.com/campbelldgunn/k8s-helm/blob/v2.7.2/Dockerfile)

## Overview
This container provides the Helm client for use with Kubernetes

## Run with tunneling
`kubectl run -it helm --env=HELM_HOST=<HOST>:<PORT> --image=campbelldgunn/k8s-helm --command /bin/sh -n kube-system --rm=true`

## Run without tunneling
`kubectl run -it helm --image=campbelldgunn/k8s-helm --command /bin/sh -n kube-system --rm=true`
