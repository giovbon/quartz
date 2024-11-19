---
title: AJAX
---
[[Drawing 2024-11-19 11.01.10.excalidraw]]
![[Pasted image 20241119111855.png]]

{{AJAX}} envolve atualizações dinâmicas na página, como troca de imagens e conteúdos, **sem recarregar a interface inteira, mas sim apenas partes específicas**, utilizando para isso do HTML, JavaScript e DOM (*Document Object Model*).
<!--SR:!2024-11-23,4,270-->

Utilizando-se o {{AJAX}}, qualquer ação que requeira uma resposta do servidor ocorre de forma **assíncrona**, assim o usuário pode continuar interagindo com a interface da aplicação enquanto as requisições ao servidor estão sendo processadas, resultando em uma experiência mais fluida e responsiva.
<!--SR:!2024-11-23,4,270-->

O objeto Javascript {{`XMLHttpRequest`}} é uma parte fundamental da tecnologia AJAX (Asynchronous JavaScript and XML) pois permite a comunicação assíncrona com servidores web, é usado para enviar e receber dados de um servidor sem precisar recarregar a página.
<!--SR:!2024-11-20,1,230-->

O AJAX, que carrega (recuperação de dados de uma URL) e renderiza uma página utilizando recursos de scripts que estão rodando pelo lado do cliente (navegador), utiliza um objeto `XMLHttpRequest` e o método {{`open`}} para abrir um documento em uma linguagem de marcação, bem como para passar argumentos e capturar uma resposta.
