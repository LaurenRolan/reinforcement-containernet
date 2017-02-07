
### Setup
* Virtual Box 5.1. Duas opções diferentes de configurações:
* 1) Vá em File -> Preferences -> Network -> "Add host-only network" button com configurações default. Isso permite, se necessário no futuro, acessar a VM a partir da máquina host (e.g. ssh).
* 2) Botão direito sobre Docker Clone -> Network -> Adapter 2 -> Desabilite a caixa "Enable Network Adapter". Isso não permite um ssh na VM, mas por ora é irrelevante.

### Controlador:

* def initialise(filename="ext/switch_portsF.csv"):
	* Recebe um .csv com a topologia


* def send_orchestrator(ip="127.0.0.1", port=50008, filename="paths"):
	* Envia ao orquestrador, por TCP, algum arquivo.

* def change_route(ip="127.0.0.1"):
	* Recebe um pedido do orquestrador para alterar uma rota entre dois hosts. O formato é a seguinte string:
		* # "src,dst,route", como, por exemplo, "h3|h1|1" (optar pela rota 1 entre h3 e h1)
	

* Estruturas de dados:
	* paths: dicionário. Chave é uma tupla de strings representando hosts (e.g. ("h1, h3")). Conteúdo é uma lista de lista. Cada sublista representa um caminho entre os dois hosts. São formadas por strings. Cada string é o nome de um switch que compõe a rota entre os hosts. (e.g. paths[("h1, h3")] = [ ['s1', 's3']  , ['s1', 's2', 's3']  ]

* default_route: dicionário. Chave é uma tupla de strings representando hosts. Valor é o caminho, dentre os possíveis descritos na variável 'path', efetivamente adotado pelo controlador.

* switch_ports: dicionário. Chave é um switch, e valor é uma lista com o que está conectado a cada porta do switch. Por exemplo, # switch_ports['s1'] = ['s2','s3','s5','h1','nat0''], siginifica que s2 está na porta eth1, s3 está conectado à porta eth2, e assim por diante.

* link_status. Dicionário que traz informações sobre os links. A chave é uma tupla de strings, contendo switch e porta. Por exemplo, link_status[(s1, 1)] = [s2, cumulative, differenceFromLastTimStep], link_status[(s1, 2)] = [s3, 5025252562155, 43242],  # link s1-eth2, indo para s3, tinha 43242 bytes de tráfego no último time step, e 5025252562155 bytes trafegados desde o princípio.


