Para não precisar cuidar de todas as dependências atreladas ao _geth_, que é a implementação oficial do protocolo Ethereum (na linguagem _Go_), vamos usar uma imagem Docker com tudo prontinho dentro.

Para instalar o Docker:

`apt install docker.io -y`{{execute}}

_Caso você esteja usando outro sistema operacional (Windows ou MacOS), qualquer alternativa que te forneça o mesmo resultado (uma instalação Docker) é suficiente._

Para verificar que a instalação foi bem sucedida, execute:

`docker --version`{{execute}}

Agora, com o Docker instalado, podemos baixar qualquer imagem com dependências pré-configuradas que quisermos.