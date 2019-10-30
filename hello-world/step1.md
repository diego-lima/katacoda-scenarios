O primeiro passo é baixar e rodar uma imagem Docker com o cliente Geth instalado.

## Alguns utilitários

Primeiramente, vamos só instalar alguns utilitários:

`apt-get update && apt-get install wget`{{execute}}

Agora, vamos descobrir qual é o nosso IP dentro da rede:

`export meu_ip=$(ip addr | grep 'state UP' -A2 | tail -n1 | awk '{print $2}' | cut -f1 -d'/') && echo "seu ip: $meu_ip"`{{execute}}

 Verifique se o seu IP foi detectado corretamente analisando o output do comando abaixo:

 `ip addr`{{execute}}

## Imagem docker

Primeiro vamos **construir** a imagem:

`wget https://raw.githubusercontent.com/diego-lima/workshop_blockchain_navi/master/Dockerfile`{{execute}}

`docker build . -t cliente_geth`{{execute}}

Agora, **rodamos** a imagem:

`docker run -it -p 30303:30303 -p 8546:8546 -p 8545:8545 \
    --name no_1 cliente_geth \
    --datadir /root/workshop_blockchain_navi/rede \
    --networkid=621 --nat extip:$meu_ip --syncmode full  \
    --rpc --rpcaddr 0.0.0.0 --rpccorsdomain “*” \
    --wsport 8546 --wsorigins "*" --wsaddr 0.0.0.0 \
    console`{{execute}}

Digite `admin.nodeInfo.enode`{{execute}}.

Isso vai mostrar qual o endereço do seu nó.

## Descobrindo o endereço do nó (outra forma)

Para que possamos nos conectar com outros nós, precisamos saber o endereço do nosso próprio.

Saia do nó, pressionando `Ctrl + (P + Q)`.

`export meu_nodekey=$(docker container exec -it no_1 sh -c "cat /root/workshop_blockchain_navi/rede/geth/nodekey")`{{execute}}

`echo "enode://$meu_nodekey@$meu_ip:30303"`{{execute}}

Copie esse resultado.
