# PostgreSQL


# Introduçao ao Sistema de Banco de Dados PostgreSQL

### O QUE É POSTGRESQL?

Anúncio site oficial: o banco de dados open source mais avançado do mundo! • Sistema de gerenciamento de banco de dados objetorelacional • Baseado no POSTGRES versão 4.2, desenvolvido na Universidade de Berkeley na Califórnia • Suporta grande parte dos comandos da linguagem SQL/ANSI padrão • Oferece muitas características modernas e pode ser estendido

### HISTÓRICO DO POSTGRESQL

Postgres: criado na UCB por um professor de ciência da computação • 1995, Postgres95: substituição linguagem de consulta PostQUEL do Postgres por um subconjunto estendido de funções do SQL • 1996, PostgreSQL: desenvolvimento do open source fora do campus • PostgreSQL versão 6.0: novos recursos adicionados e vários aprimoramentos

### ÚLTIMAS VERSÕES (10.6 E 11.1)

10.6 - Replicação Lógica - Uma estrutura de publicação / assinatura para distribuição de dados, Particionamento Declarativo de Tabelas, Melhor paralelismo de consulta, Commit por Quórum para Replicação Síncrona, Autenticação SCRAM-SHA-256

11.1 - Maior Robustez e Desempenho para Particionamento, Transações Suportadas em Procedimentos Armazenados, Recursos Aprimorados para Paralelismo de Consultas, Compilação Just-in-Time (JIT) para Expressões, Melhorias Gerais para Experiência do Usuário, como inclusão das palavras-chave "quit" e "exit" na interface de linha de comando

### INSTALANDO O POSTGRESQL

• Disponível em uma ampla gama de plataformas 

• Licença de código aberto TPL (The PostgreSQL License)

 • Usado por muitos pacotes de aplicativos diferentes 

• Muitas distribuições Linux incluem PostgreSQL como parte da instalação básica

 • É possível baixar o código-fonte ou baixar um dos pacotes a partir de:

 – http://www.postgresql.org/download/ 

– Basta seguir o guia de instalação

 – Diretório normalmente chamado /usr/local/pgsql

### CONECTANDO A UM SERVIDOR POSTGRES

• É preciso ter um servidor PostgreSQL rodando no host, escutando uma porta 

• Devem existir um banco de dados e um usuário devidamente cadastrado 

• O host deve permitir explicitamente conexões dos clientes que fornecem os dados para autenticação – usando o método especificado pelo servidor

### EXEMPLO DE UMA CONEXÃO USANDO O SQL SHELL (PSQL)

• localhost para o servidor 

• TRT_PR para o banco de dados

• 5432 para a porta 

• postgres para o usuário

### SQL SHELL (PSQL)

• É um front-end baseado em terminal para PostgreSQL 

– permite que você digite os comandos interativamente 

– sua entrada também pode ser um arquivo 

• Fornece um número de meta-comandos 

• Possui diversas funcionalidades shell-like

 – facilitar a escrita de scripts 

– automatizar uma grande variedade de tarefas

### SERVIDOR DE BANCO DE DADOS POSTGRESQL

• É classificado como cliente-servidor 

• Local onde sistema roda é conhecido como host 

• Podemos acessar remotamente através da rede 

• Devemos especificar o host 

– nome de host ou hostaddr (endereço IP) 

• Podemos especificar o host como "localhost“ 

– conexão TCP/IP para o mesmo servidor 

• Possibilidade de conexão socket Unix 

– nome do host inicia por barra (/)

### CARACTERÍSTICAS CONEXÃO POSTGRESQL

• Cada servidor escuta exatamente uma porta de rede 

– não pode ser compartilhada entre os servidores no mesmo host 

• O número da porta padrão para PostgreSQL é 5432 

– pode ser usado para identificar exclusivamente um servidor de BD específico (se existirem muitos) 

• Um servidor de banco de dados também é conhecido como um "cluster de banco de dados“ 

– servidor PostgreSQL permite definir um ou mais DB em cada servidor 

• Cada solicitação de conexão deve identificar exatamente um banco de dados identificado por seu DBNAME

### CONFIRMAÇÃO DE CONEXÃO A SERVIDOR CERTO

• SELECT inet_server_port(); 

Exibe a porta na qual o servidor está escutando 

• SELECT current_database(); 

Mostra o banco de dados atual 

• SELECT current_user; 

Mostra o ID do usuário atual 

• SELECT inet_server_addr();

