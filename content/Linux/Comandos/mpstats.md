---
title: mpstats
---
```bash
~/Área de trabalho/TESTE01 ❯ mpstat
Linux 6.11.6-arch1-1 (giovani-a320mh) 	11/11/2024 	_x86_64_	(4 CPU)

13:31:44     CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest  %gnice   %idle
13:31:44     all   10,05    0,01    5,19    0,22    0,00    0,13    0,00    0,00    0,00   84,4
```

* **CPU**: Esta coluna indica qual CPU está sendo monitorada. Quando aparece "all", significa que os dados apresentados são uma média de todas as CPUs disponíveis no sistema.
*  **%usr**: Esta coluna mostra a porcentagem de tempo que a CPU está ocupada executando processos de usuário (não privilegiados). No seu caso, **10,05%**  do tempo da CPU está sendo utilizado para executar processos de usuário.
*  **%nice**: Esta coluna indica a porcentagem de tempo que a CPU está ocupada executando processos de usuário que têm prioridade "nice" (ou seja, processos que foram configurados para ter uma prioridade menor). No seu caso, **0,01%**  do tempo da CPU está sendo utilizado para esses processos.
*  **%sys**: Esta coluna mostra a porcentagem de tempo que a CPU está ocupada executando processos do sistema (privilegiados). No seu caso, **5,19%**  do tempo da CPU está sendo utilizado para executar processos do sistema.
*  **%iowait**: Esta coluna indica a porcentagem de tempo que a CPU está ociosa, mas aguardando operações de entrada/saída (I/O) serem concluídas. No seu caso, **0,22%**  do tempo da CPU está aguardando por operações de I/O.
*  **%irq**: Esta coluna mostra a porcentagem de tempo que a CPU está ocupada lidando com interrupções de hardware. No seu caso, **0,00%**  do tempo da CPU está sendo utilizado para lidar com interrupções.
*  **%soft**: Esta coluna indica a porcentagem de tempo que a CPU está ocupada lidando com interrupções de software. No seu caso, **0,13%**  do tempo da CPU está sendo utilizado para lidar com interrupções de software.
*  **%steal**: Esta coluna mostra a porcentagem de tempo que a CPU está "roubada" por máquinas virtuais (ou seja, tempo que a CPU poderia estar usando, mas está sendo usada por outra máquina virtual). No seu caso, **0,00%**  do tempo da CPU está sendo "roubado".
*  **%guest**: Esta coluna indica a porcentagem de tempo que a CPU está ocupada executando máquinas virtuais (guest). No seu caso, **0,00%**  do tempo da CPU está sendo utilizado para executar máquinas virtuais.
*  **%gnice**: Esta coluna mostra a porcentagem de tempo que a CPU está ocupada executando processos de máquinas virtuais que têm prioridade "nice". No seu caso, **0,00%**  do tempo da CPU está sendo utilizado para esses processos.
*  **%idle**: Esta coluna indica a porcentagem de tempo que a CPU está ociosa, ou seja, não está executando nenhum processo. No seu caso, **84,40%**  do tempo da CPU está ociosa.