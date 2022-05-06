DevOps Commands
============

___

A list of my favorite commands :)

### K8s

| Command                                                                                                                                        | Description                                                                                                                           |
|------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| `sudo containerd config default > /etc/containerd/config`                                                                                      | Generate containerd default config                                                                                                    |
| `sudo crictl —runtime-endpoint unix:///run/containerd/containerd.sock ps -a`                                                                   | List Linux runtime containers                                                                                                         |
| `sudo crictl —runtime-endpoint unix:///run/containerd/containerd.sock logs -f ff8313`                                                          | Check container logs by container id                                                                                                  |
| `kubeadm init --pod-network-cidr=<net_cidr> --control-plane-endpoint=<shared-ep> --apiserver-advertise-address=<ip-address> —secure-port=6443` | Init K8s cluster on control plane node ( with net-cidr and shared endpoint ( Load balancer ) in case of HA cp )                       |
| `kubectl create -f https://git-io/weave-kube`                                                                                                  | Apply network plugin ( e.g. calico, weave-kube, Cisco ACI )                                                                           |
| `kubeadm join`                                                                                                                                 | Join worker nodes                                                                                                                     |
| `kubectl upgrade plan`                                                                                                                         | Cluster upgrade operation                                                                                                             |
| `kubectl upgrade apply`                                                                                                                        |                                                                                                                                       |
| `kubectl upgrade diff`                                                                                                                         | Equivalent to apply --dry-run                                                                                                         |
| `kubectl upgrade node`                                                                                                                         | Upgrade other cp nodes and the kubelet config on workers                                                                              |
| `kubectl config view --minify`                                                                                                                 | Verify kubectl configuration                                                                                                          |
| `kubectl config use-context <context_name>`                                                                                                    | Switch kubectl context                                                                                                                |
| `kubectl config set-context --current --namespace=<namespace>`                                                                                 | Set namespace permanently for current context                                                                                         |
| `kubectl api-resources --namespaced=true`                                                                                                      | List resources in a namespace                                                                                                         |
| `kubectl get namespace`                                                                                                                        | List namespaces                                                                                                                       |
| `kubectl run nginx --image=nginx:1.10.0`                                                                                                       | Create Nginx deployment                                                                                                               |
| `kubectl run nginx --image=nginx:1.10.0 --namespace=<namespace>`                                                                               | Create Nginx deployment in specific namespace                                                                                         |
| `kubectl expose deployments nginx --port 80 --type LoadBalancer`                                                                               | Expose Nginx deployment                                                                                                               |
| `kubectl port-forward nginx 10080:80`                                                                                                          | Setup port-forwarding                                                                                                                 |
| `kubectl apply -f <filename>.yaml --record`                                                                                                    | Declarative configuration Deployment                                                                                                  |
| `kubectl create -f <filename>.yaml`                                                                                                            | Create the object defined in yaml file                                                                                                |
| `kubectl replace -f <filename>.yaml`                                                                                                           | Replace the object defined in yaml file ( this action overwrite the live config )                                                     |
| `kubectl delete -f <filename1>.yaml -f <filename2>.yaml`                                                                                       | Delete the object defined in two config files                                                                                         |
| `kubectl diff -R -f <dir_name>`                                                                                                                | Recursively verify diffs between live config and config files in dir_name                                                             |
| `kubectl apply -R -f <dir_name>`                                                                                                               | Recursively create or patch all the objects in dir_name                                                                               |
| `kubectl diff -R -f <dir_name>`                                                                                                                | Recursively verify diffs between live config and config files in dir_name                                                             |
| `kubectl diff -R -f <dir_name>`                                                                                                                | Recursively verify diffs between live config and config files in dir_name                                                             |
| `kubectl get pods`                                                                                                                             | Verify pods in the default namespace                                                                                                  |
| `kubectl describe pods nginx`                                                                                                                  | Verify nginx pod in the default namespace                                                                                             |
| `kubectl get services`                                                                                                                         | Verify services in the default namespace                                                                                              |
| `kubectl logs -f pod_name`                                                                                                                     | Get pod logs                                                                                                                          |
| `kubectl exec pod_name --stdin --tty -c pod_name /bin/sh`                                                                                      | Run interactive Shell inside pod                                                                                                      |
| `kubectl get events -A --field-selector=reason=OwnerRefInvalidNamespace`                                                                       | List warnings about invalid cross-namespace ownerReference, or a cluster-scoped dependent with an ownerReference to a namespaced kind |
| `kubectl get pods -l 'environment in (qa,prod),tier in (fe)'`                                                                                  | Select pods based on label selectors environment/tier                                                                                 |
| `kubectl get pods --field-selector=status.phase!=Running,spec.restartPolicy=Always`                                                            | Select restarting pods based on field selectors                                                                                       |
| `kubectl get statefulsets,services --all-namespaces --field-selector metadata.namespace!=default`                                              | Select statefulsets and services on all non-default namespaces                                                                        |
| `kubectl cordon <node_name> `                                                                                                                  | Mark a node object unscheduled, usually used before maintenance tasks.                                                                |
| `kubectl describe node <node_name>`                                                                                                            | Check node informations ( e.g. addresses, conditions, capacity )                                                                      |


