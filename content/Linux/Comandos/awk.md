---
title: awk
---
`awk`​ é uma poderosa linguagem de programação e ferramenta de processamento de texto que é frequentemente utilizada em sistemas Unix e Linux. O `awk`​ é especialmente útil para manipulação e análise de dados em formato de texto, como arquivos CSV ou saídas de comandos. Ele permite que você processe e extraia informações de linhas de texto com base em padrões e condições.

No exemplo:

```bash
echo "O que é essa budega de AWK?" | awk '{print $7}'
```

* O comando `echo`​ imprime a string "O que é essa budega de AWK?".
* O símbolo `|`​ (pipe) redireciona a saída do comando `echo`​ para a entrada do comando `awk`​.
* O `awk`​ recebe a linha de texto e a processa. A expressão `{print $7}`​ instrui o `awk`​ a imprimir o sétimo campo da linha.

Por padrão, o `awk`​ divide a linha em campos usando espaços em branco como delimitadores. Portanto, a linha "O que é essa budega de AWK?" é dividida em campos da seguinte forma:

* ​`$1`​: O
* ​`$2`​: que
* ​`$3`​: é
* ​`$4`​: essa
* ​`$5`​: budega
* ​`$6`​: de
* ​`$7`​: AWK?

Assim, o comando `awk '{print $7}'`​ imprime o sétimo campo, que é "AWK?".
## printf

A função `printf`​ é uma função disponível no `awk`​. Ela é usada para formatar e imprimir saídas de maneira controlada, permitindo que você especifique como os dados devem ser apresentados.

A função `printf`​ tem a seguinte estrutura:

```bash
printf "formato", valor
```

* ​`"formato"`​: Esta é a string de formato que define como o valor deve ser apresentado. Os especificadores de formato (como `%f`​, `%d`​, `%s`​, etc.) são usados aqui para indicar o tipo de dado e como ele deve ser formatado.
* ​`valor`​: Este é o valor que será calculado ou extraído e que será impresso de acordo com o formato especificado.

```bash
printf "%.2f\n", 100 - $12
```

* ​`"%.2f\n"`​: Este é o formato de saída. O `%.2f`​ indica que o valor deve ser impresso como um número de ponto flutuante com duas casas decimais. O `\n`​ adiciona uma nova linha após a impressão do valor.
* ​`100 - $12`​: Este é o valor que está sendo calculado. Aqui, `$12`​ refere-se ao 12º campo da linha atual que está sendo processada pelo `awk`​. O resultado da expressão `100 - $12`​ é o valor que será formatado e impresso.

### Especificadores de Formato

1. ​`%d`​: Inteiro decimal (número inteiro).
2. ​`%u`​: Inteiro sem sinal (número inteiro não negativo).
3. ​`%f`​: Número de ponto flutuante (float).
4. ​`%.nf`​: Número de ponto flutuante com `n`​ casas decimais (por exemplo, `%.2f`​ para duas casas decimais).
5. ​`%s`​: String (sequência de caracteres).
6. ​`%c`​: Caractere único.
7. ​`%o`​: Inteiro em formato octal.
8. ​`%x`​: Inteiro em formato hexadecimal (letras minúsculas).
9. ​`%X`​: Inteiro em formato hexadecimal (letras maiúsculas).
10. ​`%p`​: Ponteiro (endereço de memória).
11. ​`%e`​: Notação científica (exponencial) em minúsculas.
12. ​`%E`​: Notação científica (exponencial) em maiúsculas.
13. ​`%g`​: Notação geral (usa `%f`​ ou `%e`​, dependendo do valor).
14. ​`%G`​: Notação geral em maiúsculas.

### Modificadores

Além dos especificadores, você pode usar modificadores para controlar a largura e a precisão da saída:

* **Largura**: Você pode especificar a largura mínima do campo. Por exemplo, `%5d`​ garante que o número inteiro tenha pelo menos 5 caracteres de largura.
* **Precisão**: Para números de ponto flutuante, você pode especificar a precisão. Por exemplo, `%.2f`​ imprime o número com duas casas decimais.
* **Sinal**: Para números, você pode usar `+`​ para sempre mostrar o sinal (positivo ou negativo). Por exemplo, `%+d`​.

Aqui estão alguns exemplos de como usar esses especificadores:

```bash
awk 'BEGIN {
    printf "Inteiro: %d\n", 42
    printf "Ponto flutuante: %.2f\n", 3.14159
    printf "String: %s\n", "Olá, mundo!"
    printf "Hexadecimal: %x\n", 255
}'
```

A saída será:

```
Inteiro: 42
Ponto flutuante: 3.14
String: Olá, mundo!
Hexadecimal: ff
```

Esses especificadores e modificadores permitem que você formate a saída de maneira flexível e precisa ao usar `printf`​ no `awk`​.