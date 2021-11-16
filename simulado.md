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
