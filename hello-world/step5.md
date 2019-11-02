Os passos até aqui serviram para você simular uma rede de nós dentro de uma mesma máquina. Isso porque, aqui nesse ambiente de aprendizado, não dá para testar com várias máquinas numa mesma rede.

Porém, para levar o que fizemos até agora para uma sala real com vários computadores, basta adicionar alguns parâmetros na hora de rodar a imagem:

`docker run --name meu_no_real -e "extip" -p 30303:30303 -d diblacksmith/no_ethereum_exemplo`{{execute}}

Observe que apenas acrescentamos dois parâmetros.

O `-e "extip"` faz com que o container receba, como uma variável de ambiente, o seu IP dentro da rede. Com isso, por causa da forma como a imagem foi construída, esse nó poderá funcionar sob o seu IP.

No `-p 30303:30303`, estamos mapeando a porta `30303` do container para a porta `30303` da nossa máquina host. Essa é a porta de operação normal do cliente, que a utiliza para se conectar com outros nós (na hora de montar a rede peer to peer).