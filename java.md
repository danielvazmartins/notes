# Java

## Maven
Gerenciador de projetos Java. Se baseia no arquivo de configuração pom.xml (Project Object Model) para baixar as dependências, gerar builds, etc.

```bash
# Ver a versão do Maven
mvn -v

# Gerar um projeto (deixar todos valores default)
mvn archetype:generate

# Compilar o projeto
mvn build

# Gerar o pacote jar
mvn package

# Executar o pacote jar
java -cp target/my-app-1.0-SNAPSHOT.jar com.mycompany.app.App
```

## SpringBoot

[Spring Initializr](https://start.spring.io/) - Gerar projeto SprintBook com as dependências selecionadas. Ou utilizar o Initializr através do VSCode com o atalho CTRL+SHIT+P e escolher a "Spring Initializr: Create a Maven Project..."

## Dependências

[Spring Web](https://spring.io/guides/gs/rest-service/) - Criar aplicações RESTful. Utiliza o Apache Tomcat embutido para rodar a aplicação

[Spring Boot Dev Tools]() - Detecta alterações no projeto e faz o reload automaticamente

[Spring Data JPA]() - Java Persistence API. Faz o acesso ao banco de dados, utilizando métodos facilitadores, usando o Spring Data e o Hibernate

[Lombok](https://projectlombok.org/) - Dependência para criar automaticamente os getters e setters

[H2 Database](https://www.h2database.com/) - Banco de dados em memória que não precisa de instalação, pode ser utilizado como uma dependência do projeto
 - Application Properties
 ```properties
 spring.datasource.url=jdbc:h2:mem:curso_dio
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=admin
spring.datasource.password=admin123
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.h2.console.enabled=true
 ```
 - Console `http://localhost:8080/h2-console`
