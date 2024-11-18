---
title: ifconfig
tags:
  - cybersecurity
  - redes
---
# ifconfig

O comando `ifconfig`​ no Linux é utilizado para configurar e exibir informações sobre as interfaces de rede do sistema. Ele permite que os usuários visualizem detalhes como o endereço IP, máscara de sub-rede, endereço MAC e estatísticas de transmissão e recepção de dados para cada interface de rede.

![[Untitled-2024-11-13-2252-20241113225306-4zo46qg.png]]
Vale ressaltar que o `ifconfig`​ está sendo gradualmente substituído pelo comando `ip`​, que faz parte do pacote `iproute2`​ e oferece funcionalidades mais avançadas e uma sintaxe mais consistente. Por exemplo, para exibir informações de interfaces com o comando `ip`​, você usaria:

```bash
ip addr show
```

## Como obter o CIDR

Vamos explicar cada um desses termos:

1. **IP (Protocolo de Internet)** : O IP é um conjunto de regras que governam a forma como os dados são enviados e recebidos pela internet. Um endereço IP é um identificador único atribuído a cada dispositivo conectado a uma rede que utiliza o Protocolo de Internet. Existem duas versões principais de endereços IP: IPv4 (ex: 192.168.1.1) e IPv6 (ex: 2001:0db8:85a3:0000:0000:8a2e:0370:7334).
2. **Máscara de Sub-rede**: A máscara de sub-rede é um número que divide um endereço IP em duas partes: a parte da rede e a parte do host. Ela ajuda a determinar quais endereços IP pertencem à mesma rede. Por exemplo, uma máscara de sub-rede comum para uma rede local é 255.255.255.0, que indica que os primeiros três octetos do endereço IP representam a rede, enquanto o último octeto representa os hosts.
3. **CIDR (Classless Inter-Domain Routing)** : O CIDR é uma forma de alocação de endereços IP e roteamento que substitui o sistema de classes de endereços IP. Em vez de usar classes fixas (A, B, C), o CIDR permite que os endereços IP sejam agrupados em blocos de tamanhos variáveis. A notação CIDR é expressa como um endereço IP seguido de uma barra e um número (ex: 192.168.1.0/24), onde o número indica quantos bits são usados para a parte da rede.
4. **Sub-redes**: Sub-redes são divisões de uma rede maior em redes menores. Isso é feito para melhorar a eficiência do uso de endereços IP e para aumentar a segurança e o desempenho da rede. Cada sub-rede pode ter sua própria máscara de sub-rede, permitindo que um número específico de dispositivos se conecte a ela.

Esses conceitos são fundamentais para a configuração e gerenciamento de redes de computadores.

Com o comando `ifconf`​ é recebido: `inet 192.168.1.101 netmask 255.255.255.0`​, sendo o IP e a máscara de rede.

​​![[Untitled-2024-11-13-2253-20241113225416-23t7jml.png]]