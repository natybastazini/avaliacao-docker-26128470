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

A saída listou `50x.html` (página de erro padrão da imagem), `estilo.css` e `index.html`. No navegador
apareceu o meu nome e a minha matrícula no rodapé, em vez da página "Welcome to nginx!".

## Parte 2 · Docker Hub

3. Nome completo da imagem publicada e link público do repositório no Docker Hub.

A imagem publicada é `natybastazini/agrovale-portal:1.0-26128470`. O repositório público está em
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
| 1 | falta de `COPY` | O Dockerfile só tinha `FROM` e `WORKDIR`: a pasta `site/` com a página de manutenção nunca era copiada para dentro da imagem. | O build funcionou e o container ficou `Up`, sem erro no `docker logs`, mas em http://localhost:7070 apareceu a página padrão "Welcome to nginx!" em vez do "Voltamos em breve". | Adicionei `COPY site/ /usr/share/nginx/html/`, refiz o build e o run, e a página "Voltamos em breve" apareceu com o container ainda `Up`. |

6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?

O formato é `-p PORTA_DO_HOST:PORTA_DO_CONTAINER`. Em `-p 7042:80`, a porta 7042 do meu computador
aponta para a porta 80 dentro do container, que é onde o Nginx escuta. Em `-p 80:7042` seria o
contrário: a porta 80 do meu computador apontaria para a 7042 do container, onde o Nginx não está
escutando, e a página não abriria. A porta do container é o número depois dos dois pontos.

## Parte 4 · docker-compose.yml

7. No serviço `blog`, por que `WORDPRESS_DB_HOST` recebe `db` e não `localhost`?

Cada container tem a sua própria rede interna, então `localhost` dentro do container do blog aponta
para o próprio blog, onde não existe banco nenhum. Como o blog e o banco estão na mesma rede do
compose, o Docker resolve o nome do serviço `db` para o IP do container do MariaDB. Por isso o host
do banco é `db`.

8. Por que o serviço `db` não publica a porta 3306? Se precisar consultar o banco, como faz sem publicar
   a porta? Mostre o comando.

Não publiquei a 3306 para o banco não ficar exposto no meu computador e na rede: só o blog, que está
na mesma rede interna do compose, precisa falar com ele. Para consultar o banco sem publicar a porta,
entro no container do `db`:

## Parte 5 · Persistência

9. Quais comandos você usou para derrubar e subir a stack? Qual comando teria apagado o post que você criou,
   e por quê?

10. Código de conclusão impresso pelo verificador:

```
(cole aqui)
```