### Docker

| Command                                                                                                                                                                                                                         | Description                                                            |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------|
| `docker-compose up -d --build`                                                                                                                                                                                                  | Build and run container from a compose file                            |
| `docker swarm init --auto-lock`                                                                                                                                                                                                 | Init a cluster of nodes                                                |
| `docker swarm leave -f`                                                                                                                                                                                                         | Force a node to leave a swarm                                          |
| `docker service create --name --replicas <replicas_count> --publish 80:80 --rollback-failure-action=<continue/pause> --update-failure-action rollback --update-max-failure-ratio 0.1 --update-monitor-period 10s <image_name> ` | Deploy a replicated service                                            |
| `docker stack deploy -c compose-file.yml < stack_name >`                                                                                                                                                                        | Deploy a stack of services using a compose file                        |
| `docker service ls`                                                                                                                                                                                                             | Get Swarm services                                                     |
| `docker service logs --tail <service_name>`                                                                                                                                                                                     | Get service logs                                                       |
| `docker secret create my-password <password.file>`                                                                                                                                                                              | Create a secret                                                        |
| `docker service update --secret-add=<sec-name> <service_name>`                                                                                                                                                                  | Update the service to use the created secret                           |
| `docker service --update-failure-action=<action>`                                                                                                                                                                               | Automatic rollback action has 3 values ( rollback, continue or pause ) |
| `curl -X GET https://myregistry:5000/v2/_catalog`                                                                                                                                                                               | List all repositories in a Docker registry                             |
| `curl -X GET https://myregistry:5000/v2/<repo_name>/tags/list`                                                                                                                                                                  | List tags of a repository                                              |


### Cloud

| Command                                                                                   | Description                                                 |
|-------------------------------------------------------------------------------------------|-------------------------------------------------------------|
| `cf create <myapp>`                                                                       | CloudFoundry platform operations                            |
| `cf push <myapp>`                                                                         |                                                             |
| `cf create-service <myservice>`                                                           |                                                             |
| `cf start <myapp>`                                                                        |                                                             |
| `cf scale <myapp> -i <desired_instance_number>`                                           |                                                             |
| `gcloud container clusters create <cluster_name>`                                         | GC K8s Cluster operations                                   |
| `gcloud container clusters list`                                                          |                                                             |
| `gcloud get nodes`                                                                        |                                                             |
| `gcloud container clusters delete <cluster_name>`                                         |                                                             |
| `aws configure`                                                                           | Configure AWS CLI ( e.g. IAM, region, format )              |
| `aws ec2 describe-instances --output json --query 'Reservation[].Instances[].InstanceId'` | List EC2 instance ids ( support text/table output formats ) |


### Linux

| Command                               | Description                                                    |
|---------------------------------------|----------------------------------------------------------------|
| `jobs -l`                             | Check background jobs                                          |
| `rpm -qf <file_path>`                 | Check which rpm package has created a file                     |
| `du -sh <folder_path>`                | Check folder size                                              |
| `fdisk <device_name>`                 | Check partition and partition table                            |
| `lsblk`                               | Check partition and partition table                            |
| `cat /proc/meminfo`                   | Check informations about memory                                |
| `vmstat`                              | Check informations about memory                                |
| `renice <desirable_nice_value> <pid>` | Set process priority ( -20 is highest and 19 is lowest value ) |
| `pstree`                              | Check processes as tree                                        |
| `w`                                   | Check average load                                             |
| `top`                                 | Check processes                                                |
| `ss -a -t`                            | Check TCP socket information                                   |
| `ss -a -u`                            | Check UDP socket information                                   |


### Networking

| Command                                                        | Description                                                   |
|----------------------------------------------------------------|---------------------------------------------------------------|
| `configure terminal`                                           | Enter global configuration mode                               |
| `restconf`                                                     | Enable RestConf                                               |
| `show interface Gi0/0`                                         | Verify duplex and speed settings configured for a switch port |
| `show ip interface brief`                                      | Verify interfaces summary                                     |
| `show ip eigrp neighbors`                                      | Verify EIGRP neighbors                                        |
| `ipv6 unicast-routing`                                         | Configure a router as IPv6 router                             |
| `ipv6 route <ipv6-prefix/ipv6-prefix-length> <exit_interface>` | Configure static IPv6 route                                   |
| `ipv6 router eigrp 2`                                          | Configure EIGRP routing process for IPv6                      |
| `eigrp router-id 1.0.0.0`                                      | Configure EIGRP router id                                     |
| `ipv6 eigrp 2`                                                 | Enable EIGRP for IPv6 on interface                            |
| `redistribute static`                                          | Propagate static default route in EIGRP for IPv6              |
| `ipv6 router ospf 10`                                          | Configure OSPFv3 routing process for IPv6                     |
| `router-id 1.1.1.1`                                            | Assign router id for OSPFv3                                   |
