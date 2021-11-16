Simulado
Dia 1
Qual comando realiza o download das imagens de componentes do Kubernetes, como o etcd ou API, antes da criação do cluster?
R: kubeadm config images pull

Qual comando inicializa um cluster Kubernetes?
R: kubeadm init

Qual o comando para adicionar um novo node ao cluster Kubernetes?
R: kubeadm join

Para você adicionar um novo node em seu cluster, o comando é executado no node master ou no node a ser adicionado?
R: no novo node

Qual o comando exibe a linha de comando inteira, inclusive com o token e o ca-cert-hash, para adicionar novos nodes ao cluster?
R: sudo kubeadm token create --print-join-command

Qual comando cria um simples pod do Nginx?
R:kubectl run nginx --image nginx

Qual o comando lista os deployment do namespace default?
R:kubectl get deploy

Como eu posso criar um service para um deployment em execução?
R:kubectl expose deployment/nome_do_deployment

Eu posso ter a swap habilitada em meu cluster?
R: Não

Qual o comando utilizado para visualizar os nodes que fazem parte do meu node?
R: kubectl get nodes
