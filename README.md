
### Setup

* Recomendo esta imagem: http://yuba.stanford.edu/~srini/tutorial/SDN_tutorial_VM_64bit.ova
* `sudo apt-get update`
* `sudo apt-get upgrade`
* `sudo apt-get install python-pip git ansible sqlite3 python-numpy python-matplotlib nmap aptitude`
* `sudo pip install enum`
* `sudo vim /etc/ansible/hosts`
* Add: `localhost ansible_connection=local`
* `git clone https://github.com/containernet/containernet.git`
* `cd containernet/ansible`
* `sudo ansible-playbook install.yml`


### Executar

* Arquivos da pasta controlador devem ficar em ~/pox/ext
* Controlador deve ser invocado a partir de ~/pox/ (primeira linha de controllerFirewall.py descreve como)
* Build todas imagens Docker (ver dockerfiles)
* Em orchestrator/ estao os ambientes Mininet

* Em um terminal, executar o controlador.
* Em outro, executar topologia (e.g. orchestratorFirewall.py).


