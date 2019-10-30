FROM ethereum/client-go:v1.8.27
LABEL maintainer="ddddiegolima@gmail.com"


# Instalando dependências
RUN apk add git

# Montando a rede interna
RUN cd ~ && \
    git clone https://github.com/diego-lima/workshop_blockchain_navi && \
    cd workshop_blockchain_navi/rede && \
    geth --datadir . init genesis.json