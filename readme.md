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

- @GetMapping(): Essa anotação quer dizer que estou mapeando o retorno do método para uma chamada _GET_. Ao mapear, eu passo entre parênteses o caminho da URL de minha preferência.

### Aula 10 Criando endpoints para recebimento dos produtos

**Novos conhecimentos**

- Model: É uma pasta para organizar a classe que representa uma entidade ou modelo. Ela define a estrutura dos dados que serão manipulados durante a aplicação.

- Controller: É uma classe que vai receber requisições REST.

**Anotações aprendidas**

- @RequestMapping(): Serve para passar a URL base do controller

- @RequestBody: Serve para colocar os dados JSON no objeto do controller

### Aula 11 Aprendendo a configurar conexao com banco de dados

**Properties**

No projeto Spring Boot há arquivos de configuração. Existe o .properties e o .yml. Neste curso prosseguiremos com o .yml para realizar as configurações de forma mais moderna.

Exemplo de "application.yml":

```
spring:
 application:
   name: Produtos API
 datasource:
   url: jdbc:h2:mem:produtos
   username: sa
   password: admin
 jpa:
   database-platform: org.hibernate.dialect.H2Dialect
 h2:
   console:
     enabled: true
     path: /h2-console
```

### Aula 12 Executando SQL ao subir aplicação

**Como será executado?**
O arquivo data.sql dentro da pasta resources será executado e criará a tabela do banco de dados.

Exemplo de "data.sql":

```
create table produto (
    id varchar(255) not null primary key,
    nome varchar(90) not null,
    descricao varchar(300),
    preco numeric(18, 2) not null
)
```

### Aula 13 Criando o mapeamento JPA para entidade Produto

O mapeamento JPA (Java Persistence API) serve para fornecer uma forma de mapear objetos Java para tabelas de um banco de dados relacional. O JPA é uma especificação que permite gerenciar a persistência de dados em uma aplicação Java, facilitando o armazenamento e a recuperação de objetos Java no banco de dados sem precisar escrever SQL manualmente.

**Anotações aprendidas**

- @Entity: é uma anotação para mapear a entidade para o banco de dados (tabela).
- @Column(): define as colunas da entidade (colunas). Caso o nome das variaveis se diferencie do nome no banco de dados, existe a possibilidade de mapear isso na chamada. Basta colocar (name = "nome_do_atributo").

- @Table: tem as mesmas usabilidades da anotação @Column, com a possibilidade de mapear a entidade, caso o nome da classe também esteja diferente do banco de dados. Basta colocar (name = "nome_da_tabela").

- @Id: a variavel que representar a primary key deverá conter essa anotação.

### Aula 14 Persistindo produtos no banco de dados

A criação de uma interface é necessária para definir um conjunto de métodos que uma classe deve implementar. No nosso caso, a interface a ser criada é a "ProdutoRepository", e ela vai encapsular as operações de persistência da classe Produto.

Para as operações de CRUD, a classe ProdutoRepository vai ficar assim:

```
package com.github.Matheuspgonsalves.produtosapi.repository;

import com.github.Matheuspgonsalves.produtosapi.model.Produto;
import org.springframework.data.jpa.repository.JpaRepository;

public interface ProdutoRepository extends JpaRepository<Produto, String> {
}

```

A interface deve ser intermediada dentro de controller. A função do controller em uma arquitetura de software é agir como intermediário entre a interface do usuário (ou outras interfaces de entrada, como APIs) e a camada de dados ou de lógica de negócios. O controller não é necessariamente a API que conecta diretamente ao banco de dados, mas ele coordena as operações entre a interface e o banco, muitas vezes utilizando serviços e repositórios para interagir com os dados.

Após mapear a interface na classe ProdutoController, obtemos o seguinte código:

```
package com.github.Matheuspgonsalves.produtosapi.controller;

import com.github.Matheuspgonsalves.produtosapi.model.Produto;
import com.github.Matheuspgonsalves.produtosapi.repository.ProdutoRepository;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.UUID;

@RestController
@RequestMapping("/produtos")
public class ProdutoController {

    private ProdutoRepository produtoRepository;

    public ProdutoController(ProdutoRepository produtoRepository) {
        this.produtoRepository = produtoRepository;
    }

    @PostMapping
    public Produto salvar(@RequestBody Produto produto){
        System.out.println("Produto recebido " + produto);

        var id = UUID.randomUUID().toString();
        produto.setId(id);

        produtoRepository.save(produto);
        return produto;
    }
}

```

### Aula 15 Obtendo os dados do produto

Já temos mapeado no controller a operação para salver os produto, utilizando o POST. Nesta aula, será mapeado o método para obter os produtos através da operação GET.

**Anotações aprendidas**
 - @PathVariable("id"): essa anotação permite que eu insira o id, ou elemento pra pesquisa em questão, pela url. Usando a anotação @GetMapping("/{id}"), eu posso definir o elemento que vai ser usado na url. O elemento dentro de chaves vai servir como parâmetro.

 Construimos o método "obterPorId", da seguinte forma:
 ````
 @GetMapping("/{id}")
    public Produto obterPorId(@PathVariable("id") String id){
//        Optional<Produto> produto = produtoRepository.findById(id);
//        return produto.isPresent() ? produto.get() : null;

        return produtoRepository.findById(id).orElse(null);
    }
 ````

 As linhas comentadas são outra forma de realizar o return da nossa busca.

 ### Aula 16 Deletando produtos

 Uma das etapas do CRUD é o delete de produtos, que será realizado nessa aula.

 **Anotações aprendidas**
 - @DeleteMapping("{id}): é a operação de exclusão de um item. Assim como o *GET*, é necessário passar o elemento por parâmetro na url e utilizar o @PathVariable("id"). 

Este é o codigo para deletar produtos:

````
@DeleteMapping("{id}")
    public void deletar(@PathVariable("id") String id){
        produtoRepository.deleteById(id) ;
    }
````

 ### Aula 17 Atualizando os dados de um produto

 Por último, será criado o método para atualizar o produto, para completar as operações do nosso CRUD.

 **Anotações aprendidas**
 - @PutMapping("{id}"): essa é a operação de atualização do produto. Assim como *GET* e *DELETE*, essa anotação vai receber um parâmetro para enviar no @PathVariable("id"). 

**Para conseguir ter uma maior velocidade no avanço do curso, estarei pausando as anotações e resumo das aulas por aqui, mas continuarei commitando os códigos das próximas aulas.**