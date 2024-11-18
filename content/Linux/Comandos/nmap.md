---
title: nmap
tags:
  - cybersecurity
  - redes
---
O Nmap (Network Mapper) é uma ferramenta de código aberto usada para explorar e auditar a segurança de redes. Suas principais funções incluem:

1. **Descoberta de Hosts**: Identifica dispositivos ativos em uma rede.
2. **Varredura de Portas**: Verifica quais portas estão abertas, fechadas ou filtradas.
3. **Detecção de Serviços**: Identifica serviços e suas versões em portas abertas.
4. **Detecção de Sistema Operacional**: Tenta determinar o sistema operacional de um host.
5. **Auditoria de Segurança**: Ajuda a identificar vulnerabilidades em sistemas.
6. **Mapeamento de Rede**: Cria um mapa visual da rede.

Para descobrir o CIDR da rede use [[ifconfig]]

## `-sn`​

O comando `sudo nmap -sn 192.168.1.0/24`​ realiza uma varredura de rede usando o Nmap. Em resumo, esse comando irá identificar quais dispositivos estão ativos na sub-rede 192.168.1.0/24, uma "varredura de descoberta de hosts" (ping scan), sem verificar quais serviços estão rodando ou quais portas estão abertas:

* ​`sudo`​: Executa o comando com privilégios de superusuário, o que pode ser necessário para acessar informações de rede mais detalhadas.
* ​`nmap`​: Chama a ferramenta Nmap.
* ​`-sn`​: Este parâmetro indica que o Nmap deve realizar uma "varredura de descoberta de host" (ping scan) sem realizar a varredura de portas. Isso significa que o Nmap tentará identificar quais dispositivos estão ativos na rede, mas não verificará quais portas estão abertas.
* ​`192.168.1.0/24`​: Este é o intervalo de endereços IP que será escaneado. O `/24`​ indica que a varredura será feita em toda a sub-rede 192.168.1.0, que abrange os endereços de 192.168.1.1 a 192.168.1.254.

![[Untitled-2024-11-13-2255-20241113225600-s281fin.png]]
​​
Ao usar `sudo nmap -sn 192.168.1.1/24 | grep 192 | cut -d ' ' -f 5 > ips.txt`​ será salvo os ips localizados na rede:

```
192.168.1.1
192.168.1.103
192.168.1.101
```

## `-sA`​

A opção `-sA`​ no Nmap é utilizada para realizar uma varredura de "TCP ACK Scan". Essa técnica é usada principalmente para determinar quais portas estão filtradas em um host, ou seja, se um firewall ou um dispositivo de segurança está bloqueando o tráfego.

O que `-sA`​ faz:

1. **TCP ACK Scan**: O Nmap envia pacotes TCP com o flag ACK (Acknowledgment) definido para as portas especificadas. O objetivo é observar como o host de destino responde a esses pacotes.
2. **Identificação de Portas Filtradas**:
    * **Resposta de RST (Reset)** : Se o host responder com um pacote RST, isso indica que a porta está aberta ou fechada, dependendo do estado do firewall.
    * **Sem Resposta**: Se não houver resposta ou se o pacote for descartado, isso geralmente indica que a porta está filtrada (ou seja, um firewall está bloqueando o tráfego).
3. **Mapeamento de Firewall**: Essa técnica é útil para mapear regras de firewall, pois permite que você veja quais portas estão acessíveis e quais estão sendo filtradas sem enviar pacotes SYN, que são mais facilmente detectáveis por sistemas de detecção de intrusões.

O comando `sudo nmap -sA 192.168.1.0/24`​ faz o escaneamento

```bash
~/Kali ❯ sudo nmap -sA 192.168.1.0/24

Starting Nmap 7.95 ( https://nmap.org ) at 2024-11-08 18:16 -03
Nmap scan report for 192.168.1.1
Host is up (0.000085s latency).
All 1000 scanned ports on 192.168.1.1 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)
MAC Address: 38:6B:1C:18:1F:38 (Shenzhen Mercury Communication Technologies)

Nmap scan report for 192.168.1.103
Host is up (0.0019s latency).
All 1000 scanned ports on 192.168.1.103 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)
MAC Address: B4:2E:99:64:7B:41 (Giga-byte Technology)

Nmap scan report for 192.168.1.101
Host is up (0.0000070s latency).
All 1000 scanned ports on 192.168.1.101 are in ignored states.
Not shown: 1000 unfiltered tcp ports (reset)

Nmap done: 256 IP addresses (3 hosts up) scanned in 56.63 seconds
```

