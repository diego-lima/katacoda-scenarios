O primeiro passo é baixar e rodar uma imagem Docker com o cliente Geth instalado.

## Imagem docker

Primeiro vamos **construir** a imagem:

`wget https://raw.githubusercontent.com/diego-lima/workshop_blockchain_navi/master/Dockerfile`{{execute}}

`docker build . -t cliente_geth`{{execute}}

Agora, **rodamos** a imagem:

`docker run -it -p 30303:30303  -p 8546:8546  -p 8545:8545 77035a6002bd \
    --datadir /root/workshop_blockchain_navi/rede \
    --networkid=621 --nat extip:SEU IP --syncmode full  \
    --rpc --rpcaddr 0.0.0.0 --rpccorsdomain “*” \
    --wsport 8546 --wsorigins "*" --wsaddr 0.0.0.0 \
    console`{{execute}}
