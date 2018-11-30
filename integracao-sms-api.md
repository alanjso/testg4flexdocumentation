<!-- TITLE: Integracao Sms Api -->
<!-- SUBTITLE: A quick summary of Integracao Sms Api -->

# Integração SMS API v1.0
## Introdução
A integração com o sistema de envio de SMS deve ser realizado através de requisições HTTP a determinados endpoints utlizando alguns parâmetros e recebendo em resposta um conteúdo formatado de sucesso ou de falha.

## Login
Efetua autentcação na plataforma de integração. É enviado um POST com “login” e “password” e como resposta é retornado um token. Esse token é uma chave única que deverá ser utlizada em TODAS as requisições subsequentes sendo enviado no header das mesmas, do contrário o acesso será negado. O token gerado será o mesmo para TODAS as requisições.

|    Nome        |    Tipo      |    Obrigatório    |    Observação                 |   |
|----------------|--------------|-------------------|-------------------------------|---|
|    login       |    String    |    Sim            |    Login cedido pela G4fex    |   |
|    password    |    String    |    Sim            |    Senha cedida pela G4fex    |   |
|                |              |                   |                               |   |