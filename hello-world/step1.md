O primeiro passo é baixar e rodar uma imagem Docker com o cliente Geth instalado.

## Preparando

Primeiramente, vamos só descobrir qual nosso ip dentro da rede:

`export extip=$(ip addr | grep 'state UP' -A2 | tail -n1 | awk '{print $2}' | cut -f1 -d'/') && echo "seu ip: $extip"`{{execute}}

 Verifique se o seu IP foi detectado corretamente analisando o output do comando abaixo:

 `ip addr`{{execute}}

## Imagem docker

Vamos rodar uma imagem pré-montada que foi preparada para facilitar a instalação de um nó ethereum:

`docker run --name meu_no_ethereum -e "extip" -d diblacksmith/no_ethereum_exemplo`{{execute}}

Com isso, colocamos o nó para executar em segundo plano. Para verificar isso, liste os containers em execução:

`docker ps`{{execute}}

Para se conectar ao nosso cliente, vamos iniciar uma sessão interativa:

`docker container exec -it meu_no_ethereum sh -c 'geth attach $datadir/geth.ipc'`{{execute}}

Agora, dentro da sessão interativa, podemos rodar vários comandos.

Digite `admin.nodeInfo.enode`{{execute}} para encontrar o endereço do nó dentro da rede.

Isso vai mostrar qual endereço os outros nós podem utilizar para se conectar ao seu.

## Descobrindo o endereço do nó (outra forma)

`export meu_nodekey=$(docker container exec -it no_1 sh -c "cat /root/workshop_blockchain_navi/rede/geth/nodekey")`{{execute}}
`echo "enode://$meu_nodekey@$meu_ip:30303"`{{execute}}