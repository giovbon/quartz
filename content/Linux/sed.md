---
title: sed
tags:
  - devops
---
`sed`​ é uma ferramenta de linha de comando usada para editar e transformar texto em fluxos de dados, permitindo operações como substituição, inserção e exclusão de forma não interativa e eficiente, frequentemente utilizada em scripts para automatizar a manipulação de grandes volumes de dados.

Vamos considerar um arquivo chamado `usuarios.txt`​ com o seguinte conteúdo:

```
Nome,Idade,Cidade
Alice,30,Nova Iorque
Bob,25,Los Angeles
Carlos,35,São Paulo
Diana,28,Rio de Janeiro
```

Você pode usar `sed`​ para realizar essas operações da seguinte forma:

```bash
# 1. Substituir "São Paulo" por "Brasília"
sed -i 's/São Paulo/Brasília/g' usuarios.txt

# 2. Remover a linha que contém "Bob"
sed -i '/Bob/d' usuarios.txt

# 3. Adicionar um novo usuário ao final do arquivo
echo "Eve,22,Curitiba" | sed -i '$a\' usuarios.txt
```

* O `-i`​ faz a edição in-place, alterando o arquivo original.
* ​`s/`​ é um prefixo que indica que você está realizando uma operação de **substituição**
* ​`/g`​ significa "global". Isso indica que a substituição deve ser feita em  todas as ocorrências da string "São Paulo" em cada linha do arquivo `usuarios.txt`​, e não apenas na primeira ocorrência.
* ​`/d`​ indica que a linha deve ser deletada.
* ​`echo "Eve,22,Curitiba" | sed -i '$a\' usuarios.txt`​ adiciona uma nova linha com o usuário "Eve,22,Curitiba" ao final do arquivo. O `$a\`​ indica que a nova linha deve ser adicionada após a última linha do arquivo.

Após executar esses comandos, o conteúdo do arquivo `usuarios.txt`​ será:

```
Nome,Idade,Cidade
Alice,30,Nova Iorque
Carlos,35,Brasília
Diana,28,Rio de Janeiro
Eve,22,Curitiba
```

### Comandos Comuns​

No `sed`​, os padrões que você pode usar para indicar ações a serem realizadas em linhas específicas são geralmente precedidos por uma barra (`/`​). Aqui estão alguns dos comandos mais comuns que podem ser usados com o `sed`​:

* ​`d`​: Deletar linhas que correspondem ao padrão.
	* Exemplo: `sed '/padrão/d' arquivo.txt`​ (remove todas as linhas que contêm "padrão").
* ​`s`​: Substituir texto que corresponde ao padrão.
	* Exemplo: `sed 's/antigo/novo/g' arquivo.txt`​ (substitui "antigo" por "novo" em todas as ocorrências).
* ​`p`​: Imprimir linhas que correspondem ao padrão.
	* Exemplo: `sed -n '/padrão/p' arquivo.txt`​ (imprime apenas as linhas que contêm "padrão").
* ​`a`​: Adicionar uma linha após a linha que corresponde ao padrão.
	* Exemplo: `sed '/padrão/a nova linha' arquivo.txt`​ (adiciona "nova linha" após cada linha que contém "padrão").
* ​`i`​: Inserir uma linha antes da linha que corresponde ao padrão.
	* Exemplo: `sed '/padrão/i nova linha' arquivo.txt`​ (insere "nova linha" antes de cada linha que contém "padrão").
* ​`c`​: Substituir a linha que corresponde ao padrão por uma nova linha.
	* Exemplo: `sed '/padrão/c nova linha' arquivo.txt`​ (substitui a linha que contém "padrão" por "nova linha").
* ​`y`​: Transliterar caracteres (substituir um conjunto de caracteres por outro).
	* Exemplo: `sed 'y/abc/xyz/' arquivo.txt`​ (substitui 'a' por 'x', 'b' por 'y' e 'c' por 'z').
* ​`r`​: Ler e inserir o conteúdo de um arquivo após a linha que corresponde ao padrão.
	* Exemplo: `sed '/padrão/r outro_arquivo.txt' arquivo.txt`​ (insere o conteúdo de `outro_arquivo.txt`​ após cada linha que contém "padrão").
* ​`w`​: Gravar as linhas que correspondem ao padrão em um arquivo.
	* Exemplo: `sed '/padrão/w saida.txt' arquivo.txt`​ (grava as linhas que contêm "padrão" em `saida.txt`​).