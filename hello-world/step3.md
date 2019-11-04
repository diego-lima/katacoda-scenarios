Vamos rodar uma imagem pré-montada que foi preparada para facilitar a instalação de um nó ethereum:

`docker run --name meu_no_ethereum -e "identity=meu_no_ethereum" -d diblacksmith/no_ethereum_exemplo`{{execute}}

Com isso, colocamos o nó para executar em segundo plano. Para verificar isso, liste os containers em execução:

`docker ps`{{execute}}

Para se conectar ao nosso cliente, vamos iniciar uma sessão interativa:

`docker container exec -it meu_no_ethereum sh -c 'geth attach $datadir/geth.ipc'`{{execute}}

Agora, dentro da sessão interativa, podemos rodar vários comandos.

Digite `admin.nodeInfo.enode`{{execute}} para encontrar o endereço do nó dentro da rede.

Isso vai mostrar qual endereço os outros nós podem utilizar para se conectar ao seu.

Aperte `Ctrl + D` para sair da sessão interativa do cliente.

## O que aconteceu?

Como utilizamos uma imagem já pronta, muitos detalhes acabaram fugindo da nossa atenção.

Porém, a verdade é que muita coisa já foi previamente decidida. Algumas delas:
- A versão do cliente ethereum é o _Geth_ v1.8.27
- O algoritmo de consenso é o _Proof of Authority_
- Quatro contas já foram previamente criadas
- As quatro contas já foram previamente "carregadas" com saldo
- Uma das quatro contas já recebeu "autoridade" para inserir novos blocos na cadeia (de acordo com o _Proof of Authority_)
- O arquivo _genesis.json_, que abarca todas as informações do primeiro bloco da cadeia e deve ser igual para todos os nós da rede, já foi escrito