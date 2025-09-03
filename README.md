# Laboratório de Simulação de Vulnerabilidades em Aplicações Web

## 📖 Sobre o Projeto

Este projeto, desenvolvido para o Desafio de Projeto da DIO, consiste na criação de um ambiente controlado (laboratório) para simular e estudar vulnerabilidades comuns em aplicações web. O objetivo é demonstrar de forma prática os conceitos de segurança ofensiva, entendendo como um atacante poderia explorar falhas para, então, aprender a mitigá-las.

O ambiente foi containerizado com Docker para garantir portabilidade, isolamento e facilidade na replicação dos cenários.

---

## 🎯 Objetivo

O principal objetivo deste laboratório é aplicar os conhecimentos de segurança da informação em um cenário prático, documentando o processo de identificação, exploração e mitigação de vulnerabilidades conhecidas, como SQL Injection e Cross-Site Scripting (XSS).

---

## 🛠️ Tecnologias Utilizadas

- **Python:** Linguagem de programação principal da aplicação.
- **Flask:** Micro-framework web para criar a aplicação vulnerável.
- **SQLite:** Banco de dados relacional para simular a persistência de dados.
- **Docker:** Plataforma de containerização para criar e gerenciar o ambiente controlado.
- **Git & GitHub:** Para controle de versão e documentação do projeto.

---

## ⚙️ Configuração do Ambiente Controlado

Para executar este laboratório, você precisará ter o Git e o Docker instalados em sua máquina.

1.  **Clone o repositório:**
    ```bash
    git clone [https://github.com/SEU_USUARIO/SEU_REPOSITORIO.git](https://github.com/SEU_USUARIO/SEU_REPOSITORIO.git)
    cd SEU_REPOSITORIO
    ```

2.  **Construa e execute o container Docker:**
    O `docker-compose` irá orquestrar a construção da imagem e a execução do container.
    ```bash
    docker-compose up --build
    ```

3.  **Acesse a aplicação:**
    Após a execução do comando acima, a aplicação web vulnerável estará disponível no seu navegador no seguinte endereço:
    [http://localhost:5000](http://localhost:5000)

---

## 💣 Cenários de Vulnerabilidade Estudados

### 1. SQL Injection (SQLi)

**O que é?**
A Injeção de SQL é uma falha de segurança que permite a um atacante interferir nas consultas que uma aplicação faz ao seu banco de dados. Isso geralmente ocorre quando a entrada do usuário não é devidamente validada ou sanitizada antes de ser incluída em uma instrução SQL.

**Simulação do Ataque:**
A aplicação possui uma tela de login simples. Para simular o ataque, podemos bypassar a autenticação:

1.  Acesse a página de login em `http://localhost:5000/login`.
2.  No campo "Usuário", insira a seguinte string: `admin' --`
3.  No campo "Senha", insira qualquer valor.
4.  Clique em "Entrar". Você conseguirá acesso como administrador sem saber a senha.

**Evidência:**
*(Aqui você insere uma captura de tela mostrando o login bem-sucedido com o payload de SQLi)*
![Exemplo de SQL Injection](images/sqli-exemplo-1.png)

**Mitigação:**
A forma mais eficaz de prevenir SQL Injection é utilizar **consultas parametrizadas (Prepared Statements)**. Em vez de concatenar strings para montar a query, passamos os dados do usuário como parâmetros, e o driver do banco de dados se encarrega de tratá-los de forma segura.

### 2. Cross-Site Scripting (XSS) Refletido

**O que é?**
O XSS é uma vulnerabilidade que permite a um atacante injetar scripts maliciosos (geralmente JavaScript) em páginas web vistas por outros usuários. No XSS Refletido, o script é injetado através de uma requisição HTTP (como um parâmetro de URL) e refletido de volta na resposta do servidor.

**Simulação do Ataque:**
A aplicação possui uma página de busca que reflete o termo pesquisado na tela.

1.  Acesse a página de busca em `http://localhost:5000/busca`.
2.  No campo de busca, insira o seguinte payload: `<script>alert('Você foi hackeado!');</script>`
3.  Clique em "Buscar". Um pop-up de alerta do JavaScript será exibido, demonstrando que o script foi executado.

**Evidência:**
*(Aqui você insere uma captura de tela mostrando o alerta do JavaScript aparecendo na tela)*
![Exemplo de XSS](images/xss-exemplo-1.png)

**Mitigação:**
Para prevenir XSS, é crucial realizar o **Output Encoding**. Isso significa que qualquer dado proveniente do usuário que será exibido na página deve ser tratado para que o navegador o interprete como texto, e não como código HTML/JavaScript. Frameworks modernos como o Flask (com o motor de templates Jinja2) fazem isso automaticamente na maioria dos casos.

---

## 🎓 Conclusão

Este projeto permitiu a aplicação prática de conceitos teóricos de segurança, destacando a importância de práticas de desenvolvimento seguro. A criação de um ambiente controlado com Docker se mostrou uma abordagem eficaz para estudar vulnerabilidades de forma segura e isolada.

---

## 👨‍💻 Autor

**[Seu Nome Completo]**

- LinkedIn: https://pt.linkedin.com/
- GitHub: https://www.youtube.com/watch?v=TsaLQAetPLU
