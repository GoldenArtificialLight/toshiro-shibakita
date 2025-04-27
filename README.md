# 🐋Docker: Utilização prática no cenário de Microsserviços
## Denilson Bonatti, Instrutor - Digital Innovation One

Neste desafio de projeto, fui apresentado à arquitetura de microsserviços em nuvem através do Docker, uma ferramenta de conteinerização de sistemas.

O desafio consistia em configurar um cluster Swarm – uma funcionalidade do Docker – para escalar contêineres em múltiplas máquinas virtuais EC2 na AWS.

## 🏛Detalhes da arquitetura
### Cluster Swarm

Há, ao todo, três máquinas virtuais (ou instâncias) EC2 com docker instalado. A primeira máquina atua como mestre num cluster de contêineres através de uma funcionalidade nativa do Docker, chamada Swarm, enquanto as outras participam do cluster com seus contêineres e são gerenciadas pela primeira.

### Espelhamento e escalabilidade

As máquinas contém uma imagem docker executando um servidor web apache, responsável por receber e processar requisições HTTP na porta 80 e executar uma página PHP, a qual tem uma conexão com um banco de dados MySQL presente na primeira máquina. Para facilitar o compartilhamento dessa página PHP entre as três, é utilizado um software de compartilhamento de arquivos chamado NFS, instalado como servidor na primeira máquina e como cliente nas demais. O NFS espelha os conteúdos da pasta da página web entre as três instâncias.

### Distribuição de carga

Para reduzir o estresse nas máquinas individuais, é preciso fazer com que as requisições HTTP sejam distribuídas entre as três instâncias. Isso é possível através da criação de um proxy com a ferramenta NGINX. Esse software recebe as requisições na porta 4500 da máquina principal e replica para as outras duas.

## 📁Detalhes dos Arquivos

Os arquivos presentes nesse repositório são os recursos utilizados para a criação do sistema. Abaixo, segue uma breve descrição de seu conteúdo e/ou propósito:
- **banco.sql**: Contém um código para criação da tabela de exemplo "dados". Deve ser utilizado no banco já criado.
- **index.php**: Contém a página PHP mencionada.
- **nginx.conf**: Contém a configuração do proxy. É preciso trocar os endereços IP para os que forem determinados ao criar as instâncias.
- **dockerfile**: Parâmetros de criação da imagem docker que executa o nginx e o proxy.

## 💭O que aprendi

Apesar de não ter experiência com contêineres, nuvem e microsserviços, pude perceber a flexibilidade que essa arquitetura propicia, pois permite o desacoplamento do sistema e, consequentemente, uma facilidade maior ao gerenciar recursos relacionados, mas independentes. Além disso, utilizar tais tecnologias permite escalar serviços e forma gradual e controlada, sem que seja preciso escalar o sistema inteiro, reduzindo custos e esforços. É uma boa estratégia que não pode ser ignorada nos tempo atuais.
