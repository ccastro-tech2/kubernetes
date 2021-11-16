Por default master não recebe containers, porém isso pode ser parametrizado para que o master os receba

kubectl describe nodes ip-172-31-81-38

Describe do node do worker **ip-172-31-81-38**

root@ip-172-31-85-102:/home/ubuntu# kubectl describe nodes ip-172-31-81-38
Name:               ip-172-31-81-38
Roles:              <none>
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=ip-172-31-81-38
                    kubernetes.io/os=linux
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: /var/run/dockershim.sock
                    node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Mon, 15 Nov 2021 15:18:17 +0000
Taints:             <none>
Unschedulable:      false
Lease:
  HolderIdentity:  ip-172-31-81-38
  AcquireTime:     <unset>
  RenewTime:       Mon, 15 Nov 2021 15:30:42 +0000
Conditions:
  Type                 Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----                 ------  -----------------                 ------------------                ------                       -------
  NetworkUnavailable   False   Mon, 15 Nov 2021 15:18:26 +0000   Mon, 15 Nov 2021 15:18:26 +0000   WeaveIsUp                    Weave pod has set this
  MemoryPressure       False   Mon, 15 Nov 2021 15:28:49 +0000   Mon, 15 Nov 2021 15:18:17 +0000   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure         False   Mon, 15 Nov 2021 15:28:49 +0000   Mon, 15 Nov 2021 15:18:17 +0000   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure          False   Mon, 15 Nov 2021 15:28:49 +0000   Mon, 15 Nov 2021 15:18:17 +0000   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready                True    Mon, 15 Nov 2021 15:28:49 +0000   Mon, 15 Nov 2021 15:18:27 +0000   KubeletReady                 kubelet is posting ready status. AppArmor enabled
Addresses:
  InternalIP:  172.31.81.38
  Hostname:    ip-172-31-81-38
Capacity:
  cpu:                2
  ephemeral-storage:  8065444Ki
  hugepages-2Mi:      0
  memory:             4028152Ki
  pods:               110
Allocatable:
  cpu:                2
  ephemeral-storage:  7433113179
  hugepages-2Mi:      0
  memory:             3925752Ki
  pods:               110
System Info:
  Machine ID:                 78de3edeb75e4020887bffdfb0d0b243
  System UUID:                ec239a9a-e265-b92a-af21-80819afd0aa3
  Boot ID:                    76121c64-d803-4078-b146-1911e15417f8
  Kernel Version:             5.4.0-1058-aws
  OS Image:                   Ubuntu 18.04.6 LTS
  Operating System:           linux
  Architecture:               amd64
  Container Runtime Version:  docker://20.10.10
  Kubelet Version:            v1.22.3
  Kube-Proxy Version:         v1.22.3
Non-terminated Pods:          (2 in total)
  Namespace                   Name                CPU Requests  CPU Limits  Memory Requests  Memory Limits  Age
  ---------                   ----                ------------  ----------  ---------------  -------------  ---
  kube-system                 kube-proxy-prfsx    0 (0%)        0 (0%)      0 (0%)           0 (0%)         12m
  kube-system                 weave-net-vvvd7     100m (5%)     0 (0%)      200Mi (5%)       0 (0%)         12m
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests    Limits
  --------           --------    ------
  cpu                100m (5%)   0 (0%)
  memory             200Mi (5%)  0 (0%)
  ephemeral-storage  0 (0%)      0 (0%)
  hugepages-2Mi      0 (0%)      0 (0%)
Events:
  Type    Reason                   Age                From        Message
  ----    ------                   ----               ----        -------
  Normal  Starting                 12m                kube-proxy
  Normal  Starting                 12m                kubelet     Starting kubelet.
  Normal  NodeHasSufficientMemory  12m (x2 over 12m)  kubelet     Node ip-172-31-81-38 status is now: NodeHasSufficientMemory
  Normal  NodeHasNoDiskPressure    12m (x2 over 12m)  kubelet     Node ip-172-31-81-38 status is now: NodeHasNoDiskPressure
  Normal  NodeHasSufficientPID     12m (x2 over 12m)  kubelet     Node ip-172-31-81-38 status is now: NodeHasSufficientPID
  Normal  NodeAllocatableEnforced  12m                kubelet     Updated Node Allocatable limit across pods
  Normal  NodeReady                12m                kubelet     Node ip-172-31-81-38 status is now: NodeReady
  
  **Recuperar Token**
Adicionar novos nodes ao seu cluster
kubeadm token create --print-join-command
  
comandos com auto complete
**apt-get install -y bash-completion**  
kubectl completion bash > /etc/bash_completion.d/kubectl
source <(kubectl completion bash)  
  
kubeadm join 172.31.85.102:6443 --token lm1a0n.4f77rrrsu9e81055 --discovery-token-ca-cert-hash sha256:d712cf4bd8c42237d5929fc28fb9b11cbe0902c94f754b40a354e461a0192770
                 
POD é a menos unidade e eu posso ter varios containers dentro desse pod, compartilhando recursos.
                 
todos os namespaces 
kubectl get pods --all-namespaces
root@ip-172-31-85-102:/home/ubuntu# kubectl get pods --all-namespaces
NAMESPACE     NAME                                       READY   STATUS    RESTARTS      AGE
kube-system   coredns-78fcd69978-h7bw2                   1/1     Running   0             34m
kube-system   coredns-78fcd69978-w4mx6                   1/1     Running   0             34m
kube-system   etcd-ip-172-31-85-102                      1/1     Running   0             34m
kube-system   kube-apiserver-ip-172-31-85-102            1/1     Running   0             34m
kube-system   kube-controller-manager-ip-172-31-85-102   1/1     Running   0             34m
kube-system   kube-proxy-prfsx                           1/1     Running   0             32m
kube-system   kube-proxy-vkhwd                           1/1     Running   0             34m
kube-system   kube-proxy-z7p24                           1/1     Running   0             32m
kube-system   kube-scheduler-ip-172-31-85-102            1/1     Running   0             34m
kube-system   weave-net-4l8vn                            2/2     Running   0             32m
kube-system   weave-net-bmz7w                            2/2     Running   1 (33m ago)   33m
kube-system   weave-net-vvvd7                            2/2     Running   0             32m

                 
                 
kubectl get namespaces
NAME              STATUS   AGE
default           Active   36m
kube-node-lease   Active   36m
kube-public       Active   36m
kube-system       Active   36m
                 
                 
                 
