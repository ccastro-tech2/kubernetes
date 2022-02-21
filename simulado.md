<p class="has-line-data" data-line-start="31" data-line-end="33">ANOTAÇÕES<br>
<p class="has-line-data" data-line-start="31" data-line-end="33">1: Master e Workers <br>
 <p class="has-line-data" data-line-start="31" data-line-end="33">1: ReplicaSet controla os pods <br>
  <p class="has-line-data" data-line-start="31" data-line-end="33">1: Deamonset você não escolha quantas replicas! vantagem???? quando vc precisa que a aplicação sempre up <br>
<p class="has-line-data" data-line-start="31" data-line-end="33">2: componentes services, forma de pegar o deployment precisa do service para o deployment possa ser acessado de fora do cluster<br>
<p class="has-line-data" data-line-start="31" data-line-end="33"> 3 controler do pod? resposta replica Set.<br>
<p class="has-line-data" data-line-start="31" data-line-end="33"> 4: Controler do replica Set Resposta deployment<br>
<p class="has-line-data" data-line-start="31" data-line-end="33"> NameSpace Cotas "limitação" isolar sua aplicação.<br>
<p class="has-line-data" data-line-start="31" data-line-end="33"> Storage volume e Claim  <br>
<p class="has-line-data" data-line-start="31" data-line-end="33"> class="has-line-data" data-line-start="31" data-line-end="33"> CLUSTER IP só acessa dentro do Cluster<br>
<p class="has-line-data" data-line-start="31" data-line-end="33"> Entender esse Role<br>
<p class="has-line-data" data-line-start="31" data-line-end="33"> Service?<br>
<p class="has-line-data" data-line-start="31" data-line-end="33">Resposta: Um serviço no Kubernetes é uma abstração que define um conjunto lógico de Pods e uma política pela qual acessá-los. Serviços permitem um baixo acoplamento entre os Pods      dependentes. Um serviço é definido usando YAML (preferencialmente) ou JSON, como todos objetos Kubernetes.<br>


<h1 class="code-line" data-line-start=0 data-line-end=1 ><a id="Simulado_0"></a>Simulado</h1>
<h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Dia 1</h2>
<p class="has-line-data" data-line-start="4" data-line-end="6">Qual comando realiza o download das imagens de componentes do Kubernetes, como o etcd ou API, antes da criação do cluster?<br>
R: kubeadm config images pull</p>
<p class="has-line-data" data-line-start="7" data-line-end="9">Qual comando inicializa um cluster Kubernetes?<br>
R: kubeadm init</p>
<p class="has-line-data" data-line-start="10" data-line-end="12">Qual o comando para adicionar um novo node ao cluster Kubernetes?<br>
R: kubeadm join</p>
<p class="has-line-data" data-line-start="13" data-line-end="15">Para você adicionar um novo node em seu cluster, o comando é executado no node master ou no node a ser adicionado?<br>
R: no novo node</p>
<p class="has-line-data" data-line-start="16" data-line-end="18">Qual o comando exibe a linha de comando inteira, inclusive com o token e o ca-cert-hash, para adicionar novos nodes ao cluster?<br>
R: sudo kubeadm token create --print-join-command</p>
<p class="has-line-data" data-line-start="19" data-line-end="21">Qual comando cria um simples pod do Nginx?<br>
R:kubectl run nginx --image nginx</p>
<p class="has-line-data" data-line-start="22" data-line-end="24">Qual o comando lista os deployment do namespace default?<br>
R:kubectl get deploy</p>
<p class="has-line-data" data-line-start="25" data-line-end="27">Como eu posso criar um service para um deployment em execução?<br>
R:kubectl expose deployment/nome_do_deployment</p>
<p class="has-line-data" data-line-start="28" data-line-end="30">Eu posso ter a swap habilitada em meu cluster?<br>
R: Não</p>
<p class="has-line-data" data-line-start="31" data-line-end="33">Qual o comando utilizado para visualizar os nodes que fazem parte do meu node?<br>
R: kubectl get nodes</p>


<h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Dia 2</h2>
<p class="has-line-data" data-line-start="28" data-line-end="30">1º  Eu tenho um arquivo .yaml que possui as informações de um deployment que eu preciso criar. A pergunta é: Qual o comando é utilizado para criar um deployment especificado a partir de um arquivo yaml?<br>
<p class="has-line-data" data-line-start="28" data-line-end="30"> resposta kubectl creat -f<br>

 <p class="has-line-data" data-line-start="28" data-line-end="30">2º Qual o comando utilizado para exibir os detalhes sobre determinado deployment, sendo que sua saída deverá ser no padrão yaml?/p>
 <p class="has-line-data" data-line-start="28" data-line-end="30"> resposta kubectl get deploy nome_deploy -o yaml <br>
 <p class="has-line-data" data-line-start="28" data-line-end="30"> 3º O que melhor define um service node port?  <br> 
 <p class="has-line-data" data-line-start="28" data-line-end="30"> RESPOSTA - Permite que determinada porta de todos os nodes do cluster seja ultilizada pelo cliente para acessar os endpoints desse service<br>
 <p class="has-line-data" data-line-start="28" data-line-end="30"> 4º O que melhor define um service clusterIP?  <br>
 <p class="has-line-data" data-line-start="28" data-line-end="30"> Resposta -> Automaticamente realiza a criação de um ip privado, que somente poderá ser acessado de dentro do cluster <br>
