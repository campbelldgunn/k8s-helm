# Helm Client

### Container Details
[![](https://images.microbadger.com/badges/image/gunnertime/k8s-helm.svg)](http://microbadger.com/images/gunnertime/k8s-helm "Get your own image badge on microbadger.com")
[![](https://images.microbadger.com/badges/version/gunnertime/k8s-helm.svg)](http://microbadger.com/images/gunnertime/k8s-helm "Get your own version badge on microbadger.com")
[![](https://images.microbadger.com/badges/commit/gunnertime/k8s-helm.svg)](http://microbadger.com/images/gunnertime/k8s-helm "Get your own commit badge on microbadger.com")

# Supported tags and respective `Dockerfile` links
* `v2.6.1`, `latest`    [(v2.6.1/Dockerfile)](https://github.com/campbelldgunn/k8s-helm/blob/v2.6.1/Dockerfile)

## Overview
This container provides the Helm client for use with Kubernetes

## Run with tunneling
`kubectl run -it helm --env=HELM_HOST=<HOST>:<PORT> --image=gunnertime/k8s-helm --command /bin/sh -n kube-system --rm=true`

## Run without tunneling
`kubectl run -it helm --image=gunnertime/k8s-helm --command /bin/sh -n kube-system --rm=true`
