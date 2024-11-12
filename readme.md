# Curso de Spring Boot Udemy

## Modulo 1 Introducao

### Aula 1

**Objetivo**
 - Profissionalizar o aluno na stack backend mais requisitada do java, partindo do zero ao Deploy em containers Cocker

**Porquê Spring Boot?**
 - Produtividade
 - Padronização
 - Fácil de colocar em produção
 - Poucas configurações

**Conteúdo**
 - Arquitetura detalhada, funcionamento do Framework, injeção de dependências, IOC.
 - APIs RESTFUL, modelagem e boas práticas.
 - Banco de dados e persistência com JPA.
 - Security, OAuth2, Login Social Google
 - Testes unitários e integração, Mocks, etc.
 - Build e Deploy em containers Docker.

**Requisitos**
 - [x] Java e orientação a objetos
 - [x] Desejável conhecimento em SQL
 - [x] Saber instalar ferramentas

 **Algumas das ferramentas e tecnologias utilizadas**
 - Java
 - PostgreSQL
 - Docker
 - IntelijIDE
 - Postman
 - Google Cloud

### Aula 2

**Recomendações**

- Link para repositório no [Github](https://github.com/cursodsousa/curso-spring-boot-especialista)
- Link para [documentação](https://whimsical.com/curso-sboot-expert-CKxrH3Bcd65xsfS6TibJqX)
- Slides: [O que é?](./docs/modulo1/spring-boot-expert+slides.pdf) e [Como funciona](./docs/modulo1/Spring+Boot+Expert+SLIDES.pdf)

### Aula 3

**Instalação da JDK**

Link para instalação: [JDK](https://www.oracle.com/br/java/technologies/downloads/#java21)

### Aula 4

**Instalação da IDE Intellij**

Link para instalação: [IDEA Intellij Comunity](https://www.jetbrains.com/idea/download/?section=windows)

### Aula 5

**Instalação do Postman**

Link para instalação: [POSTMAN](https://www.postman.com/downloads/)

### Aula 6

**Instalação do Docker**

Link para instalação no windows: [Docker](https://www.docker.com/products/docker-desktop/)

Link para instalação no Linux: [Docker](https://docs.docker.com/desktop/setup/install/linux/)

## Modulo 2 Primeiros passos

### Aula 7 Criando um projeto

O site [Spring Initialzr](https://start.spring.io) é uma boa alternativa para começar o projeto. Após nomear o projeto e seu Group, basta apenas definir as dependências que serão utilizadas.

### Aula 8 Conhecendo a estrutura do projeto e dicas Maven

**Anotações aprendidas**
 - @SpringBootApplication: Essa é a anotação que starta o projeto Spring

 ### Aula 9 Hello World com Spring Boot

**Anotações aprendidas**
- @RestController(): Transforma a classe em controlador Rest para que seja possível o mapeamento dos métodos.

 - @GetMapping(): Essa anotação quer dizer que estou mapeando o retorno do método para uma chamada *GET*. Ao mapear, eu passo entre parênteses o caminho da URL de minha preferência.
 