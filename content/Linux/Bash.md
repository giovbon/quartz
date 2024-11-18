---
title: Bash Script
fonte: https://www.youtube.com/watch?v=tK9Oc6AEnR4
tags:
  - devops
---
> [!info] Links Bash
> - [Bash Cheat Sheet & Quick Reference](https://cheatsheets.zip/bash)

> [!tip] Veja +
> 
> [[awk]] [[sed]]

![[neovim#Começar usando]]
## Variáveis

- definição com maiúsculas e `=` 
	- `VARIAVEL=`
- `read` define de acordo com o que for digitado
- uso dessas variáveis com `$` na frente.


```bash
VARIAVEL=Eita_porra
echo $VARIAVEL

echo Qual o seu nome?
read PRIMEIRO_NOME
echo E qual o segundo?
read SOBRENOME

echo E ai $PRIMEIRO_NOME $SOBRENOME
```

## Permissões

Dar permissão com `u+x`​ de execução apenas para dono do arquivo: `chmod u+x script.sh`​  
argumento posicional

```bash
#!/bin/bash

echo E aew manolo $1 $2
```

- usar isso no comando para capturar os argumentos: `./script.sh arg1 arg2`​

## Operadores de Redirecionamento

- **piping (tubulação)**  `|`​ envia a saída de um comando para o outro
- Envia a saída de um comando para um arquivo `>`​ (sobrescreve) ou `>>`​ (append)  

```bash
wc -w < teste.txt

wc -w <<< "Hello there here"

cat << EOF
...várias linhas de texto com Enter ...
EOF
```

 `wc -w`​ na linha de comando do Linux é utilizado para contar o número de palavras em um arquivo ou na entrada padrão. O wc significa "word count" (contagem de palavras), e a opção -w especifica que você deseja contar apenas as palavras.
## Return Code

```bash
[ 1 = 0 ]
echo $? # 1
```

- Quando você digita `[ 1 = 0 ]`​ em um terminal Unix/Linux, você está usando um comando de teste que verifica se a condição entre os colchetes é verdadeira ou falsa. Neste caso, você está perguntando se `1`​ é igual a `0`​, o que é falso.  
- Após isso, ao digitar `echo $?`​, você está pedindo para exibir o código de saída do último comando executado. No contexto do shell, um código de saída de `0`​ geralmente indica que o comando foi bem-sucedido (ou seja, a condição era verdadeira), enquanto um código diferente de `0`​ indica que houve uma falha (ou seja, a condição era falsa).  
- Portanto, ao executar `[ 1 = 0 ]`​, o resultado será falso, e ao executar `echo $?`​, você verá `1`​, que é o código de saída indicando que a condição não foi satisfeita.

## Condicionais

```bash
#!/bin/bash
if [ ${1,,} = "herbert" ]; then
    echo "Oh, you're the boss here. Welcome!"
elif [ ${1,,} = "help" ]; then
    echo "Just enter your username, duh!"
else
    echo "I don't know who you are. But you're not the boss of me!"
fi
```

- **​`${1,,}`​** ​: Esta é uma forma de expansão de parâmetro no Bash que converte o valor de `$1`​ para minúsculas (mais especificamente `,,`​) envolve o uso de argumento posicional

## Case Statements

O `case`​ é uma estrutura de controle que permite comparar uma variável com diferentes padrões.

```bash
case ${1,,} in
    herbert | administrator)
        echo "Hello, you're the boss here!"
        ;;
    help)
        echo "Just enter your username!"
        ;;
    *)
        echo "Hello there. You're not the boss of me. Enter a valid username!"
        ;;
esac
```

- **​`${1,,}`​** ​: Esta é uma forma de expansão de parâmetro no Bash que converte o valor de `$1`​ para minúsculas (mais especificamente `,,`​) envolve o uso de argumento posicional

##  Arrays

```bash
MEU_ARRAY=(um dois tre quatro cinco)

echo $MEU_ARRAY # um
echo ${MEU_ARRAY[@]} # um dois tre quatro cinco
echo ${MEU_ARRAY[1]} # dois
```
## `for`

```bash
${MEU_ARRAY[@]}; do echo -n $item | wc -c; done
2
4
3
6
5
```

* ​**​`do`​**​: Indica o início do bloco de comandos que será executado para cada item do array.
* ​**​`echo -n $item`​**​: O comando `echo`​ imprime o valor da variável `item`​ (que contém o elemento atual do array). A opção `-n`​ faz com que `echo`​ não adicione uma nova linha ao final da saída, ou seja, a saída será apenas o conteúdo do item.
* ​ **​`| wc -c`​**​: O símbolo `|`​ é um pipe que redireciona a saída do comando anterior (`echo -n $item`​) para o comando `wc`​. O comando `wc`​ (word count) com a opção `-c`​ conta o número de caracteres na entrada. Portanto, ele contará quantos caracteres estão no item atual.
* ​**​`done`​**​: Indica o fim do bloco de comandos do loop.

## Funções

```bash
showuptime() {
    local up=$(uptime -p | cut -c 4-)
    local since=$(uptime -s)
    cat << EOF
Esta máquina está ativa há $up
Ela está em funcionamento desde $since
EOF
}

showuptime #chama a função

❯ ./teste.sh
Esta máquina está ativa há 41 minutes
Ela está em funcionamento desde 2024-11-14 09:53:50
```

* **Obtenção do Tempo de Atividade**:
	* ​`uptime -p`​: Este comando retorna o tempo de atividade da máquina em um formato legível, como "up 5 hours, 10 minutes".
	* ​`cut -c 4-`​: Este comando remove os primeiros três caracteres da saída (que geralmente são "up "), deixando apenas o tempo de atividade.
	* O resultado é armazenado na variável `up`​.

* **Obtenção da Data/Hora de Início**:
	* ​`uptime -s`​: Este comando retorna a data e hora exatas em que a máquina foi iniciada pela última vez.
	* O resultado é armazenado na variável `since`​.

* sobre o uso de `local`​ antes da definição de variáveis
	* O uso da palavra-chave `local`​ em um script de shell (como o Bash) é utilizado para declarar variáveis que têm um escopo limitado à função em que são definidas. Isso significa que as variáveis declaradas como `local`​ não estarão disponíveis fora da função, evitando assim conflitos com variáveis de mesmo nome que possam existir em um escopo mais amplo (como variáveis globais).
	* No seu exemplo, as variáveis `up`​ e `since`​ são declaradas como locais dentro da função `showuptime()`​. Isso garante que, ao chamar essa função, as variáveis `up`​ e `since`​ não afetarão ou serão afetadas por variáveis com os mesmos nomes que possam existir fora da função.

Uso de parâmetros posicionais em função com `$1`
​
```bash
showname(){
	echo Olá $1
}
showname GIOBON


❯ ./teste.sh
Olá GIOBON
```
