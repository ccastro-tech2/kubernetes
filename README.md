kubernetes
Todos os projetos que particei até agora sempre encontramos a infra pronta, VM, cluster, On primesse e a partir apenas instalavamos nossos produtos. Com a possibilidade de eu ter que criar esses Cluster e agindo de forma preventiva comecei a pesquisar e tentar entender como fazer esta tipo de demanda.

O resultado final foi a criação de um cluster com 3 instancias na aws em 20 minutos de laboratório.

Vamos lá!

Anotações e comentarios!

Kubernetes composto por um Máquina master e outras denominadas como worker Por boas práticas a Master apenas apenas fará a gestão dos outras máquinas denominadas worker´s.

Analogia: Master - gerencia worker - carrega o piano

#Informações

kubeAPI unico que escreve no worker kube scheduler criar novo container (criar pod) kube scheduler agente que esta em todos os nós inclusiveno worker kube proxy porteiro sabe onde esta rodando tudo... expoe serviço

O pod? menor unidade do kubernets

diferença entre pod e container namespace divide o mesmo ip, posso ter varios conteiners dentro do POD

PreReq - AWS

VAMOS INICIAR CRIANDO 3 Instancias NA AWS... 2 VCPUS - aws medium size - 2GB de RAM porta http 8080 abertas vou prevenir de não trocar os ips e vou fixar os ips ultilizando elastic IPS Todos os comandos devem ser repetidos no workers e Master, até o momento de tokens. Nesta parte apenas será executado o comando de master para worker.

################# COMANOS DE INSTALAÇÃO #########################################

1º passo, instalar o docker em todas as máquinas

executar o comando abaixo em todas as máquinas curl -fsSL https://get.docker.com | bash

Valide a instalação do Docker com os comandos abaixo:

docker container ls ou apenas com docker info,

2º - Como boas práticas do kubernetes vamos mudar o grupo de inicialização do docker

crie um arquivo na rota /etc/docker/daemon.json vim /etc/docker/daemon.json

{ "exec-opts": ["native.cgroupdriver=systemd"], "log-driver": "json-file", "log-opts": { "max-size": "100m" }, "storage-driver": "overlay2" }

Nos workers execute O comando EOF vai permitir que escreva linhas de códigos até que apareça outro EOF para finalizar o comando.

vim > /etc/docker/daemon.json <<EOF { "exec-opts": ["native.cgroupdriver=systemd"], "log-driver": "json-file", "log-opts": { "max-size": "100m" }, "storage-driver": "overlay2" } EOF

3º - criando diretorio system.d

mkdir -p /etc/systemd/system/docker.service.d

4º Recarregar o systemctl

systemctl daemon-reload systemctl restart docker

validar cgroup alterado docker info | grep -i cgroup

Para travar a uma versão especifica do docker utilize o seguinte comando: export VERSION=<versão do docker> && curl -fsSL https://get.docker.com | bash

.....adição dos repositórios do k8s e efetuar a instalação do kubeadm <<<<<<<<<<<<<<<<<<<<<<<<

sudo apt-get update && sudo apt-get install -y apt-transport-https gnupg2

curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

sudo echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update

sudo apt-get install -y kubelet kubeadm kubectl

>>>>>>>>>>>>>>>>>> Inicialização do cluster <<<<<<<<<<<<<<<<<<<<<<<<<<

download das imagens ultilizadas pelo sistemas kubernets

sudo kubeadm config images pull

Execute o comando a seguir também apenas no nó master para a inicialização do cluster.

sudo kubeadm init

A saída do comando

[WARNING SystemVerification]: docker version is greater than the most recently validated version. Docker version: 18.05.0-ce. Max validated version: 17.03 ... To start using your cluster, you need to run the following as a regular user:

mkdir -p $HOME/.kube sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config sudo chown $(id -u):$(id -g) $HOME/.kube/config ... kubeadm join --token 39c341.a3bc3c4dd49758d5 IP_DO_MASTER:6443 --discovery-token-ca-cert-hash sha256:37092 ...

Configuração do arquivo do kubectl

mkdir -p $HOME/.kube cp -i /etc/kubernetes/admin.conf $HOME/.kube/config sudo chown $(id -u):$(id -g) $HOME/.kube/config

Instalação do pod network O orquestrador

**carregando módulos do Kernel ** sudo modprobe br_netfilter ip_vs_rr ip_vs_wrr ip_vs_sh nf_conntrack_ipv4 ip_vs

Instalando Weave-net

kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"

pod network foi criado com sucesso, execute o seguinte comando.

kubectl get pods -n kube-system

exemplo de saida: NAME READY STATUS RESTARTS AGE coredns-66bff467f8-pfm2c 1/1 Running 0 8d coredns-66bff467f8-s8pk4 1/1 Running 0 8d etcd-docker-01 1/1 Running 0 8d kube-apiserver-docker-01 1/1 Running 0 8d kube-controller-manager-docker-01 1/1 Running 0 8d kube-proxy-mdcgf 1/1 Running 0 8d kube-proxy-q9cvf 1/1 Running 0 8d kube-proxy-vf8mq 1/1 Running 0 8d kube-scheduler-docker-01 1/1 Running 0 8d weave-net-7dhpf 2/2 Running 0 8d weave-net-fvttp 2/2 Running 0 8d weave-net-xl7km 2/2 Running 0 8d

Inserindo os nós workers no cluster

Para inserir os nós workers no cluster, basta executar a linha que começa com kubeadm join fornecida na saida do comando sudo kubeadm init executada no master

saida: kubeadm join --token 39c341.a3bc3c4dd49758d5 IP_DO_MASTER:6443 --discovery-token-ca-cert-hash sha256:37092

Copie a saida e cole nos worke's

com o comando kubectl get pods, vera que terá duas novas instacias vinculadas ao seu master.

NAME STATUS ROLES AGE VERSION ip-172-31-81-144 Ready control-plane,master 20m v1.22.3 ip-172-31-86-242 Ready 12m v1.22.3 ip-172-31-86-46 Ready 3m v1.22.3

About
No description, website, or topics provided.
Topics
Resources
 Readme
Releases
No releases published
Create a new release
Packages
No packages published
Publish your first package
© 2021 GitHub, Inc.
Terms
Privacy
Security
Status
Docs
Contact GitHub
Pricing
API
Training
Blog
About
