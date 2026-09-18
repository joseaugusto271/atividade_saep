# Cadastro eleitoral - CRUD em PHP + MySQL

CRUD de **eleitores** e **candidatos** (banco `eleitor`), feito com PHP puro (PDO), MySQL, HTML e CSS.

## Como rodar

1. Instale o **XAMPP** (ou WAMP/Laragon) e inicie **Apache** e **MySQL**.
2. Copie a pasta `crud-eleitoral` para `C:\xampp\htdocs\`.
3. **Se você já tem o banco criado**, não precisa importar nada: abra `config.php` e coloque o nome do seu banco em `DB_NAME`.
   Se ainda não tem, no phpMyAdmin (`http://localhost/phpmyadmin`) vá em **Importar** e envie `database.sql` (cria o banco `eleitor` com dados de exemplo).
4. Se o seu MySQL tiver senha, ajuste `DB_USER` e `DB_PASS` em `config.php`.
5. Acesse `http://localhost/crud-eleitoral/`.

## Estrutura

| Arquivo | Função |
|---|---|
| `database.sql` | Cria o banco `eleitor`, as tabelas `eleitor1` e `candidato1` e dados de exemplo |
| `config.php` | Conexão PDO, CSRF, mensagens e funções auxiliares |
| `index.php` | Página inicial com totais e últimos cadastros |
| `eleitores.php` | **R**ead: lista e busca eleitores |
| `eleitor_form.php` | **C**reate e **U**pdate de eleitor (mesmo formulário) |
| `eleitor_excluir.php` | **D**elete de eleitor |
| `candidatos.php`, `candidato_form.php`, `candidato_excluir.php` | Mesmo CRUD para candidatos |
| `includes/header.php`, `includes/footer.php` | Layout compartilhado |
| `assets/style.css`, `assets/app.js` | Visual e comportamento (confirmação de exclusão, prévia do número) |

## Tabelas

**eleitor1**: `id_eleitor1` (PK, INT), `nome` (VARCHAR 100), `numero_titulo` (VARCHAR 20, formato `TIT` + 3 dígitos, ex.: `TIT001`), `cidade` (VARCHAR 80, opcional)

**candidato1**: `id_candidato1` (PK, INT), `nome` (VARCHAR 100), `numero_candidato` (INT), `cargo` (VARCHAR 50), `partido_ficticio` (VARCHAR 50, opcional)

As colunas `id_eleitor1` e `id_candidato1` precisam ser **AUTO_INCREMENT** para o cadastro funcionar.

## Boas práticas usadas

- Consultas com **prepared statements** (PDO), sem concatenar dados do usuário no SQL.
- Saída escapada com `htmlspecialchars` (função `e()`), contra XSS.
- Exclusão apenas por **POST** com token **CSRF**.
- Validação no servidor e checagem de duplicidade (título/número já cadastrado), feita no PHP e não só no banco.

## SCRUM: sugestão para o grupo

**Papéis:** Product Owner (define prioridades), Scrum Master (remove impedimentos e conduz as reuniões) e Time de Desenvolvimento (demais integrantes).

**Product Backlog**

| # | História de usuário | Prioridade |
|---|---|---|
| 1 | Como administrador, quero cadastrar um eleitor para manter a lista atualizada | Alta |
| 2 | Como administrador, quero listar e buscar eleitores | Alta |
| 3 | Como administrador, quero editar um eleitor para corrigir dados | Alta |
| 4 | Como administrador, quero excluir um eleitor com confirmação | Alta |
| 5 | Como administrador, quero cadastrar, listar, editar e excluir candidatos | Alta |
| 6 | Como administrador, quero ver um resumo na página inicial | Média |
| 7 | Como administrador, quero mensagens claras de erro e sucesso | Média |

**Sprint 1:** banco de dados, conexão e CRUD de eleitores (histórias 1 a 4).
**Sprint 2:** CRUD de candidatos, página inicial e ajustes de interface (histórias 5 a 7).

**Definition of Done:** funciona no XAMPP, valida os campos, não quebra com dados duplicados e foi revisado por outro integrante.

**Cerimônias:** Sprint Planning (início), Daily (o que fiz, o que farei, impedimentos), Sprint Review (demonstração) e Retrospectiva (o que melhorar).
