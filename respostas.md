# Respostas · Avaliação Prática de Docker · Cooperativa AgroVale (Turma A)

Nome: Natália Bastazini
Matrícula: 26128470
Usuário do GitHub: natybastazini
Usuário do Docker Hub: natybastazini

Responda com as suas palavras e com o que aconteceu na SUA máquina. Resposta curta e certa vale mais
do que texto longo copiado. Resposta que contradiz o seu próprio Dockerfile ou compose vale zero.

## Parte 1 · Dockerfile do portal

1. Qual imagem base você usou e qual o tamanho final da imagem do portal (saída de `docker images`)?

Usei a imagem oficial `nginx:1.27-alpine`, com tag fixa, porque `latest` não é aceita e a versão alpine
é bem mais leve. Na saída do `docker images`, a imagem `natybastazini/agrovale-portal:1.0-26128470`
ficou com 73.6MB.

2. Em qual pasta do container o Nginx procura os arquivos do site? Mostre o comando que você usou para
   conferir que o `index.html` está lá dentro.

O Nginx serve os arquivos da pasta `/usr/share/nginx/html`. Por isso o meu Dockerfile tem
`COPY html/ /usr/share/nginx/html/`. Para conferir que o `index.html` estava lá dentro, usei:

```
docker exec teste-portal ls /usr/share/nginx/html
```

A saída listou `50x.html`, `estilo.css` e `index.html`. No navegador
apareceu o meu nome e a minha matrícula no rodapé, em vez da página "Welcome to nginx!".

## Parte 2 · Docker Hub

3. Nome completo da imagem publicada e link público do repositório no Docker Hub.

natybastazini/agrovale-portal:1.0-26128470
https://hub.docker.com/r/natybastazini/agrovale-portal

4. Por que o `docker login` foi feito com um token de acesso e não com a senha da conta?

No meu caso o login foi feito com a senha da conta, e deu `Login Succeeded`. Mesmo assim, o próprio
Docker avisa no terminal que um token de acesso (PAT) pode ser usado no lugar, e o token é a opção
mais segura: dá para limitar as permissões (só leitura ou leitura e escrita), definir uma validade e
revogar o token sem precisar trocar a senha da conta. Se a senha vazar, o atacante tem acesso a toda
a conta; se um token vazar, basta apagá-lo. Em um computador de laboratório compartilhado, o token
seria a escolha mais prudente.

## Parte 3 · Página de manutenção

5. Preencha uma linha por defeito encontrado. Defeito inexistente listado aqui desconta pontos.

| # | Instrução | O que estava errado | O que você viu acontecer | Como corrigiu |
|---|---|---|---|---|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |

6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?

## Parte 4 · docker-compose.yml

7. No serviço `blog`, por que `WORDPRESS_DB_HOST` recebe `db` e não `localhost`?

8. Por que o serviço `db` não publica a porta 3306? Se precisar consultar o banco, como faz sem publicar
   a porta? Mostre o comando.

## Parte 5 · Persistência

9. Quais comandos você usou para derrubar e subir a stack? Qual comando teria apagado o post que você criou,
   e por quê?

10. Código de conclusão impresso pelo verificador:

```
(cole aqui)
```