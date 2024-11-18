---
title: Python
tags:
  - devops
  - linguagem
---
## Ambientes virtuais

* O `pip`​ é o gerenciador de pacotes oficial do Python, utilizado para instalar, atualizar e gerenciar pacotes (bibliotecas) no ambiente Python. Com ele, você pode adicionar ferramentas e bibliotecas específicas para o seu projeto, como frameworks web, bibliotecas de análise de dados, e outras. O `pip`​ e ambientes virtuais são conceitos essenciais em Python que ajudam a gerenciar pacotes e dependências de projetos de maneira organizada e isolada.
* Comandos básicos do pip:
	* ​`pip install <nome_do_pacote></nome_do_pacote>`​: instala um pacote específico.
	* ​`pip uninstall <nome_do_pacote></nome_do_pacote>`​: remove um pacote específico.
	* ​`pip list`​: lista todos os pacotes instalados no ambiente atual.

* Ambientes virtuais em Python são espaços isolados criados para cada projeto, onde você pode instalar pacotes específicos sem afetar outros projetos ou o sistema principal. Isso é especialmente útil para evitar conflitos entre versões de pacotes e manter seu projeto mais organizado.
	* No terminal, navegue até a pasta do projeto.
	* ​`python -m venv nome_do_ambiente`​ substitua `nome_do_ambiente`​ por um nome desejado, como `venv`​ ou `env`​.
	* ative o ambiente `source nome_do_ambiente/bin/activate`​
	* Depois de ativar o ambiente, use `pip install <nome_do_pacote></nome_do_pacote>`​ para instalar pacotes apenas dentro deste ambiente. Esses pacotes não afetam o ambiente global.
	* Para sair do ambiente virtual, basta usar `deactivate`​