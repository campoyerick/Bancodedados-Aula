<p align="center">
    <img src="https://img.shields.io/badge/Language-Java-brightgreen" alt="Language: Java">
    <img src="https://img.shields.io/badge/Database-MySQL-blue" alt="Database: MySQL">
</p>

<p align="center">
  <img src="https://github.com/campoyerick/Bancodedados-Aula/blob/main/mysql.jpg?raw=true"></img>
    <b>Desenvolva habilidades avançadas em MySQL para seus projetos Java Bukkit.</b>
</p>

## 📘 Introdução

Bem-vindo ao repositório que irá acelerar seu aprendizado sobre o uso do MySQL em seus projetos Java Bukkit. Este guia foi criado com o objetivo de proporcionar uma introdução rápida e acessível para desenvolvedores que desejam incorporar bancos de dados relacionais em seus plugins Bukkit.

### 💡 Por que usar MySQL em projetos Bukkit?

Ao desenvolver plugins para servidores Minecraft baseados em Bukkit, é comum a necessidade de armazenar e recuperar dados de forma eficiente. Utilizar bancos de dados relacionais, como o MySQL, permite uma organização estruturada dos dados, facilitando consultas e otimizando o desempenho do seu plugin.

### 🚀 Como utilizar este guia?

Este guia é dividido em seções simples e diretas, projetadas para levar você de iniciante a proficiente no uso do MySQL e SQL em Java Bukkit. Siga os passos, experimente os exemplos e sinta-se à vontade para adaptar as instruções conforme necessário para atender às necessidades específicas do seu projeto.

