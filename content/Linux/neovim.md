---
title: neovim
fonte: https://www.youtube.com/watch?v=RZ4p-saaQkc
tags:
  - devops
---
## Começar usando

Trabalha com dois modos, modo normal, com comandos dados através de `:`​ e modo de inserção, apertando tecla `i`​, o que faz escrever os textos norma, a tecla `esc`​ sai do modo de inserção. `d`​ para deletar e `a`​ (append) de anexar

* ​`nvim arq.txt`​
* ​`i`​ ou `a`​ para modo inserir texto e `esc`​ pra sair
* ​`:w`​ pra salvar
* ​`:q`​ pra sair
* ​`:wq`​ salva e sai
* ​`:q!`​ fecha sem salvar (ignora mudanças no arquivo)

## Básico

* Diferenças entre `i`​ `a`​ e `o`​ / `I`​ `A`​ e `O`​
	* ​`i`​: Insere antes do cursor.
	* ​`a`​: Insere após o cursor.
	* ​`o`​: Insere em uma nova linha abaixo do cursor.
	* ​**​`I`​**​: Entra no modo de inserção no início da linha atual.
	* ​**​`A`​**​: Entra no modo de inserção no final da linha atual.
	* ​**​`O`​**​: Cria uma nova linha acima da linha atual e entra no modo de inserção.

* APAGAR
	* fora do modo inserção `dd`​ para apagar linha atual
	* `5dd`​ apagará as próximas 5 linhas a partir da linha atual.
	* entrar no modo visual pressionando `V`​ (maiusculo) e, em seguida, mover o cursor para selecionar várias linhas. Depois de selecionar as linhas, pressione `d`​ para apagá-las.
	* comando `:delete`​ ou `:d`​ seguido de um intervalo de linhas. Por exemplo, `:1,5d`​ apagará as linhas de 1 a 5.

## Recursos

  * para persistir qualquer configuração aplicada, incluir alterações em `nvim ~/.config/nvim/init.vim`​ (no arch é esse o caminho), não usar o `:`​ no arquivo de configuração
  * ​`:set number`​ ativa mostrar o número de linhas
  * ​`:set relavivenumber`​ mostra numero de linhas relativos a onde se está
  * ​`:set tabstop=4`​ define que uma tabulação equivale a 4 espaços.
  * ​`:set shiftwidth=4`​ define que a indentação automática usa 4 espaços.
  * ​`:set autoindent`​ ativa a indentação automática com base na linha anterior.
  * ​`:set mouse=a`​ habilita o uso do mouse em todas as modalidades do editor.
  * ​`:colorscheme + tab`​ abre várias opções visuais de cores
  * no modo norma inserir `5 🔼`​ ou `5 ⬇️`​ faz com que se mova 5 linhas, o mesmo funciona com `5 ➡️`​ ou `5 ⬅️`​
  * ​`j`​ sobe e `k`​ desce, `h`​ vai pra esquerda e `l`​ para a direita, serve pra aumentar a velocidade de movimentação de quem digita com os 10 dedos (tmb pode usar recurso onde `10+j`​ vai subir 10 linhas)

* [ ] DOING [ https://youtu.be/RZ4p-saaQkc?t=1467](https://youtu.be/RZ4p-saaQkc?t=1467)

‍