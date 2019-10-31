O primeiro passo é descobrir qual o IP que estamos rodando dentro da rede.

Para isso, executamos o comando abaixo:

`export extip=$(hostname -I | cut -f1 -d ' ') && echo "seu ip interno na rede: $extip"`{{execute}}

_Caso você esteja usando outro sistema operacional (Windows ou MacOS), qualquer alternativa que te forneça o mesmo resultado (o seu IP dentro da rede) é suficiente._

Assim, estamos armazenando na variável de ambiente `extip` o nosso ip. Isso será usado mais pra frente, porque é importante informar, na hora de rodar o cliente Ethereum, qual o IP que ele deve estar atrelado. Sem isso, outros clientes que estiverem rodando na mesma rede não poderão se conectar ao nosso cliente.

E, para que possamos realmente montar uma rede de computadores participantes da mesma rede Ethereum, precisamos que todos os nós estejam conectados de alguma forma.