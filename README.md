
### Setup

* Ubuntu 14.04 ou superior.
* `sudo apt-get update`
* `sudo apt-get upgrade`
* `sudo apt-get install python-pip git ansible sqlite3 python-numpy python-networkx python-matplotlib nmap aptitude`
* `sudo pip install enum`
* `sudo vim /etc/ansible/hosts`
* Add: `localhost ansible_connection=local`
* `git clone https://github.com/phfaustini/containernet.git`
* `cd containernet/ansible`
* `sudo ansible-playbook install.yml` # Arquivo .yml modificado para docker-py 1.7.2 em função de bug em versões mais recentes: https://github.com/docker/docker-py/issues/1054
* Testar se instalação funcionou: `sudo mn` o shell interativo deve conter a expressão `containernet >`. Se sim, ambiente Mininet com suporte a Docker está funcionando.

### Executar exemplo de ambiente

* Arquivos da pasta containernet/controller devem ser movidos ou copiados para ~/pox/ext
* Para invocar o controlador: `cd ~/pox && ./pox.py log.level --INFO spanning_tree samples.pretty_log openflow.discovery`
* Build todas imagens Docker (ver comando na primeira linha de server/Dockerfile e orchestrator/Dockerfile; terceira linha de cada arquivo mostra como executar em modo 'standalone')
* Em orchestrator/ estao os ambientes Mininet
* Em outro terminal, executar uma topologia (e.g. orchestratorFirewall.py).
* No terminal principal, aparecem as informações coletadas pelo agente. Nos xterms abertos, pode-se controlar os hosts clientes.
* Para o cliente solicitar um vídeo a um servidor: `sh start.sh`


