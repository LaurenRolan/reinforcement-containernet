
### Setup
* Virtual Box 5.1. Duas opções diferentes de configurações:
* 1) Vá em File -> Preferences -> Network -> "Add host-only network" button com configurações default. Isso permite, se necessário no futuro, acessar a VM a partir da máquina host (e.g. ssh).
* 2) Botão direito sobre Docker Clone -> Network -> Adapter 2 -> Desabilite a caixa "Enable Network Adapter". Isso não permite um ssh na VM, mas por ora é irrelevante.

### Controlador:

* Executar:
	`cd ~/pox && ./pox.py log.level --INFO spanning_tree samples.pretty_log openflow.discovery`

* def initialise(filename="ext/switch_portsF.csv"):
	* Recebe um .csv com a topologia. Cada linha diz respeito a um switch. Primeira coluna informa o switch. As colunas seguintes informam o que se conecta a cada porta daquele switch.


* def send_orchestrator(ip="127.0.0.1", port=50008, filename="paths"):
	* Envia ao orquestrador, por TCP, algum arquivo.

* def change_route(ip="127.0.0.1"):
	* Recebe um pedido do orquestrador para alterar uma rota entre dois hosts. O formato é a seguinte string:
		* # "src,dst,route", como, por exemplo, "h3|h1|1" (optar pela rota 1 entre h3 e h1)

* def calculate_paths():
	* Calcula os caminhos, em switches, entre dois hosts. Por ora, está estático.
	

* Estruturas de dados:
	* paths: dicionário. Chave é uma tupla de strings representando hosts (e.g. ("h1, h3")). Conteúdo é uma lista de lista. Cada sublista representa um caminho entre os dois hosts. São formadas por strings. Cada string é o nome de um switch que compõe a rota entre os hosts. (e.g. paths[("h1, h3")] = [ ['s1', 's3']  , ['s1', 's2', 's3']  ]

	* default_route: dicionário. Chave é uma tupla de strings representando hosts. Valor é o caminho, dentre os possíveis descritos na variável 'path', efetivamente adotado pelo controlador.

	* switch_ports: dicionário. Chave é um switch, e valor é uma lista com o que está conectado a cada porta do switch. Por exemplo, # switch_ports['s1'] = ['s2','s3','s5','h1','nat0''], siginifica que s2 está na porta eth1, s3 está conectado à porta eth2, e assim por diante.

	* link_status. Dicionário que traz informações sobre os links. A chave é uma tupla de strings, contendo switch e porta. Por exemplo, link_status[(s1, 1)] = [s2, cumulative, differenceFromLastTimStep], link_status[(s1, 2)] = [s3, 5025252562155, 43242],  # link s1-eth2, indo para s3, tinha 43242 bytes de tráfego no último time step, e 5025252562155 bytes trafegados desde o princípio.

	* ip_to_mac: dicionário que mapeia, como o nome diz, um endereço IP para um endereço MAC. Por ora, está estático. Assim como a descoberta de topologia, feita por um arquivo csv, pode ser dinamizada.


### OrchestratorFirewall

* Ambiente com hosts e conteiners. Para inicializar, basta digitar em um terminal `sudo python orchestratorFirewall.py`

* O terminal exibe informacoes da rede. Terminais xterm dos clientes abrem. Ao digitar `sh start.sh`, o respectivo cliente solicita um arquivo a um servidor.

* No mesmo arquivo há dois simples firewalls que bloqueiam o tráfego de um dado host. A linhas 328-331 mostram comandos de exemplo para se fazer isso com um host.

* Estrutura mais importante: q_table_traffic, que recebe as recompensas dos balanceamentos conforme equacao de atualizacao do algoritmo sarsa (funcao: update_q_table_traffic(self, reward, state, action)). 

### Dockerfiles

* Abrigam funções de rede (e.g. firewall). Mas são versáteis e podem abrigar muitas coisas diferentes. No exemplo, os servidores são contêineres também.

* Primeira linha dos arquivos Dockerfile contém informações de como construí-los, executá-los em separado, etc.