Mostra o endereço IP do servidor que aceitou a conexão

### CRIANDO UM BANCO DE DADOS

• Sintaxe: initdb [option...] [--pgdata | -D] directory 

– Permite criar um novo cluster de banco de dados 

– parâmetro PGDATA/-D: especifica o diretório onde o cluster de BD deve ser armazenado 

• Comando CREATE DATABASE: cria uma nova base de dados

## ADMINISTRAÇÃO DO SERVIDOR

### DISTRIBUIÇÃO DOS ARQUIVOS EM DIRETÓRIOS

• /usr/local/pgsql - diretório raiz após instalação 

• /bin - programas de linha de comando 

• /data/base - Um subdiretório é criado para cada banco de dados 

• /doc - documentação do PostgreSQL 

• /lib - bibliotecas 

• /man - manuais POSTGRESQL

## PGADMIN 4

• Plataforma para administração e desenvolvimento de banco de dados PostgreSQL 

• Aplicativo pode ser usado em: – Linux, FreeBSD, Solaris, Mac OSX e Windows e versões comerciais/derivadas de PostgreSQL 

• Projetado para atender as necessidades dos usuários 

• É possível escrever consultas SQL para desenvolver bases de dados complexas 

• Interface gráfica suporta todas as funcionalidades do PostgreSQL

### FUNCIONALIDADES DE SEGURANÇA DA INFORMAÇÃO NO POSTGRES

• Revogar o acesso do usuário a uma tabela 

• Concessão do acesso de usuário a uma tabela 

• Criação de um novo usuário 

• Impedir temporariamente a conexão de um usuário 

• Remover um usuário sem deixar apagar os seus dados 

• Verificar se todos os usuários têm uma senha segura 

• Limitar os poderes de superusuário a usuários específicos 

• Criar auditoria para comandos DDL 

• Integração com LDAP 

• Conectar-se usando SSL 

• Criptografia de dados confidenciais

### AUTENTICAÇÃO DO CLIENTE

• Processo pelo qual o servidor de banco de dados estabelece a identidade do cliente 

• Determina se o aplicativo cliente tem permissão para se conectar com o banco de dados 

• O PostgreSQL oferece diferentes métodos de autenticação para o cliente 

• Método utilizado para autenticação pode ser baseado em: 

– endereço de host do cliente

 – banco de dados 

– usuários

### O ARQUIVO PG_HBA.CONF

• Arquivo de configuração que controla autenticação do cliente 

• É armazenado no diretório de dados raiz do banco de dados 

• Um arquivo padrão é criado quando o diretório de dados é inicializado 

• O formato geral é um conjunto de registos, um por linha 

• Cada registro especifica um tipo de conexão 

– uma faixa de endereço IP de cliente (se relevante)

 – um nome de banco de dados 

– um nome de usuário

 – o método de autenticação a ser usado

### MÉTODOS DE AUTENTICAÇÃO

• trust – permite a conexão incondicionalmente 

• reject – rejeita qualquer conexão incondicionalmente 

• md5 – exige que o cliente forneça uma senha double-MD5- hash 

• password – exige que o cliente forneça uma senha não criptografada 

• GSS – usa GSSAPI para autenticar usuário (conexões TCP/IP) 

• sspi - usa SSPI para autenticar o usuário (apenas Windows)

### MÉTODOS DE AUTENTICAÇÃO (CONT.)

• ident – obtém o nome do usuário no servidor e faz verificação (conexões TCP/IP) 

• peer – obtém o nome do usuário do sistema operacional e faz verificação (conexões locais) 

• ldap – autentica usando um servidor LDAP 

• radius – autentica usando um servidor RADIUS 

• cert – autentica usando certificados de cliente SSL 

• PAM - autentica utilizando o serviço PAM

### CONCEITO DE PAPÉIS

PostgreSQL administra as permissões utilizando o conceito de papéis 

• Refere-se a grupo de usuários da base de dados 

– dependendo de como o papel é configurado 

• Roles (papéis) podem possuir permissões sobre: 

– objetos de banco de dados (por exemplo, tabelas) 

• Papeis podem atribuir privilégios sobre: 

– objetos a outros papéis 

• Qualquer papel pode atuar como um usuário, um grupo ou ambos

### PAPÉIS NO BANCO DE DADOS

• São conceitualmente separados dos usuários do sistema operacional 

• São globais através de uma instalação de um cluster de banco de dados 

• CREATE ROLE nome; - cria um papel 