> [!NOTE]
>  Este guia assume que você já possui conhecimento básico de Java e Bukkit. Se necessário, consulte a [documentação oficial do Bukkit](https://bukkit.gamepedia.com/Main_Page) para obter mais informações.

## 🛠️ Pré-requisitos

Antes de começar, certifique-se de ter o seguinte instalado:

- [Java Development Kit (JDK)](https://www.oracle.com/java/technologies/javase-downloads.html)
- [Bukkit API](https://hub.spigotmc.org/javadocs/spigot/)
- [MySQL Server](https://dev.mysql.com/downloads/installer/)

## 📖 Conteúdo

1. [Configuração do Ambiente](#1-configuração-do-ambiente)
2. [Conexão com o MySQL](#2-conexão-com-o-mysql)
3. [Operações Básicas do SQL](#3-operações-básicas-do-sql)
4. [Exemplos Práticos](#4-exemplos-práticos)
5. [Considerações Finais](#5-considerações-finais)

---

### 1. Configuração do Ambiente

Antes de começar a trabalhar com MySQL e SQL em Java Bukkit, é essencial configurar o ambiente corretamente. Certifique-se de seguir estes passos:

#### 1.1. Instalação do JDK (Java Development Kit)

Certifique-se de ter o JDK instalado em seu sistema. Você pode baixar a versão mais recente do JDK [aqui](https://www.oracle.com/java/technologies/javase-downloads.html). Siga as instruções de instalação fornecidas no site oficial.

#### 1.2. Configuração do Projeto Bukkit

- Crie um novo projeto Bukkit em seu ambiente de desenvolvimento integrado (IDE) preferido.
- Adicione a biblioteca Bukkit ao seu projeto para acessar as funcionalidades do Bukkit API. Você pode encontrar as bibliotecas no site oficial do [Bukkit](https://hub.spigotmc.org/javadocs/spigot/).

#### 1.3. Instalação do MySQL Server

Para armazenar e gerenciar dados de forma eficiente, você precisará de um servidor MySQL. Siga estas etapas:

- Baixe e instale o [MySQL Server](https://dev.mysql.com/downloads/installer/).
- Durante a instalação, defina a senha do usuário "root" e anote-a para referência futura.

#### 1.4. Adição do Driver JDBC ao Projeto

Para permitir que seu projeto Java Bukkit se comunique com o MySQL, adicione o driver JDBC ao seu projeto. Você pode baixar o driver JDBC para MySQL no [site oficial da MySQL](https://dev.mysql.com/downloads/connector/j/).

Após o download, adicione o arquivo JAR do driver ao seu projeto.

**Exemplo de adição do driver JDBC no Maven:**

```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.33</version>
</dependency>
```

**Exemplo de adição do driver JDBC no Gradle:**

```groovy
implementation 'mysql:mysql-connector-java:8.0.33'
```

#### 1.5. Configuração do Banco de Dados MySQL

- Inicie o MySQL Server.
- Use um cliente MySQL, como o MySQL Workbench, para criar um novo banco de dados e tabelas conforme necessário para o seu projeto.

Com a configuração do ambiente concluída, você está pronto para começar a conectar seu plugin Bukkit ao MySQL. Continue para a próxima seção para aprender como estabelecer a conexão com o MySQL em seu código Java.

--- 

### 2. Conexão com o MySQL

Nesta seção, você aprenderá a estabelecer uma conexão com o MySQL em seu plugin Bukkit usando Java. Siga os passos abaixo:

#### 2.1. Importação de Pacotes

No início do seu arquivo Java, importe os pacotes necessários para lidar com a conexão JDBC. Adicione as seguintes linhas:

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
```

#### 2.2. Variáveis de Configuração

Declare variáveis para armazenar as informações de conexão, como URL do banco de dados, nome de usuário e senha. Substitua os valores de exemplo pelos seus próprios:

```java
String jdbcUrl = "jdbc:mysql://localhost:3306/nome_do_seu_banco";
String username = "seu_usuario";
String password = "sua_senha";
```

Certifique-se de substituir "nome_do_seu_banco", "seu_usuario" e "sua_senha" pelos valores apropriados.

#### 2.3. Estabelecimento da Conexão

Crie um método para estabelecer a conexão com o MySQL. Você pode fazer isso da seguinte maneira:

```java
public Connection conectarAoMySQL() {
    try {
        return DriverManager.getConnection(jdbcUrl, username, password);
    } catch (SQLException e) {
        e.printStackTrace();
        return null;
    }
}
```

Este método retorna uma instância de `Connection` que você pode usar para executar consultas SQL.

#### 2.4. Teste da Conexão

Para garantir que a conexão esteja funcionando corretamente, você pode adicionar um método de teste:

```java
public void testarConexao() {
    Connection conexao = conectarAoMySQL();
    if (conexao != null) {
        System.out.println("Conexão bem-sucedida!");
        try {
            conexao.close(); // Certifique-se de fechar a conexão após o uso
        } catch (SQLException e) {
            e.printStackTrace();
        }
    } else {
        System.out.println("Falha na conexão.");
    }
}
```

Chame o método `testarConexao()` em algum lugar apropriado do seu código para verificar se a conexão está funcionando corretamente.

Com esses passos, você estabeleceu com sucesso a conexão com o MySQL em seu plugin Bukkit. Na próxima seção, exploraremos operações básicas do SQL para que você possa interagir efetivamente com o banco de dados.

---

### 3. Operações Básicas do SQL

Agora que você estabeleceu uma conexão com o MySQL em seu plugin Bukkit, é hora de aprender algumas operações básicas do SQL para interagir com o banco de dados. Abaixo estão exemplos de como realizar operações CRUD (Create, Read, Update, Delete):

#### 3.1. Inserção de Dados (CREATE)

Para inserir dados em uma tabela, você pode usar a declaração SQL `INSERT INTO`. Aqui está um exemplo de como inserir um jogador no banco de dados:

```java
public void inserirJogador(String nome, int pontos) {
    try (Connection conexao = conectarAoMySQL()) {
        String sql = "INSERT INTO tabela_jogadores (nome, pontos) VALUES (?, ?)";
        try (PreparedStatement preparedStatement = conexao.prepareStatement(sql)) {
            preparedStatement.setString(1, nome);
            preparedStatement.setInt(2, pontos);
            preparedStatement.executeUpdate();
        }
    } catch (SQLException e) {
        e.printStackTrace();
        // Tratamento adequado de erros deve ser implementado
    }
}
```

Certifique-se de substituir "tabela_jogadores" pelos nomes reais das suas tabelas.

#### 3.2. Consulta de Dados (READ)

Para recuperar dados de uma tabela, você pode usar a declaração SQL `SELECT`. Aqui está um exemplo de como obter a pontuação de um jogador:

```java
public int obterPontuacao(String nome) {
    try (Connection conexao = conectarAoMySQL()) {
        String sql = "SELECT pontos FROM tabela_jogadores WHERE nome = ?";
        try (PreparedStatement preparedStatement = conexao.prepareStatement(sql)) {
            preparedStatement.setString(1, nome);
            try (ResultSet resultSet = preparedStatement.executeQuery()) {
                if (resultSet.next()) {
                    return resultSet.getInt("pontos");
                }
            }
        }
    } catch (SQLException e) {
        e.printStackTrace();
        // Tratamento adequado de erros deve ser implementado
    }
    return 0; // Valor padrão se não encontrar o jogador
}
```

#### 3.3. Atualização de Dados (UPDATE)

Para atualizar dados em uma tabela, você pode usar a declaração SQL `UPDATE`. Aqui está um exemplo de como atualizar a pontuação de um jogador:

```java
public void atualizarPontuacao(String nome, int novaPontuacao) {
    try (Connection conexao = conectarAoMySQL()) {
        String sql = "UPDATE tabela_jogadores SET pontos = ? WHERE nome = ?";
        try (PreparedStatement preparedStatement = conexao.prepareStatement(sql)) {
            preparedStatement.setInt(1, novaPontuacao);
            preparedStatement.setString(2, nome);
            preparedStatement.executeUpdate();
        }
    } catch (SQLException e) {
        e.printStackTrace();
        // Tratamento adequado de erros deve ser implementado
    }
}
```

#### 3.4. Exclusão de Dados (DELETE)

Para excluir dados de uma tabela, você pode usar a declaração SQL `DELETE`. Aqui está um exemplo de como excluir um jogador:

```java
public void excluirJogador(String nome) {
    try (Connection conexao = conectarAoMySQL()) {
        String sql = "DELETE FROM tabela_jogadores WHERE nome = ?";
        try (PreparedStatement preparedStatement = conexao.prepareStatement(sql)) {
            preparedStatement.setString(1, nome);
            preparedStatement.executeUpdate();
        }
    } catch (SQLException e) {
        e.printStackTrace();
        // Tratamento adequado de erros deve ser implementado
    }
}
```

Essas são operações básicas do SQL que você pode realizar em seu plugin Bukkit para interagir com o banco de dados MySQL. Na próxima seção, aplicaremos esses conceitos em exemplos práticos para consolidar seu aprendizado.

---

### 4. Exemplos Práticos

Agora que você aprendeu a conectar seu plugin Bukkit ao MySQL e realizar operações básicas do SQL, vamos explorar exemplos práticos de como aplicar esses conceitos em situações do mundo real.

#### 4.1. Exemplo de Sistema de Pontuação para Jogadores

Vamos criar um sistema simples de pontuação para jogadores, onde podemos adicionar, consultar, atualizar e excluir jogadores e suas pontuações no banco de dados.

```java
public class SistemaPontuacao {

    public void adicionarJogador(String nome, int pontos) {
        inserirJogador(nome, pontos);
        System.out.println("Jogador adicionado: " + nome);
    }

    public void consultarPontuacao(String nome) {
        int pontuacao = obterPontuacao(nome);
        System.out.println("Pontuação de " + nome + ": " + pontuacao);
    }

    public void atualizarPontuacao(String nome, int novaPontuacao) {
        atualizarPontuacao(nome, novaPontuacao);
        System.out.println("Pontuação de " + nome + " atualizada para: " + novaPontuacao);
    }

    public void removerJogador(String nome) {
        excluirJogador(nome);
        System.out.println("Jogador removido: " + nome);
    }

    public static void main(String[] args) {
        SistemaPontuacao sistema = new SistemaPontuacao();

        // Adiciona um jogador
        sistema.adicionarJogador("Player1", 100);

        // Consulta a pontuação do jogador
        sistema.consultarPontuacao("Player1");

        // Atualiza a pontuação do jogador
        sistema.atualizarPontuacao("Player1", 150);

        // Consulta a pontuação atualizada
        sistema.consultarPontuacao("Player1");

        // Remove o jogador
        sistema.removerJogador("Player1");
    }
}
```

### Outro exemplo:

```java
import org.bukkit.command.Command;
import org.bukkit.command.CommandExecutor;
import org.bukkit.command.CommandSender;
import org.bukkit.plugin.java.JavaPlugin;

import java.sql.*;

public class PontuacaoPlugin extends JavaPlugin implements CommandExecutor {

    private String jdbcUrl = "jdbc:mysql://localhost:3306/seu_banco";
    private String username = "seu_usuario";
    private String password = "sua_senha";

    @Override
    public void onEnable() {
        getLogger().info("Plugin PontuacaoPlugin ativado!");

        // Registra o comando /pontuacao
        getCommand("pontuacao").setExecutor(this);

        // Cria a tabela de jogadores se não existir
        criarTabelaJogadores();
    }

    @Override
    public void onDisable() {
        getLogger().info("Plugin PontuacaoPlugin desativado!");
    }

    // Método para criar a tabela de jogadores se não existir
    private void criarTabelaJogadores() {
        try (Connection conexao = DriverManager.getConnection(jdbcUrl, username, password);
             Statement statement = conexao.createStatement()) {
            String sql = "CREATE TABLE IF NOT EXISTS tabela_jogadores (nome VARCHAR(50) PRIMARY KEY, pontos INT)";
            statement.executeUpdate(sql);
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    @Override
    public boolean onCommand(CommandSender sender, Command command, String label, String[] args) {
        if (command.getName().equalsIgnoreCase("pontuacao")) {
            if (args.length == 1) {
                String nome = args[0];

                // Consulta a pontuação do jogador
                int pontuacao = obterPontuacao(nome);

                sender.sendMessage("Pontuação de " + nome + ": " + pontuacao);
            } else if (args.length == 2) {
                String nome = args[0];
                int pontos = Integer.parseInt(args[1]);

                // Atualiza a pontuação do jogador
                atualizarPontuacao(nome, pontos);

                sender.sendMessage("Pontuação de " + nome + " atualizada para: " + pontos);
            } else {
                sender.sendMessage("Uso correto: /pontuacao <nome> [pontos]");
            }
            return true;
        }
        return false;
    }

    // Método para obter a pontuação de um jogador
    private int obterPontuacao(String nome) {
        try (Connection conexao = DriverManager.getConnection(jdbcUrl, username, password)) {
            String sql = "SELECT pontos FROM tabela_jogadores WHERE nome = ?";
            try (PreparedStatement preparedStatement = conexao.prepareStatement(sql)) {
                preparedStatement.setString(1, nome);
                try (ResultSet resultSet = preparedStatement.executeQuery()) {
                    if (resultSet.next()) {
                        return resultSet.getInt("pontos");
                    }
                }
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return 0; // Valor padrão se não encontrar o jogador
    }

    // Método para atualizar a pontuação de um jogador
    private void atualizarPontuacao(String nome, int novaPontuacao) {
        try (Connection conexao = DriverManager.getConnection(jdbcUrl, username, password)) {
            String sql = "INSERT INTO tabela_jogadores (nome, pontos) VALUES (?, ?)" +
                         "ON DUPLICATE KEY UPDATE pontos = ?";
            try (PreparedStatement preparedStatement = conexao.prepareStatement(sql)) {
                preparedStatement.setString(1, nome);
                preparedStatement.setInt(2, novaPontuacao);
                preparedStatement.setInt(3, novaPontuacao);
                preparedStatement.executeUpdate();
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

Este exemplo demonstra como criar e utilizar um sistema básico de pontuação em um servidor Bukkit, integrando-o ao MySQL para armazenar e recuperar dados de jogadores.

#### 4.2. Outros Exemplos

Além do sistema de pontuação, você pode adaptar esses conceitos para diversas aplicações, como armazenar configurações do servidor, registrar eventos de jogadores, entre outros.

Com esses exemplos práticos, você está pronto para incorporar o MySQL em seus projetos Bukkit de maneira eficiente e escalável. Na seção final, discutiremos algumas considerações finais e forneceremos recursos adicionais para aprimorar seus conhecimentos.

---

### 5. Considerações Finais

Parabéns! Você agora tem uma compreensão básica de como utilizar o MySQL em seus plugins Bukkit Java. Aqui estão algumas considerações finais para consolidar seu aprendizado:

#### 5.1. Boas Práticas

- **Segurança**: Evite expor informações sensíveis, como credenciais de banco de dados, diretamente no código fonte. Considere o uso de arquivos de configuração ou sistemas de autenticação mais seguros.

- **Gerenciamento de Conexão**: Certifique-se de fechar as conexões com o banco de dados após o uso para evitar vazamentos de recursos.

#### 5.2. Melhorias e Otimizações

- **Pool de Conexões**: Considere o uso de pools de conexões para melhor gerenciamento de conexões com o banco de dados.

- **Caching**: Implemente estratégias de cache para otimizar o desempenho, especialmente para consultas frequentes.

#### 5.3. Documentação Adicional

- Consulte a [documentação oficial do MySQL](https://dev.mysql.com/doc/) para informações detalhadas sobre SQL e configuração do MySQL.

- Explore a [documentação do Bukkit](https://hub.spigotmc.org/javadocs/spigot/) para aprofundar seus conhecimentos sobre o desenvolvimento de plugins Bukkit.

#### 5.4. Recursos Adicionais

- [MySQL JDBC Connector](https://dev.mysql.com/downloads/connector/j/): Baixe o driver JDBC do MySQL para sua aplicação.

- [Bukkit API Reference](https://hub.spigotmc.org/javadocs/spigot/): Explore a documentação oficial do Bukkit para aprender mais sobre a API Bukkit.

Lembre-se de adaptar o código conforme necessário para atender aos requisitos específicos do seu projeto. Se surgirem dúvidas ou desafios adicionais, consulte a comunidade Bukkit e os recursos online disponíveis.

Esperamos que este guia tenha sido útil para acelerar seu aprendizado sobre o uso do MySQL em plugins Bukkit Java. Boa sorte em seus projetos futuros!

---

> [!WARNING]
>  Foi utilizado CHAT GPT 3.5 TURBO para estilização dos textos para mais entendimento do nosso guia.
