Para simular um segundo nó, vamos simplesmente criar um novo container com a mesma imagem utilizada anteriormente.

Com isso, teremos dois clientes Ethereum rodando na mesma máquina, e eles irão se comportar como se fossem dois nós independentes.

Se esses passos fossem executados em uma segunda máquina (na mesma rede), eles poderiam se conectar do mesmo jeito.

## Rodando o segundo nó

Para instanciar um segundo nó, basta repetir o comando executado anteriormente, mudando apenas o nome do container que será criado. No segundo terminal, rode:

`docker run --name segundo_no -e "identity=segundo_no" -d diblacksmith/no_ethereum_exemplo`{{execute}}

Para verificar que, agora, temos os dois nós rodando:

`docker ps`{{execute}}

## Testando a conectividade

Para garantir que o primeiro nó conseguirá se conectar ao segundo, é bom realizar um teste antes.

Considerando o cenário em que o primeiro nó está na sua máquina e o segundo nó está em uma outra máquina, devemos ter certeza de que as duas máquinas conseguem se comunicar pela rede no IP e porta esperados.

No nosso caso, estamos rodando dois nós na mesma máquina, então é evidente que eles irão conseguir se comunicar. Porém, quando for a hora de conectar nós em máquinas diferentes, uma alternativa para testar a conectividade entre as duas máquinas é usando o comando `telnet`:

`telnet <IP DA OUTRA MAQUINA> <PORTA>`

Caso as duas máquinas consigam se conectar na rede, a saída deverá ser algo parecido com o seguinte:

`Trying 172.17.0.2...
Connected to 172.17.0.2.
Escape character is '^]'.
Connection closed by foreign host.`

Caso exista algum problema na conexão entre as máquinas, a saída poderá se parecer com o seguinte:

`Trying 172.17.0.2...
telnet: Unable to connect to remote host: No route to host`

Nesse caso, será necessário realizar mais investigação para conseguir desbloquear essa conexão entre as máquinas. No Windows, pode ser que seja necessário criar uma regra no firewall para permitir que a conexão aconteça.

No nosso caso, vamos simular esse teste usando o IP do segundo nó e a porta padrão de operação do cliente ethereum `30303`:

`export ip_segundo_no=$(docker inspect segundo_no | grep '"IPAddress"' | tail -n1 | awk '{print $2}' | cut -f2 -d'"') && echo ip do segundo no: $ip_segundo_no`{{execute}}

`telnet $ip_segundo_no 30303`{{execute}}

## Conectando os nós

Para efetivamente conectar os dois clientes, vamos precisar obter o endereço enode.

Inicie uma sessão interativa no primeiro nó e obtenha o enode da seguinte forma:

`docker container exec -it meu_no_ethereum sh -c 'geth attach $datadir/geth.ipc'`{{execute}}

`admin.nodeInfo.enode`{{execute}}

Com o enode do primeiro nó copiado, vamos iniciar uma sessão interativa no segundo nó e conectá-lo com o primeiro:
`docker container exec -it segundo_no sh -c 'geth attach $datadir/geth.ipc'`{{execute}}

`admin.addPeer("<AQUI O ENODE DO PRIMEIRO NÓ>")`{{execute}}

Uma chamada correta desse comando se parece com o seguinte:

`admin.addPeer("enode://24dcdfa2a2c38375c06d1a8bde0cbab554ad26d669bc41ade1d8120ddb48ff51575f2038b41f0b3c0f1e250a73e9bb5303e676cf7d649fe70f49482e940f8ecd@192.168.0.13:30303")`

Para verificar que a conexão foi realizada com sucesso, podemos obter a contagem de "peers" conectados (que deve ser superior a 0):

`net.peerCount`{{execute}}

Para verificar algumas informações sobre os nós conectados:

`admin.peers`{execute}

Observe que o nome do nó está de acordo:

`admin.peers[0].name`