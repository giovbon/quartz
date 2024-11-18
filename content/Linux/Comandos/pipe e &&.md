---
title: "| e &&"
---
O pipe (`|`​) é usado para redirecionar a saída de um comando para a entrada de outro comando. Isso permite que você encadeie comandos, permitindo que a saída de um comando seja processada por outro comando. Exemplo: `ls -l | grep “txt”`​

Quando você usa `&&`​ entre comandos no Linux, está criando uma sequência de comandos que serão executados de forma condicional. O operador `&&`​ executa o próximo comando apenas se o comando anterior for bem-sucedido (ou seja, retornar um código de saída igual a 0). Exemplo: `mkdir nova_pasta && cd nova_pasta && touch arquivo.txt`​