## Sumário

- [O que é o HTTP?](#o-que-é-o-http)
- [A Web Segura - HTTPS](#a-web-segura---https)
- [Endereços sob seu domínio](#endereços-sob-seu-domínio)
- [O cliente pede o servidor responde](#o-cliente-pede-o-servidor-responde)
- [Depurando a requisição HTTP](#depurando-a-requisição-http)
- [Parâmetros da requisição](#parâmetros-da-requisição)
- [Serviços na Web com REST](#serviços-na-web-com-rest)
- [HTTP2 - Por uma Web mais eficiente](#http2---por-uma-web-mais-eficiente---dados-binários-gzip-ativo-e-tls)

## O que é o HTTP?
- Protocolo HTTP são Regras de Comunicação entre Cliente e Servidor
- Documentação: https://tools.ietf.org/html/rfc2616

## A Web Segura - HTTPS:
- HTTP Puro: Dados transportados enviados em texto puro, ficando visível para qualquer um que consiga interceptar nossa conexão.
- HTTP + SSL/TLS (Secure Sockets Layer/Transport Layer Security)
  - SSL/TLS - Envio de dados criptografados
- Identidade/Certificado Digital: Guarda a chave pública que irá criptografar os dados que serão enviados para o servidor, para que esse possa descriptografar a mensagem com uma chave privada e decifrar a informação. 
- Autoridade Certificadora: orgão que garante ao navegador e ao usuário que a identidade de um servidor (ex: Alura) é realmente válida. Portanto, é segura a troca de informações.
- Criptografia Assimétrica: Par de Chaves diferentes envolvidas. Processo lento. (ex: HTTPS)
- Criptografia Simétrica: usa a mesma chave para cifrar e decifrar dados. Processo mais rápido. (ex: porta na vida real, HTTPS)
  - HTTPS começa com criptografia assimétrica para depois mudar para criptografia simétrica. Essa chave simétrica será gerada no início da comunicação e será reaproveitada nas requisições seguintes. Autenticação/Autorização?

## Endereços sob seu domínio:
- Protocolo + Domínio (Nome fácil de ser gravado) + Porta + Recurso
- Raiz do domínio: COM, BR, ORG, NET ...
- HTTP://172.217.29.68 - Endereço IP do servidor
- DNS: Domain Name System - Serviço que resolve o nome do domínio e transforma em endereço IP
- http://www.google.com.br:80 - Porta 80 é a porta padrão
- https://www.google.com.br:443 - Porta 443 é a porta padrão
- Protocolo FTP - Porta 21
- Protocolo SSH - Porta 22
- https://www.alura.com.br/curso-online-html-e-css - Recurso é /curso-online-html-e-css
- Um recurso é algo concreto que queremos acessar
- URL e URN estão contidos em URI - basicamente a mesma coisa

 ## O cliente pede o servidor responde:
 - HTTP não guarda estado - Stateless
   - Como um usuário continua logado em um site se o protocolo não guarda estado? Servidor envia para o usuário um código que será enviado a toda requisição para simbolizar que o usuário está ativo
   - Conceito de Sessão introduzido - Cookie: Par de chave e valor
   - Browser consegue guardar Cookies - arquivo texto com conteúdo sobre o usuário

## Depurando a requisição HTTP:
- *Análise prática da ferramenta do desenvolvedor na aba Network*
- Introdução aos métodos HTTP - GET
- Cabeçalhos de resposta
- Introdução aos Status Code: 
  - 200 (OK);
  - 301 (MOVED PERMANENTLY);
  - 404 (NOT FOUND);
  - 500 (ERRO NO SERVIDOR)
- Em geral:
  - 2XX - Sucessful responses
  - 3XX - Redirection messages
  - 4XX - Client error responses
  - 5XX - Server error responses

## Parâmetros da requisição:
- Recurso + Parâmetros
  - Ex: https://cursos.alura.com.br/loginForm?urlAfterLogin=https://cursos.alura.com.br/dashboard 
  - É tipo um RedirectTo
- & - Símbolo usado para concatenar Parâmetros
- A URL não deve conter informações sigilosas, isto é, via query - Deve ser enviado no Header da requisição via método POST
- GET: Quando passamos os parâmetros da requisição na URL, estamos fazendo uso do método GET. O que é super útil quando precisamos repetir a requisição com os mesmos parâmetros
  - Ex: http://calculadordeimc.com.br/?peso=44&altura=1.50
- Utilizando o método GET, tanto o login quanto a senha seriam passados como parâmetro na URL, coisa que não queremos que aconteça. O método POST deixa os parâmetros no corpo da requisição, assim evita que informações importantes, como a senha, fiquem explícitas na URL.
- *Recapitulando:*
  - GET: Receber dados (params na URL)
  - POST: Submeter dados (params no corpo da requisição)
  - DELETE: Remover um recurso
  - PUT: Atualizar um recurso

## Serviços na Web com REST:

- *90% do mundo Web trabalha com GET e POST*
- *Comunicação do aplicativo AluraFood* - Envio de informações via XML/JSON/HTML
- Accept: apllication/json > maneira de indicar para o servidor o formato que quero receber a informação no app mobile
  - *Exemplos:* Accept: text/html, Accept: text/css, Accept: application/xml, Accept: application/json, Accept:image/jpeg e Accept: image/*
- O que é REST: REpresentational State Transfer
  - RECURSO (URI) + OPERAÇÕES(GET/POST/PUT/DELETE) + REPRESENTAÇÃO (JSON/XML/HTML)
  - Preferencia por substantivos na URI!
- Rest é um padrão arquitetural para comunicações entre aplicações
- Aproveita a estrutura que o HTTP proporciona
- Recursos são definidos via URI
- Cabeçalhos (Accept/Content-Type) para especificar a representação (JSON/XML)
- Para saber mais: tipos de dados
  - MIME types - tipo/subtipo
    - Exemplos de tipos: text, image, application, audio e video
    - Exemplos de subtipos:
      - text -> text/plain, text/html, text/css, text/javascript
      - image -> image/gif, image/png, image/jpeg
      - audio -> audio/midi, audio/mpeg, audio/webm, audio/ogg, audio/wav
      - video -> video/mp4
      - application -> application/xml,  application/pdf
      - *Entre outros formatos...*
## HTTP2 - Por uma Web mais eficiente - Dados binários, GZIP ativo e TLS:
- Requisição fora do browser - *curl*
- Conteúdo do Header sofreu algumas alterações
  - Corpo da resposta foi comprimido com GZIP
    - Porque? Intenção de diminuir a quantidade de dados enviados, diminuir o tráfego para suprir o uso de smartwatches por exemplo
- Cabeçalho não envia mais texto puro, envia binário
- HPACK: tem como função comprimir ainda mais o os headers, para tornar a requisição algo leve e aumentar a performance
- HTTP2 já traz uma camada de TLS - criptografia com TLS
- Headers/Cabeçalhos Stateful: não preciso mais repetir os headers que eu ja enviei em uma requisição passada caso seja os mesmos
- Server Push: 
  - HTTP1: Cada recurso novo é uma requisição nova que o cliente tem que fazer
  - HTTP2: Requisição de index.html já recebe todos os recursos, se antecipando e sem ter que fazer outra requisição
- Multiplexação:
  - Para realizar uma requisição é necessário que uma conexão TCP esteja ativa. No HTTP1 é possível que essa conexão fique aberta para que seja possível realizar requisições sem que haja necessidade de abrir uma nova conexão.
  - De 4 a 8 conexões simultâneas são permitidas no HTTP1. No HTTP2 é possível que sejam feitas requisições assíncronas, ou seja, é possível que eu faça outra requisição sem que a resposta da primeira tenha retornado, aumentando assim a performance. (Multiplexing)
- Em resumo: 
  - HTTP2 sofreu algumas melhorias, principalmente em performance
    - Header em binários e comprimidos(HPACK)
    - GZIP padrão na resposta
    - Multiplexing (Requisição e respostas são paralelas/assincronas)
    - Headers Stateful (Mandamos apenas os cabeçalhos que mudam)
    - Server-Push: ato do servidor antecipar dados que serão requisitados pelo browser em seguida.
