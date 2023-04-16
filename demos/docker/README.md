# Docker and Kubernetes Demo

This demo showcases how to use Spin with Docker and Kubernetes

## Prerequisites

- `spin plugin install -u https://raw.githubusercontent.com/chrismatteson/spin-plugin-k8s/main/k8s.json`
- Install preview version of Docker Desktop with spin support from [here](https://www.docker.com/blog/announcing-dockerwasm-technical-preview-2/)
- Enable containerd with Docker Desktop
- Enable Kubernetes experimental feature
- Install [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl)
- `kubectl config use-context docker-desktop`
- `kubectl apply -f wasm-runtimeclass.yaml`
    
## Talk Track

A local spin up and Fermyon Cloud are not the only places where a Spin app can be deployed. Kubernetes also supports a runtime to deploy spin applications. These use the "scratch" container, which is basically a blank file to provide the smallest possible deployment, no full OS required. Spin can be deployed into any Kubernetes cluster configured with the Spin shim, to allow easy use of Spin with existing infrascture and cloud environments.

To begin, we need to configure the cluster appropriately, refer to the Spin documentation for [Kubernetes](https://developer.fermyon.com/spin/kubernetes). Next install the spin kubernetes plugin. Here you can see we already have it installed.

```
spin plugins list --installed
```

We have already built our spin app here. So the next steps are to build the scratch container with the app and the spin toml file inside of it. The plugin automates this work for us with the scaffold command. This requires a namespace as an input, that can either be a Docker hub username, or the full path to something like the Github Container Registry.

```
spin k8s scaffold <namespace>
```

Then we can build the actual container locally and push it to our registry.

```
spin k8s build
spin k8s push
```

Finally we deploy our container to our Kubernetes cluster. In this instance we are using Docker Desktop with Kubernetes running locally as an experimental feature.

```
spin k8s deploy
http://localhost
```

Docker also supports running spin containers directly.

```
docker run --runtime=io.containerd.spin.v1 --platform=wasi/wasm -p 3000:80 <namespace>/<image>:latest /
http://localhost:3000
```

## Key Takeaways

* Spin can be deployed on Docker Desktop and any Kubernetes cluster with the shim installed

## Clean up
Ctrl-d to exist docker image. To destroy kuberntes deployment run:

```
kubectl delete -f deploy.yaml
```