• DROP ROLE nome; - remove uma função existente 

• SELECT rolname FROM pg_roles; - examina o catálogo do sistema

### PAPÉIS NO BANCO DE DADOS

• programa psql \du: meta-comando útil para listar os papéis existentes 

### SINTAXE CREATE ROLE

CREATE ROLE name [ [ WITH ] option [ ... ] ] 

As opções podem ser as seguintes: 

SUPERUSER | NOSUPERUSER 

| CREATEDB | NOCREATEDB 

| CREATEROLE | NOCREATEROLE 

| CREATEUSER | NOCREATEUSER 

| INHERIT | NOINHERIT 

| LOGIN | NOLOGIN 

| REPLICATION | NOREPLICATION 

| CONNECTION LIMIT connlimit 

| [ ENCRYPTED | UNENCRYPTED ] PASSWORD 'password' 

| VALID UNTIL 'timestamp' 

| IN ROLE role_name [, ...] 

| IN GROUP role_name [, ...] 

| ROLE role_name [, ...] 

| ADMIN role_name [, ...] 

| USER role_name [, ...] 

| SYSID uid

### CREATE TABLE

• Cria uma tabela nova inicialmente vazia no banco de dados 

• Tabela será de propriedade do usuário que emite o comando 

• Nome da tabela deve ser distinto do nome de qualquer outra tabela, sequência, índice, visão ou tabela estrangeira no mesmo esquema 

• Restrição: objeto SQL que ajuda a definir o conjunto de valores válidos na tabela de várias maneiras 

– restrições de tabela e restrições de coluna

### CREATE SEQUENCE

• Cria um novo gerador de números sequenciais 

• Cria e inicia uma nova tabela especial de uma única linha 

• O gerador será de propriedade do usuário que emite o comando 

• O nome da sequência deve ser distinto do nome de qualquer outra sequência, tabela, índice, visão ou tabela estrangeira no mesmo esquema

### CREATE INDEX

• Constrói um índice na(s) coluna(s) especificada(s) da relação 

• Os índices são utilizados principalmente para melhorar o desempenho do banco de dados 

• Um campo de índice pode ser uma expressão calculada a partir dos valores de uma ou mais colunas 

• PostgreSQL fornece os métodos de índice B-tree, de hash, GiST, SP-GiST e GIN 

• Cláusula WHERE presente: um índice parcial é criado

### CREATE VIEW

• Define uma visão sobre uma tabela 

• A visão não é fisicamente materializada 

• Consulta é executada toda vez que a visão é referenciada em uma consulta 

• O nome da visão deve ser distinto do nome de qualquer outra visão, tabela, sequência, índice ou tabela estrangeira no mesmo esquema

### CREATE TRIGGER

• Cria um novo gatilho 

• O gatilho fica associado a uma tabela, visão ou tabela estrangeira especificada 

• Executa a função especificada quando ocorrem certos eventos 

• Um gatilho pode ser especificado para disparar 

– antes de uma operação ser realizada em uma linha 

– após a conclusão da operação

 – em vez da operação (INSTEAD OF)

### OUTROS COMANDOS DDL

• DROP TABLE: remove tabelas do banco de dados 

• DELETE ou TRUNCATE TABLE: esvazia uma tabela de linhas sem destruir a tabela 

• ALTER TABLE: altera a definição de uma tabela existente

### COMANDOS DML

#### SELECT

• Recupera linhas de zero ou mais tabelas 

• Todas as consultas listadas na cláusula WITH são computadas 

• Todos os elementos na lista do FROM são computados 

• Cláusula WHERE especificada: todas as linhas que não satisfazem a condição são eliminadas 

• Cláusula GROUP BY especificada: saída é combinada em grupos de linhas

• Cláusula HAVING presente: elimina os grupos que não satisfaçam a condição dada

#### SELECT (CONT.)

• Operadores UNION, INTERSECT e EXCEPT: a saída de mais de uma instrução SELECT pode ser combinada para formar um único conjunto de resultado 

• Cláusula ORDER BY especificada: as linhas retornadas são classificadas na ordem especificada 

• Limite (ou FETCH FIRST) ou cláusula OFFSET especificado: a instrução de SELECT retorna apenas um subconjunto das linhas do resultado 

• FOR UPDATE, FOR NO KEY UPDATE, FOR SHARE ou FOR KEY SHARE especificados: a instrução SELECT bloqueia as linhas selecionadas contra atualizações simultâneas

#### INSERT

