# Configuração de VM's para uso do kubernetes com o Vagrant
Este projeto é apenas para facilitar a instalação de dependencias para uso do kubernetes.

## Dependências

É necessário ter instalado o [VirtualBox](https://www.virtualbox.org/)
e o [Vagrant](https://www.vagrantup.com/downloads)  

## Para utilizar

```bash
vagrant up
```

## Entrando nas máquinas
as máquinas são tem os seguintes nomes:
node-1,node-2 e node-3.
escolha o node desejado e utilize o comando:

```bash
vagrant ssh <nome-do-node-desejado>
```


## No master node
Escolha um node para ser o seu master, e utilize os seguintes comandos nele:

```bash
export MASTER_IP=<Ip-da-maquina>
kubeadm init --apiserver-advertise-address=${MASTER_IP} --pod-network-cidr=10.244.0.0/16
```

## Nos workers
Utilizar o comando de retorno que foi trazido após o comando acima

## Node master, Ápos entrada dos workers no cluster

Precisamos agora instalar a CNI do nosso cluster, no caso utilizei o flannel com o seguinte commando:

```bash
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

## License
[MIT](https://choosealicense.com/licenses/mit/)
