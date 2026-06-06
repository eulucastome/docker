# Docker e Docker Compose

## O que é Docker?

O Docker é um ambiente em nuvem onde desenvolvedores sobem suas aplicações para serem executadas sem ter que se preocupar com ter que configurar as dependências. Por exemplo: vários devs com diferentes versões do Python, PHP e .NET trabalham no mesmo projeto, ao tentar rodar iriam aparecer vários erros. Ao subir a aplicação para um Container, o Docker define as configurações que todos os devs devem trabalhar.

## Imagem vs Container

A imagem contém todas as instruções para montar um Container, com todo o binário, runtimes e outros objetos, mas é imutável, ou seja, uma vez escrito ele não muda e depende do kernel do SO host. Agora o container é o ambiente que já está pronto com tudo o necessário para rodar a aplicação, independentemente do host que está sendo usado (seria tipo uma máquina virtual rodando em nuvem) sem precisar ficar perdendo tempo configurando.

## O que é um Dockerfile?

O Dockerfile é o código que escrevemos manualmente para criar uma imagem, como se fosse uma receita de bolo, permitindo automatizar a implantação do software, aplicando as mudanças no SO e depois em um ambiente isolado, assim, personalizando a instalação de acordo com a necessidade, onde cada linha representa um comando que modifica o estado da imagem.

## O que é Docker Compose?

O Docker Compose é utilizado para facilitar o gerenciamento de múltiplos Containers em um único arquivo YAML com as instruções que são desejadas, ou seja, ele rege como uma banda deve se comportar durante uma música.

## Exemplo Prático

Imagine que tenhamos uma aplicação web em Node e um DB PostgreSQL. A estrutura inclui um .yml e um Dockerfile para a aplicação web.

O arquivo .yml pode ser feito assim:

text 
version: ‘3.8’ 
 
services: 
 web: 
   build: 
     context: ./web 
     Dockerfile: Dockerfile 
   image: minhaapp/web:latest 
   ports: 
     – “3000:3000” 
   depends_on: 
     – db 
 
 db: 
   image: postgres:13 
   environment: 
     POSTGRES_USER: user 
     POSTGRES_PASSWORD: senha 
     POSTGRES_DB: minhaappdb 
   ports: 
     – “5432:5432” 
Temos o Dockerfile que define como a imagem da aplicação será construída: 
text
FROM node:16-alpine 
WORKDIR /app 
COPY package*.json ./ 
RUN npm install 
COPY . . 
EXPOSE 3000 
CMD [“npm”, “start”] 
O Docker Compose é responsável por construir a imagem da aplicação web seguindo as instruções do Dockerfile, sem precisar reconstruir o SQL.

## Referências

https://www.reddit.com/r/brdev/comments/1kz2vwz/qual_o_real_prop%C3%B3sito_do_docker/

https://circleci.com/blog/docker-image-vs-container/

https://aws.amazon.com/pt/compare/the-difference-between-docker-images-and-containers/

https://www.alura.com.br/artigos/desvendando-o-dockerfile

https://www.mundodocker.com.br/o-que-e-dockerfile/

https://serverspace.com.br/support/help/o-que-e-um-dockerfile-guia-passo-a-passo-para-escrever-um-dockerfile/

https://blog.4linux.com.br/docker-compose-explicado/

https://imasters.com.br/banco-de-dados/docker-compose-o-que-e-para-que-serve-o-que-come

https://www.mundodocker.com.br/docker-compose-build-guia-completo-com-exemplos/ 
