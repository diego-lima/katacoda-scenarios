Neste cenário, vamos aprender o passo a passo para fazer uma instalação Linux de um nó numa rede Ethereum.

O objetivo é aprender a configurar vários nós usando docker, e conectá-los em seguida. Uma vez conectados, vamos verificar que os nós criados realmente implementam toda a teoria de blockchain: as transações, a propagação dos blocos, a interação entre contas e contratos inteligentes.

Nossa trilha será a seguinte:

- Observar as configurações de rede necessárias para instaurar uma rede em pleno funcionamento
- Instalar o Docker, para gerência facilitada de dependências
- Rodar uma imagem pré-montada, que já tem tudo necessário para começar a rodar um nó
- Replicar essa imagem para simular vários nós, e conectá-los 
- Experimentar transações, observar o movimento da rede, etc.