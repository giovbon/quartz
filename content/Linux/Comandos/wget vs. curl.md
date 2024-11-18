---
title: wget vs. curl
aliases:
  - wget
  - curl
---
* Use `wget`​ quando você precisa baixar arquivos ou sites inteiros de forma simples e rápida.
* Use `curl`​ quando você precisa de mais controle sobre a transferência de dados, especialmente ao interagir com APIs ou quando precisa de suporte a múltiplos protocolos.

Ambas as ferramentas são poderosas e úteis, dependendo do que você precisa fazer.

​`wget`​ e `curl`​ são duas ferramentas de linha de comando amplamente utilizadas no Linux para transferir dados pela internet, mas elas têm algumas diferenças importantes em termos de funcionalidade e uso.

​`wget`​

* **Objetivo Principal**: É projetado principalmente para baixar arquivos da web.
* **Recursividade**: Suporta downloads recursivos, o que significa que pode baixar não apenas um arquivo, mas também todos os arquivos de um site, seguindo links.
* **Interface Simples**: Geralmente, é mais fácil de usar para downloads simples, pois você pode simplesmente fornecer a URL e ele fará o download.
* **Suporte a Protocolos**: Suporta HTTP, HTTPS e FTP.
* **Continuação de Downloads**: Permite retomar downloads interrompidos com a opção `-c`​.

​`curl`​

* **Objetivo Principal**: É uma ferramenta mais versátil que pode enviar e receber dados usando uma variedade de protocolos.
* **Suporte a Vários Protocolos**: Suporta uma ampla gama de protocolos, incluindo HTTP, HTTPS, FTP, FTPS, SCP, SFTP, LDAP, e muito mais.
* **Interação com APIs**: É frequentemente usado para interagir com APIs RESTful, permitindo enviar dados (por exemplo, com métodos POST) e manipular cabeçalhos HTTP.
* **Saída Flexível**: Permite redirecionar a saída para um arquivo ou para a saída padrão, e você pode manipular a saída de várias maneiras.
* **Autenticação e Cookies**: Oferece suporte avançado para autenticação e manipulação de cookies.

## wget

Aqui estão alguns comandos básicos do `wget`​ que você pode usar para realizar downloads e outras operações:

```bash
# 1. Baixar um arquivo
# O comando abaixo utiliza o wget para baixar um arquivo do URL especificado e salvá-lo com o mesmo nome.
wget http://exemplo.com/arquivo.txt

# 2. Baixar um arquivo e salvar com um nome diferente
# Aqui, o wget baixa um arquivo do URL e o salva com um nome diferente, 'novo_nome.txt'.
wget -O novo_nome.txt http://exemplo.com/arquivo.txt

# 3. Baixar um arquivo em segundo plano
# Este comando permite que o wget baixe um arquivo em segundo plano, liberando o terminal para outras operações.
wget -b http://exemplo.com/arquivo.txt

# 4. Continuar um download interrompido
# O wget pode retomar um download que foi interrompido, utilizando a opção '-c'.
wget -c http://exemplo.com/arquivo.txt

# 5. Baixar um site inteiro (recursivamente)
# Este comando baixa um site inteiro de forma recursiva, sem subir para diretórios pai.
wget --recursive --no-parent http://exemplo.com/

# 6. Limitar a profundidade da recursão
# Aqui, o wget baixa um site de forma recursiva, mas limita a profundidade da recursão a 2 níveis.
wget --recursive --level=2 http://exemplo.com/

# 7. Baixar apenas arquivos de um tipo específico (por exemplo, arquivos .jpg)
# Este comando baixa apenas arquivos com a extensão .jpg de um site.
wget -r -A jpg http://exemplo.com/

# 8. Baixar arquivos de uma lista
# O wget pode ler URLs de um arquivo de texto e baixar todos os arquivos listados.
wget -i lista_de_urls.txt

# 9. Desativar a verificação de certificado SSL
# Este comando desativa a verificação de certificados SSL, útil para acessar sites com certificados inválidos.
wget --no-check-certificate https://exemplo.com/arquivo.txt

# 10. Mostrar o progresso do download
# O parâmetro '--progress=bar' exibe o progresso do download em forma de barra.
wget --progress=bar http://exemplo.com/arquivo.txt
```

Esses são apenas alguns exemplos de como usar o `wget`​. A ferramenta possui muitas outras opções e parâmetros que podem ser úteis dependendo do que você precisa fazer. Para mais informações, você pode consultar a página de manual do `wget`​ usando o comando `man wget`​ no terminal.

## curl

Aqui estão alguns comandos básicos do `curl`​ que você pode usar para transferir dados pela internet:

```bash
# 1. Baixar um arquivo
# O comando abaixo utiliza o curl para baixar um arquivo do URL especificado e salvá-lo com o mesmo nome.
curl -O http://exemplo.com/arquivo.txt

# 2. Baixar um arquivo e salvar com um nome diferente
# Aqui, o curl baixa um arquivo do URL e o salva com um nome diferente, 'novo_nome.txt'.
curl -o novo_nome.txt http://exemplo.com/arquivo.txt

# 3. Fazer uma requisição GET
# Este comando faz uma requisição GET para a API no URL especificado.
curl http://exemplo.com/api

# 4. Fazer uma requisição POST (enviando dados)
# O curl é usado para enviar uma requisição POST com dados no formato de chave-valor.
curl -X POST -d "param1=valor1&param2=valor2" http://exemplo.com/api

# 5. Enviar dados em formato JSON
# Este comando envia uma requisição POST com dados no formato JSON, especificando o cabeçalho 'Content-Type'.
curl -X POST -H "Content-Type: application/json" -d '{"param1":"valor1", "param2":"valor2"}' http://exemplo.com/api

# 6. Adicionar cabeçalhos personalizados
# Aqui, um cabeçalho de autorização é adicionado à requisição, utilizando um token Bearer.
curl -H "Authorization: Bearer seu_token" http://exemplo.com/api

# 7. Fazer uma requisição com autenticação básica
# Este comando utiliza autenticação básica, passando o usuário e a senha diretamente na requisição.
curl -u usuario:senha http://exemplo.com/api

# 8. Seguir redirecionamentos
# O curl segue redirecionamentos HTTP, permitindo que você acesse o destino final da URL.
curl -L http://exemplo.com/redirect

# 9. Desativar a verificação de certificado SSL
# Este comando desativa a verificação de certificados SSL, útil para acessar sites com certificados inválidos.
curl -k https://exemplo.com/arquivo.txt

# 10. Mostrar informações detalhadas sobre a requisição
# O parâmetro '-v' ativa o modo verbose, mostrando detalhes sobre a requisição e a resposta.
curl -v http://exemplo.com/api
```

Esses são apenas alguns exemplos de como usar o `curl`​. A ferramenta é muito poderosa e possui uma ampla gama de opções e parâmetros que podem ser úteis dependendo do que você precisa fazer. Para mais informações, você pode consultar a página de manual do `curl`​ usando o comando `man curl`​ no terminal.