<p class="has-line-data" data-line-start="28" data-line-end="30"> 5º O que melhor define um service load balancer?<br>
  <p class="has-line-data" data-line-start="28" data-line-end="30">Resposta -> quando integrado com seu cloud provider, automaticamente realiza a criação de um ip publico, que sera ultilizado pelo cliente para acessar os endpointss desse service <br>
<p class="has-line-data" data-line-start="28" data-line-end="30"> 6º Dentro de um arquivo .yaml onde estou definindo as caracteristicas de meu deployment, me bateu a dúvida sobre como é a sintaxe correta quando eu quero destinar apenas 20% de um CPU para o container, você se lembra?  <br>
<p class="has-line-data" data-line-start="28" data-line-end="30"> Resposta -> cpu: 0.2 <br>
<p class="has-line-data" data-line-start="28" data-line-end="30"> 7º Sempre quando estou criando meus yaml para definir um novo deployment, sempre fico na duvida na hora de limitar os recursos como CPU e memória. Qual a finalidade do requests e o limits?  <br>
<p class="has-line-data" data-line-start="28" data-line-end="30"> Resposta -> O request determina o valor que será garantido ao container, enquanto o limits determina o valor que o container não poderá passar  <br>

<p class="has-line-data" data-line-start="28" data-line-end="30"> 8º Como eu faço para criar, via linha de comando, um namespace? <br>
  <p class="has-line-data" data-line-start="28" data-line-end="30"> 8º kubectl create namespace NOME_NAMESPACE   <br>
    
<p class="has-line-data" data-line-start="28" data-line-end="30"> 9º Quando estou criando um LimitRange, o defaultrequest determina o valor que será garantido aos containers, enquanto o limits determina o valor que os containers não poderão ultrapassar.   <br>
  <p class="has-line-data" data-line-start="28" data-line-end="30"> resposta 9º -> verdadeiro   <br>

<p class="has-line-data" data-line-start="28" data-line-end="30"> 10º Qual o comando utilizado para que determinado node pare de receber novos containers?  <br>
  <p class="has-line-data" data-line-start="28" data-line-end="30"> resposta 10º -> kubectl taint node elliot-02 key1=value1:NoSchedule <br>
   
<h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Dia 3</h2>   
<h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a> O que é um DaemonSet?</h2>   
    <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></Responsavel por gerenciar um grupo de pods, onde teremos um pod por node</h2>   
    <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>O que é um ReplicaSet?</h2>   
    <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Responsavel por gerenciar um grupo de pods, onde teremos o numero de pods que for solicitado</h2>   
    <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Quero listar todos os labels de determinado node, como eu faço?</h2>   
    <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>kubectl label nodes meu_node --list</h2>   
    <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Eu adicionei um label chamado NODE=tosko em todos os meus nodes do cluster. Como eu posso remover esse label de todos os nodes?</h2>   
    <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>kubectl label nodes --all NODE-</h2>   
    <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Qual o comando utilizado para acompanhar um rollout?</h2>   
    <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>kubectl rollout status daemonset meu_daemonset</h2>   
    <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Qual o comando utilizado para fazer o rollback de um daemonset para uma determina 'revision'?</h2>   
 <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>kubectl rollout undo ds meu_deamonset --to-revision=1</h2> 
 
 <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Dia 4</h2>
  <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a> Qual a definição para PV?</h2>
  <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Persistence Volume</h2>
  <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Qual a definição para PVC?</h2>
  <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Persistence Volume Claim</h2>
  <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>O que é PV?</h2>
  <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Um pedaço de storage em nosso cluster, provisionado pelo administrador do cluster ou pelo Storage Class</h2>
  <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Estou editando um arquivo yaml para a criação de um Job. Qual é a linha que define o tipo de resource que estou criando?</h2>
  <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Kind: job</h2>
  <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Como eu posso ver os logs da execução de um Job?</h2>
  <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>kubectl logs nome_do_container_responsavel_pelo_job</h2>
  <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Preciso criar um secret e seu conteúdo será o conteúdo de um arquivo, como eu faço?</h2>
  <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>kubectl create secret generic my-secret --from-file=arquivo_desejado.txt</h2>
  <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Qual a função de um InitContainer?</h2>
  <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Executar algumas tarefas antes do container principal ser iniciado</h2>
  <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Para que serve um ClusterRoleBinding?</h2>
  <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Para associar o ServiceAccount com o ClusterRole</h2>
  <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Qual o nome dos arquivos que o Helm utiliza para realizar a instalação e configuração de aplicações?</h2>
  <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></ahelm chart</h2>
   
 <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a> Dia 5 </h2>
    <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Qual a definição para o Ingress?
 </h2>
    <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>O Ingress expõe rotas HTTP e HTTPS de fora do cluster para serviços dentro do cluster. O roteamento de tráfego é controlado pelas regras definidas no recurso do Ingress. </h2>
    <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Como eu posso visualizar os Ingress criados em meu cluster? </h2>
    <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>kubectl get ingress </h2>
    <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Estou criando um arquivo yaml para definir um novo Ingress para minha app. Qual opção define o tipo de resource que eu estou criando? </h2>
    <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>kind: Ingress </h2>
    <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>Como eu posso ver os detalhes de um Ingress criado? Escolha duas alternativas </h2>
    <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a>kubectl describe ingresses.extensions app-ingress </h2>
    <h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Dia_1_1"></a> </h2>
 

