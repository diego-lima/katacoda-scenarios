Vamos rodar uma imagem pré-montada que foi preparada para facilitar a instalação de um nó ethereum:

`docker run --name meu_no_ethereum -e "extip" -d diblacksmith/no_ethereum_exemplo`{{execute}}

Com isso, colocamos o nó para executar em segundo plano. Para verificar isso, liste os containers em execução:

`docker ps`{{execute}}

Para se conectar ao nosso cliente, vamos iniciar uma sessão interativa:

`docker container exec -it meu_no_ethereum sh -c 'geth attach $datadir/geth.ipc'`{{execute}}

Agora, dentro da sessão interativa, podemos rodar vários comandos.

Digite `admin.nodeInfo.enode`{{execute}} para encontrar o endereço do nó dentro da rede.

Isso vai mostrar qual endereço os outros nós podem utilizar para se conectar ao seu. **Anote esse resultado em algum lugar, pois será necessário na hora de conectar um nó com outro.**

Aperte `Ctrl + D` para sair da sessão interativa do cliente.