• Adiciona novas linhas em uma tabela 

• Pode-se inserir uma ou mais linhas especificando 

– seus valores ou zero 

– mais linhas resultantes de uma consulta

#### DELETE

• Apaga as linhas que satisfazem à cláusula WHERE da tabela especificada 

• Cláusula WHERE ausente: efeito é o de excluir todas as linhas na tabela 

• Cláusula opcional RETURNING: calcula e retorna valor (es) com base em cada linha realmente excluída 

• Qualquer expressão utilizando as colunas da tabela, e/ou colunas de outras tabelas mencionadas no USING podem ser computadas 

#### UPDATE

• Muda os valores das colunas especificadas em todas as linhas que satisfazem a condição 

• Somente as colunas a serem modificadas devem ser mencionadas na cláusula SET 

• Colunas que não serão modificadas explicitamente manterão seus valores 

• Cláusula opcional RETURNING: faz com que o UPDATE possa calcular e retornar valor(es) com base em cada linha atualizada

### FUNCIONALIDADES DO PGADMIN

| Gráfico para planos de consultas usando o EXPLAIN | oferece uma visão pictórica sobre como o planejador de consultas está pensando |
| ------------------------------------------------- | ------------------------------------------------------------ |
| Painel SQL                                        | pgAdmin consegue interagir com PostgreSQL via SQL, permitindo inclusive que você veja o SQL gerado |
| Edição direta de arquivos de configuração         | postgresql.conf e pg_hba.conf                                |
| Exportação de dados                               | pgAdmin pode facilmente exportar os resultados da consulta para CSV ou outro formato delimitado |
| Assistente de backup e restauração                | pgAdmin tem uma boa interface para fazer backup e restaurações |
| Assistente de Grant                               | assistente permitirá alteração de permissões em muitos objetos de banco de dados de uma só vez |
| Motor pgScript                                    | maneira rápida e suja para executar scripts que não têm que completar suas operações como uma transação |
| Arquitetura de Plugin                             | add-ons são rapidamente acessíveis com um único clique do mouse |
| pgAgent plugin                                    | agente de agendamento de trabalho multi-plataforma           |

### TIPOS DE DADOS DO POSTGRESQL

### PECULIARIDADES

• PostgreSQL suporta os tipos de dados tradicionais de qualquer banco de dados 

• Possui também suporte para datas e horas com fusos horários, intervalos de tempo, matrizes e XML 

• Fatores que possibilitam diferentes tipos de dados nos SGBDs

 – Resultados consistentes 

– Validação de dados 

– Armazenamento compacto

 – Desempenho

### TIPOS DE STRINGS DE CARACTERES

• Tipos de cadeias de caracteres são os tipos de dados mais comumente usados 

• Qualquer sequência de letras, números, pontuação e outros caracteres válidos 

• TEXT: não limita número de caracteres armazenados

• VARCHAR (length): limita o comprimento do campo de caracteres ao comprimento passado como parâmetro 

• CHAR(length): sempre armazena exatamente os caracteres definidos no comprimento

### CARACTERÍSTICAS TIPOS NUMÉRICOS

• Permitem a armazenagem de números 

• Consistem de inteiros de dois, quatro e oito bytes 

• Números de ponto flutuante: de quatro e oito bytes 

• Decimais: de precisão selecionável

### TIPOS NUMÉRICOS

• INTEGER, INT2, INT8: armazenam números inteiros de diferentes ranges 

– Intervalos maiores requerem mais espaço de armazenamento 

• OID: usada para armazenar o PostgreSQL identificadores de objetos 

• NUMERIC(): permite definir os dígitos de precisão e o arredondamento em casas decimais 

– os tipos DECIMAL e NUMERIC são equivalentes 

• FLOAT e FLOAT4: permitem o armazenamento de valores de ponto flutuante

### TIPOS TEMPORAIS

• Tipos temporais permitem o armazenamento de data, hora e informação do intervalo de tempo 

• DATE: permite o armazenamento de uma data única que consiste em um ano, mês e dia 

• TIME: permite o armazenamento de uma hora, minuto e segundo 

• TIMESTAMP: armazena tanto a data e a hora 

• INTERVAL: representa um intervalo de tempo

### TIPO LÓGICO

• O único tipo de dados lógico é BOOLEAN 

• Um campo BOOLEAN pode armazenar apenas: 

– Verdadeiro: true, t, yes, y, ou 1 

– Falso: false, f, no, n, ou 0

 – NULL
