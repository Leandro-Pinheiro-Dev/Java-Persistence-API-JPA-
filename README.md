
# 💾 Projeto Java com JPA e Hibernate — Nivelamento

Este projeto foi desenvolvido com o objetivo de nivelar o conhecimento prático em **JPA (Java Persistence API)** e **Hibernate**, demonstrando como configurar e utilizar o mapeamento objeto-relacional (ORM) em uma aplicação Java com persistência de dados em **MySQL**.

---

## ✅ Objetivos do projeto

- Demonstrar o uso de **JPA** com implementação **Hibernate**
- Realizar o **mapeamento objeto-relacional** com anotações
- Usar **Maven** para gerenciar dependências
- Persistir entidades em um banco MySQL
- Exibir dados de objetos Java armazenados no banco

---

## 🛠️ Tecnologias e Ferramentas

- Java 17+
- Maven
- Hibernate ORM 5.4
- JPA (javax.persistence)
- MySQL
- XAMPP (Apache + MySQL)
- Eclipse / STS (Spring Tool Suite)
- Git

---

## 🧱 Estrutura do Projeto

```
src/
├── dominio/
│   └── Pessoa.java       # Classe da entidade com mapeamento JPA
├── aplicacao/
│   └── Programa.java     # Classe principal com testes e inserção
└── resources/
    └── META-INF/
        └── persistence.xml  # Configuração JPA/Hibernate
```

---

## ⚙️ Passo a passo: Como configurar

### 🔹 1. Criação do banco de dados MySQL

1. Instale o **XAMPP**
2. Inicie **Apache** e **MySQL**
3. Acesse [http://localhost/phpmyadmin](http://localhost/phpmyadmin)
4. Crie o banco:

```sql
CREATE DATABASE aulajpa;
```

---

### 🔹 2. Criar o projeto Maven

No Eclipse/STS:

```
File → New → Other → Maven Project
```

- Marque: **Create a simple project**
- Group ID: `com.educandoweb`
- Artifact ID: `aulajpamaven`

---

### 🔹 3. Atualizar versão Java no `pom.xml`

```xml
<properties>
  <maven.compiler.source>17</maven.compiler.source>
  <maven.compiler.target>17</maven.compiler.target>
</properties>
```

---

### 🔹 4. Adicionar dependências Maven

```xml
<dependencies>
  <dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-core</artifactId>
    <version>5.4.12.Final</version>
  </dependency>

  <dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-entitymanager</artifactId>
    <version>5.4.12.Final</version>
  </dependency>

  <dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.19</version>
  </dependency>
</dependencies>
```

---

### 🔹 5. Criar e configurar o `persistence.xml`

Local: `src/main/resources/META-INF/persistence.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<persistence xmlns="http://xmlns.jcp.org/xml/ns/persistence"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence
  http://xmlns.jcp.org/xml/ns/persistence/persistence_2_1.xsd" version="2.1">

  <persistence-unit name="exemplo-jpa" transaction-type="RESOURCE_LOCAL">
    <properties>
      <property name="javax.persistence.jdbc.url" value="jdbc:mysql://localhost:3306/aulajpa?useSSL=false&amp;serverTimezone=UTC" />
      <property name="javax.persistence.jdbc.driver" value="com.mysql.cj.jdbc.Driver" />
      <property name="javax.persistence.jdbc.user" value="root" />
      <property name="javax.persistence.jdbc.password" value="" />

      <property name="hibernate.hbm2ddl.auto" value="update" />
      <property name="hibernate.dialect" value="org.hibernate.dialect.MySQL8Dialect" />
      <property name="hibernate.show_sql" value="true" />
    </properties>
  </persistence-unit>
</persistence>
```

---

## 🧩 Classe de Entidade

```java
package dominio;

import jakarta.persistence.*;
import java.io.Serializable;

@Entity
public class Pessoa implements Serializable {

  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  private Integer id;
  private String nome;
  private String email;

  // Construtores, Getters, Setters, toString()
}
```

---

## 🚀 Classe Principal (Programa.java)

```java
package aplicacao;

import dominio.Pessoa;
import jakarta.persistence.EntityManager;
import jakarta.persistence.EntityManagerFactory;
import jakarta.persistence.Persistence;

public class Programa {
  public static void main(String[] args) {

    Pessoa p1 = new Pessoa(null, "Carlos da Silva", "carlos@gmail.com");
    Pessoa p2 = new Pessoa(null, "Joaquim Torres", "joaquim@gmail.com");
    Pessoa p3 = new Pessoa(null, "Ana Maria", "ana@gmail.com");

    EntityManagerFactory emf = Persistence.createEntityManagerFactory("exemplo-jpa");
    EntityManager em = emf.createEntityManager();

    em.getTransaction().begin();
    em.persist(p1);
    em.persist(p2);
    em.persist(p3);
    em.getTransaction().commit();

    System.out.println("Dados inseridos com sucesso!");
    em.close();
    emf.close();
  }
}
```

---

## ✅ Funcionalidades demonstradas

- [x] Criação de entidade mapeada com JPA
- [x] Uso do Hibernate como provedor de persistência
- [x] Integração com banco MySQL
- [x] Inserção de dados com `EntityManager`

---

## 📌 Observações

- Certifique-se de que o **MySQL está em execução** e que a base `aulajpa` foi criada.
- Verifique o driver JDBC usado no `persistence.xml`: `com.mysql.cj.jdbc.Driver`
- A propriedade `hibernate.hbm2ddl.auto=update` permite que o Hibernate **crie ou atualize** a tabela automaticamente com base na entidade.

---

