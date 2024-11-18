---
title: Docker
tags:
  - devops
fonte: https://www.youtube.com/watch?v=RqTEHSBrYFw
---
# Docker

A containerização é sobre empacotar uma aplicação e suas dependências em um contêiner, garantindo que ela funcione da mesma forma em todos os lugares. Os contêineres são o novo padrão para empacotar software. Eles garantem que sua aplicação funcione de maneira consistente em diferentes ambientes, o que simplifica a implantação e o gerenciamento. O Docker é a ferramenta preferida para containerização.

> [!info] Links Docker
> - [Docker Cheat Sheet & Quick Reference](https://cheatsheets.zip/docker)
> - [Docker Roadmap - roadmap.sh](https://roadmap.sh/docker)

> [!tip] Veja +
> 
> [[Docker Compose]]

## Conceitos Fundamentais

Esses três componentes trabalham juntos para permitir que o Docker forneça um ambiente leve e isolado para executar aplicações, facilitando o desenvolvimento, a implantação e a escalabilidade.

### Namespaces

Os namespaces são uma característica do kernel do Linux que permite isolar recursos entre diferentes processos. Isso significa que cada container Docker pode ter sua própria visão de certos recursos do sistema, como:

* PID Namespace: Isola os IDs de processo, permitindo que processos em diferentes containers tenham o mesmo ID de processo.
* Network Namespace: Isola a pilha de rede, permitindo que cada container tenha suas próprias interfaces de rede e endereços IP.
* Mount Namespace: Isola o sistema de arquivos, permitindo que cada container tenha seu próprio sistema de arquivos montado.
* User Namespace: Isola os IDs de usuário e grupo, permitindo que um processo em um container seja executado com um ID de usuário diferente do que tem no host.

Esses namespaces garantem que os containers sejam isolados uns dos outros e do sistema host, aumentando a segurança e a eficiência.

### Control Groups (cgroups)

Os cgroups são outra funcionalidade do kernel do Linux que permite limitar, contabilizar e isolar o uso de recursos (como CPU, memória, disco, etc.) por grupos de processos. No contexto do Docker, os cgroups são usados para:

* Limitar Recursos: Você pode definir limites de CPU e memória para um container, garantindo que ele não consuma mais recursos do que o permitido.
* Monitorar Uso de Recursos: Os cgroups permitem que você monitore o uso de recursos de cada container, ajudando na identificação de problemas de desempenho.
* Isolamento de Recursos: Garante que um container não interfira no desempenho de outros containers ou do sistema host.

### Union Filesystem (Overlay FS)

O Union Filesystem é uma técnica que permite que múltiplos sistemas de arquivos sejam empilhados em um único sistema de arquivos. O Overlay FS é uma implementação específica dessa técnica que é usada pelo Docker para gerenciar imagens e containers. Ele funciona da seguinte maneira:

* Camadas: Cada imagem Docker é composta por várias camadas. Quando você cria um container a partir de uma imagem, o Docker cria uma nova camada "overlay" que permite que você faça alterações no sistema de arquivos do container sem modificar a imagem base.
* Eficiência: Como as camadas são compartilhadas entre diferentes containers, o uso de espaço em disco é otimizado. Vários containers podem usar a mesma camada base, economizando espaço.
* Imutabilidade: As camadas de uma imagem são imutáveis, o que significa que, uma vez criadas, não podem ser alteradas. Isso garante que as imagens sejam consistentes e reprodutíveis.

## Persistência de dados

**Imagens e Contêineres:**

* Uma imagem de contêiner é um modelo de leitura que contém todos os arquivos e dependências necessárias para executar um aplicativo. Quando um contêiner é criado a partir de uma imagem, ele é considerado um ambiente isolado e temporário.
* O contêiner possui uma camada de leitura (a imagem) e uma camada de gravação (a nova camada que permite modificações). As alterações feitas no contêiner são armazenadas apenas nessa camada de gravação.

![](https://github.com/sidpalas/devops-directive-docker-course/raw/main/04-using-3rd-party-containers/readme-assets/container-filesystem.jpg)

**Instalação de Dependências:**

* O exemplo demonstra como instalar um pacote (neste caso, o ping) em um contêiner em execução. Ao executar o comando apt install iputils-ping, o pacote é instalado na camada de gravação do contêiner. Quando o contêiner é encerrado e um novo contêiner é iniciado a partir da mesma imagem, ele não possui as alterações feitas anteriormente, pois cada contêiner é isolado e não compartilha a camada de gravação.

```bash
# Create a container from the ubuntu image
docker run --interactive --tty --rm ubuntu:22.04
# Try to ping google.com
ping google.com -c 1 # This results in `bash: ping: command not found`
# Install ping
apt update
apt install iputils-ping --yes
ping google.com -c 1 # This time it succeeds!
exit
docker run -it --rm ubuntu:22.04
ping google.com -c 1 # It fails! 🤔
```

**Reutilização de Contêineres:**

* Para manter as alterações feitas em um contêiner, é possível nomeá-lo e não usar a flag `--rm`, que remove o contêiner após a parada. Isso permite que o contêiner seja reiniciado e reutilizado, mantendo as alterações feitas durante a execução anterior. O uso dos comandos docker start e docker attach permite que o usuário retome a sessão do contêiner existente, onde as alterações (como a instalação do ping) ainda estão disponíveis.

```bash
# Create a container from the ubuntu image (with a name and WITHOUT the --rm flag)
docker run -it --name my-ubuntu-container ubuntu:22.04
# Install & use ping
apt update
apt install iputils-ping --yes
ping google.com -c 1
exit
# List all containers
docker container ps -a | grep my-ubuntu-container
docker container inspect my-ubuntu-container
# Restart the container and attach to running shell
docker start my-ubuntu-container
docker attach my-ubuntu-container
# Test ping
ping google.com -c 1 # It should now succeed! 🎉
exit
```

**Incluir dependências diretamente na imagem do contêiner:**

* Contêineres são projetados para serem efêmeros e descartáveis. Isso significa que, ao parar ou remover um contêiner, todas as alterações feitas durante sua execução (incluindo a instalação de pacotes) são perdidas. Portanto, não é uma boa prática confiar que um contêiner manterá dados ou configurações entre execuções. Para garantir que todas as dependências necessárias estejam disponíveis sempre que um contêiner for iniciado, é melhor incluí-las diretamente na imagem do contêiner. Isso é feito através de um Dockerfile, que é um arquivo de texto que contém instruções sobre como construir uma imagem Docker.

```bash
# Build a container image with ubuntu image as base and ping installed
docker build --tag my-ubuntu-image -<<EOF
FROM ubuntu:22.04
RUN apt update && apt install iputils-ping --yes
EOF
# Run a container based on that image
docker run -it --rm my-ubuntu-image
# Confirm that ping was pre-installed
ping google.com -c 1 # Success! 🥳
```

**Persistência de dados gerados por aplicações**

* Muitas aplicações geram dados que precisam ser armazenados de forma segura, como dados de banco de dados ou arquivos enviados por usuários. Esses dados são críticos e não devem ser perdidos quando um contêiner é destruído ou recriado.

```bash
# Create a container from the ubuntu image
docker run -it --rm ubuntu:22.04
# Make a directory and store a file in it
mkdir my-data
echo "Hello from the container!" > /my-data/hello.txt
# Confirm the file exists
cat my-data/hello.txt
exit

# Create a container from the ubuntu image
docker run -it --rm ubuntu:22.04
# Check if the file exists
cat my-data/hello.txt # Produces error: `cat: my-data/hello.txt: No such file or directory`
```

* O Docker oferece uma solução para esse problema através de volumes e montagens. Essas funcionalidades permitem que você especifique um local onde os dados devem ser armazenados, garantindo que eles persistam além do ciclo de vida de um único contêiner.

![](https://github.com/sidpalas/devops-directive-docker-course/raw/main/04-using-3rd-party-containers/readme-assets/volumes.jpg)

## Tipos de Montagens

### Volume Mount

Um local gerenciado pelo Docker onde os dados podem ser armazenados. Os volumes são a maneira recomendada de persistir dados, pois são gerenciados pelo Docker e podem ser facilmente compartilhados entre contêineres.

* Esses códigos exemplificam como usar volumes no Docker para garantir a persistência de dados gerados por contêineres. Ao criar um volume e montá-lo em um contêiner, os dados podem ser armazenados de forma segura e acessados em contêineres subsequentes. Essa abordagem é fundamental para aplicações que precisam manter dados, como bancos de dados ou arquivos de configuração, mesmo quando os contêineres são destruídos e recriados.

```bash
# create a named volume
docker volume create my-volume
# Create a container and mount the volume into the container filesystem
docker run  -it --rm --mount source=my-volume,destination=/my-data/ ubuntu:22.04
# There is a similar (but shorter) syntax using -v which accomplishes the same
docker run  -it --rm -v my-volume:/my-data ubuntu:22.04
# Now we can create and store the file into the location we mounted the volume
echo "Hello from the container!" > /my-data/hello.txt
cat my-data/hello.txt
exit
# Create a new container and mount the volume into the container filesystem
docker run  -it --rm --mount source=my-volume,destination=/my-data/ ubuntu:22.04
cd my-data
cat hello.txt # This time it succeeds! 
exit
```

* Quando você usa o Docker Desktop em um sistema operacional como Windows ou macOS, o Docker não é executado diretamente no sistema operacional host. Em vez disso, ele roda dentro de uma máquina virtual Linux. Isso é importante porque a estrutura de diretórios e a localização dos dados do Docker são diferentes do que você encontraria em um sistema Linux padrão. Os dados dos volumes do Docker são armazenados em /var/lib/docker/volumes na máquina virtual Linux que o Docker Desktop utiliza. Isso significa que, para acessar os dados persistentes que você armazenou em volumes, você precisa acessar essa máquina virtual.

### Bind Mount

Um local no sistema de arquivos do host que é montado no contêiner. Isso permite que os dados sejam persistidos em um diretório específico do host. Isso permite que você compartilhe dados entre o host e o contêiner de maneira mais direta.


* `${PWD}` é uma variável de ambiente no shell (como Bash) que representa o "diretório de trabalho atual" (current working directory). Quando você usa `${PWD}` em um comando, ele é substituído pelo caminho completo do diretório em que você está no momento em que o comando é executado.
* `-v ${PWD}/my-data:/my-data`: Esta opção monta um volume. O que acontece aqui é:
	* `${PWD}/my-data`: Refere-se ao diretório `my-data` localizado no diretório de trabalho atual do host (onde você executou o comando).
	* `:/my-data`: Este é o ponto de montagem dentro do contêiner. O diretório `my-data` do host será acessível no contêiner no caminho `/my-data`.
* **Tmpfs Mount**: Um armazenamento em memória que não persiste após a saída do contêiner. É usado para dados temporários que não precisam ser mantidos, como arquivos de credenciais. Embora seja mencionado, não deve ser usado para dados que você deseja persistir.

```bash
# Create a container that mounts a directory from the host filesystem into the container
docker run  -it --rm --mount type=bind,source="${PWD}"/my-data,destination=/my-data ubuntu:22.04
# Again, there is a similar (but shorter) syntax using -v which accomplishes the same
docker run  -it --rm -v ${PWD}/my-data:/my-data ubuntu:22.04
echo "Hello from the container!" > /my-data/hello.txt
# You should also be able to see the hello.txt file on your host system
cat my-data/hello.txt
exit
```

- [ ] DOING https://youtu.be/RqTEHSBrYFw?t=5285