* **Not shown: 1000 unfiltered tcp ports (reset)** : diz que o Nmap recebeu uma resposta RST (Reset) para todas as 1000 portas. Isso indica que as portas estão **fechadas**, mas não filtradas. Em outras palavras, o host está respondendo ativamente, mas as portas não estão abertas para conexão.
* **Not shown: 1000 filtered tcp ports (no-response):**   indica que o Nmap não conseguiu obter informações sobre as 1000 portas escaneadas em um host específico, pois não recebeu resposta, sugerindo que essas portas estão filtradas por um firewall ou dispositivo de segurança.

Quando um programa como o Nmap realiza uma varredura, ele pode ser configurado para escanear um número específico de portas. Por padrão, o Nmap escaneia as **1000 portas mais comuns** (de 1 a 1024) se você não especificar um número diferente. Isso é feito para otimizar o tempo de varredura, focando nas portas que são mais frequentemente utilizadas por serviços conhecidos.

## `--open`​

A opção `--open`​ no Nmap é utilizada para filtrar os resultados da varredura, mostrando apenas as portas que estão abertas. Quando você usa essa opção, o Nmap irá ignorar as portas que estão fechadas ou filtradas e exibirá apenas aquelas que estão ativas e aceitando conexões.

Usando o comando `sudo nmap --open 192.168.1.0/24`​

```bash
~/Kali ❯ sudo nmap --open 192.168.1.0/24

Starting Nmap 7.95 ( https://nmap.org ) at 2024-11-08 18:31 -03
Nmap scan report for 192.168.1.1
Host is up (0.00026s latency).
Not shown: 998 filtered tcp ports (no-response)
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT     STATE SERVICE
80/tcp   open  http
1900/tcp open  upnp
MAC Address: 38:6B:1C:18:1F:38 (Shenzhen Mercury Communication Technologies)

Nmap done: 256 IP addresses (3 hosts up) scanned in 22.17 seconds
```

A saída indica que, na sub-rede 192.168.1.0/24, o Nmap encontrou 3 hosts ativos, dos quais um (192.168.1.1) teve duas portas abertas (80 e 1900). A maioria das portas (998) não respondeu e foi considerada filtrada, sugerindo a presença de um firewall ou dispositivo de segurança. A opção `--open`​ foi eficaz em filtrar os resultados para mostrar apenas as portas que estavam abertas.

Sobre o ip `192.168.1.1`​ as portas estão abertas:

* **Porta 80/tcp**: Estado "open" (aberta) e serviço "http".
* **Porta 1900/tcp**: Estado "open" (aberta) e serviço "upnp".

## `--packet-trace`​

A opção `--packet-trace`​ do Nmap é utilizada para exibir informações detalhadas sobre os pacotes que estão sendo enviados e recebidos durante a execução de um scan. Quando você ativa essa opção, o Nmap mostra um resumo de cada pacote que é enviado e recebido, incluindo detalhes como:

* O tipo de pacote (por exemplo, SYN, ACK, ICMP, etc.)
* O endereço IP de origem e destino
* O número da porta de origem e destino
* O estado do pacote (se foi enviado, recebido, etc.)
* Informações sobre o protocolo utilizado

O comando `sudo nmap --packet-trace 192.168.1.0/24`​ realiza uma varredura na rede local (sub-rede 192.168.1.0/24) e exibe informações detalhadas sobre os pacotes que estão sendo enviados e recebidos durante a varredura. O parâmetro `--packet-trace`​ faz com que o Nmap mostre cada pacote que é enviado e recebido, o que pode resultar em uma saída bastante extensa.

Aqui estão algumas dicas sobre como interpretar o resultado:

* **Identificação de Hosts**: O Nmap tentará identificar quais hosts estão ativos na rede. Você verá mensagens indicando se um host respondeu ou não.
* **Tipo de Pacote**: A saída mostrará o tipo de pacote que está sendo enviado (por exemplo, ICMP, TCP, UDP) e o estado de cada pacote (enviado, recebido, perdido).
* **Respostas de Hosts**: Para cada host que responde, você verá informações sobre o que foi recebido. Isso pode incluir informações sobre portas abertas, serviços em execução e sistemas operacionais.
* **Tempo de Resposta**: O tempo que leva para receber uma resposta de um host pode ser exibido, o que pode ajudar a identificar problemas de latência na rede.
* **Erros e Timeouts**: Se houver problemas de comunicação, como timeouts ou pacotes perdidos, isso será indicado na saída. Isso pode ser útil para diagnosticar problemas de rede.
* **Filtragem de Pacotes**: Se um firewall ou outro dispositivo de segurança estiver bloqueando pacotes, você poderá ver mensagens indicando que os pacotes foram filtrados.