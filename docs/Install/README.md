# Prerequisites
* Run some docker daemon
    * [Docker desktop](https://www.docker.com/products/docker-desktop/)
    * [Rancher dektop](https://rancherdesktop.io/)
* Install some local cluster
    * tool
        * [minikube](https://minikube.sigs.k8s.io/docs/start/)
        * [kind](https://kind.sigs.k8s.io/)
            * Notes
                * Note1: If you use Rancher or Colina -> Not install via brew, since you need <=v0.19.0 [Reason](https://github.com/kubernetes-sigs/kind/issues/3277)
    * Run a local cluster
        * [minikube]  `minikube start`
        * [kind] `kind create cluster`
            * Problems:
                * Problem1: " error during container init: error mounting "cgroup" to rootfs at "/sys/fs/cgroup": mount cgroup:/sys/fs/cgroup/openrc (via /proc/self/fd/7)"
                    * Attempt1: `kind create cluster --image kindest/node:v1.28.0`
                    * Solution: Install [Go](https://go.dev/doc/install) & `go install sigs.k8s.io/kind@v0.19.0`
* Install tekton pipelines
    * `kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml`
* Gran `cluster-admin` privileges to the user who installed Tekton Pipelines
  * TODO:

# Steps
* Apply the releases
  * Common
    * Latest -- `kubectl apply --filename https://storage.googleapis.com/tekton-releases/triggers/latest/release.yaml`
    * Nightly -- `kubectl apply --filename https://storage.googleapis.com/tekton-releases-nightly/triggers/latest/release.yaml`
    * Specific -- `kubectl apply --filename https://storage.googleapis.com/tekton-releases/triggers/previous/VERSION_NUMBER/release.yaml`
  * Interceptors
    * Latest -- `kubectl apply --filename https://storage.googleapis.com/tekton-releases/triggers/latest/interceptors.yaml`
    * Nightly -- `kubectl apply --filename https://storage.googleapis.com/tekton-releases-nightly/triggers/latest/interceptors.yaml`
    * Specific -- `kubectl apply --filename https://storage.googleapis.com/tekton-releases/triggers/previous/VERSION_NUMBER/interceptors.yaml`
* Check that all is READY == 1/1
  * `kubectl get all -n tekton-pipelines`