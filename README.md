## Anotações do Curso:

# O que é o HTTP?
- Protocolo HTTP são Regras de Comunicação entre Cliente e Servidor
- Documentação: https://tools.ietf.org/html/rfc2616

# A Web Segura - HTTPS:
- HTTP Puro: Dados transportados enviados em texto puro, ficando visível para qualquer um que consiga interceptar nossa conexão.
- HTTP + SSL/TLS (Secure Sockets Layer/Transport Layer Security)
  - SSL/TLS - Envio de dados criptografados
- Identidade/Certificado Digital: Guarda a chave pública que irá criptografar os dados que serão enviados para o servidor, para que esse possa descriptografar a mensagem com uma chave privada e decifrar a informação. 
- Autoridade Certificadora: orgão que garante ao navegador e ao usuário que a identidade de um servidor (ex: Alura) é realmente válida. Portanto, é segura a troca de informações.
- Criptografia Assimétrica: Par de Chaves diferentes envolvidas. Processo lento. (ex: HTTPS)
- Criptografia Simétrica: usa a mesma chave para cifrar e decifrar dados. Processo mais rápido. (ex: porta na vida real, HTTPS)
  - HTTPS começa com criptografia assimétrica para depois mudar para criptografia simétrica. Essa chave simétrica será gerada no início da comunicação e será reaproveitada nas requisições seguintes. Autenticação/Autorização?
  