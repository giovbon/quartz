---
title: Server Performance Stats
tags:
  - devops
  - prática
---
> [!info] Descrição
> Objetivo deste projeto é escrever um script para analisar as estatísticas de desempenho do servidor. Requisitos: Você precisa escrever um script chamado `server-stats.sh` que possa analisar as estatísticas básicas de desempenho do servidor. Você deve ser capaz de executar o script em qualquer servidor Linux e ele deve fornecer as seguintes estatísticas:
> - Uso total da CPU  
> - Uso total de memória (Livre vs Usado incluindo porcentagem)  
> - Uso total de disco (Livre vs Usado incluindo porcentagem)  
> - Top 5 processos por uso de CPU  
> - Top 5 processos por uso de memória
> 
> Objetivo adicional: Sinta-se à vontade para opcionalmente adicionar mais estatísticas, como versão do sistema operacional, tempo de atividade, média de carga, usuários conectados, tentativas de login com falha, etc.
> Depois de concluir este projeto, você terá um conhecimento básico sobre como analisar as estatísticas de desempenho do servidor, a fim de depurar e obter uma melhor compreensão do desempenho do servidor.

## Resolução

> [!tip] Veja +
> [[Bash]] [[mpstats]] [[pipe e &&]] [[awk]] [[sed]] 

```bash
#!/bin/bash

# Função para mostrar o uso total da CPU
function uso_cpu {
    echo "Uso total da CPU:"
    
    # Usando mpstat para obter o uso da CPU
    cpu_usage=$(mpstat 1 1 | awk '/all/ {printf "%.2f\n", 100 - $12}')
    
    # Substitui a vírgula por ponto, se necessário
    cpu_usage=$(echo $cpu_usage | sed 's/,/./')
    
    printf "CPU Usage: %.2f%%\n\n" "$cpu_usage"
}

# Função para mostrar o uso total de memória
function uso_memoria {
    echo "Uso total de memória:"
    free -h | awk 'NR==2{printf "Usado: %s, Livre: %s (%.2f%%)\n", $3, $7, $3*100/$2}'
    echo ""
}

# Função para mostrar o uso total de disco
function uso_disco {
    echo "Uso total de disco:"
    df -h --total | awk 'END{printf "Usado: %s, Livre: %s (%.2f%%)\n", $3, $4, $3*100/$2}'
    echo ""
}

# Função para mostrar os top 5 processos por uso de CPU
function top_processos_cpu {
    echo "Top 5 processos por uso de CPU:"
    ps -eo pid,comm,%cpu --sort=-%cpu | head -n 6
    echo ""
}

 # Função para mostrar os top 5 processos por uso de memória
function top_processos_memoria {
    echo "Top 5 processos por uso de memória:"
    ps -eo pid,comm,%mem --sort=-%mem | head -n 6
    echo ""
}

# Chamada das funções
uso_cpu
uso_memoria
uso_disco
top_processos_cpu
top_processos_memoria
```