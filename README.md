# Atividade III - SEDUC DEST2

### Planejar, criar e testar um banco de dados para um domínio qualquer.

#  NOIR

**Banco de Dados para uma Plataforma de Streaming Musical**

------------------------------------------------------------------------

##  1. Contextualização

O **NOIR** é um projeto de banco de dados para uma plataforma fictícia
de streaming musical. O sistema organiza informações sobre usuários,
artistas, gêneros musicais, álbuns, músicas, playlists, favoritos e
histórico de reprodução.

O projeto utiliza um banco de dados relacional desenvolvido em MySQL,
com o propósito de manter as informações estruturadas, facilitar
consultas e garantir maior consistência dos dados.

##  2. Problemas sem um Banco de Dados

Sem um Sistema Gerenciador de Banco de Dados (SGBD) relacional, a
plataforma poderia enfrentar problemas como:

-   **Desorganização:** informações armazenadas de maneira dispersa.
-   **Duplicidade:** registros repetidos de usuários, artistas e
    músicas.
-   **Perda de informações:** dificuldade para manter os dados seguros.
-   **Consultas difíceis:** maior dificuldade para localizar músicas e
    playlists.
-   **Inconsistência:** informações divergentes entre registros.
-   **Manutenção complicada:** dificuldade para atualizar e administrar
    os dados.

##  3. Melhorias com um Banco de Dados Relacional

Com o uso do MySQL, o NOIR passa a contar com uma estrutura organizada e
integrada, proporcionando:

-   **Organização:** informações distribuídas em tabelas específicas.
-   **Integridade:** chaves primárias e estrangeiras para manter a
    consistência dos relacionamentos.
-   **Redução de redundâncias:** menos repetições desnecessárias.
-   **Consultas eficientes:** facilidade para pesquisar músicas,
    artistas, álbuns e playlists.
-   **Histórico de reprodução:** registro das músicas reproduzidas pelos
    usuários.
-   **Manutenção facilitada:** maior controle sobre os dados
    armazenados.

##  4. Estrutura do Banco de Dados

O banco de dados NOIR é composto por **13 tabelas**, cada uma responsável por armazenar um conjunto específico de informações.

### 4.1. `usuarios`

Armazena os dados dos usuários cadastrados na plataforma.

  Campo               Tipo           Descrição
  ------------------- -------------- --------------------------------------
  `id_usuarios`       INT            Identificador único do usuário (PK).
  `nome`              VARCHAR(250)   Nome completo.
  `email`             VARCHAR(150)   E-mail do usuário.
  `senha`             CHAR(50)       Senha armazenada no cadastro.
  `data_nascimento`   DATE           Data de nascimento.

  **Observação:** esta descrição segue o script `noir_usuarios.sql` enviado.

### 4.2. `artistas`

Armazena as informações dos artistas disponíveis na plataforma.

  Campo              Tipo           Descrição
  ------------------ -------------- --------------------------------------
  `id_artista`       INT            Identificador único do artista (PK).
  `nome_artistico`   VARCHAR(120)   Nome artístico.
  `biografia`        VARCHAR(150)   Biografia do artista.
  `pais_origem`      VARCHAR(80)    País de origem.

### 4.3. `generos`

Armazena os gêneros musicais disponíveis.

  Campo           Tipo           Descrição
  --------------- -------------- -------------------------------------
  `id_genero`     INT            Identificador único do gênero (PK).
  `nome_genero`   VARCHAR(80)    Nome do gênero musical.
  `descricao`     VARCHAR(255)   Descrição do gênero.

### 4.4. `artista_genero`

Relaciona artistas aos seus respectivos gêneros musicais.

  Campo          Tipo   Descrição
  -------------- ------ -------------------------------------
  `id_artista`   INT    Identificador do artista (PK e FK).
  `id_genero`    INT    Identificador do gênero (PK e FK).

### 4.5. `artista_redes_sociais`

Armazena os links das redes sociais dos artistas.

  Campo             Tipo           Descrição
  ----------------- -------------- ------------------------------------
  `id_rede`         INT            Identificador da rede social (PK).
  `id_artista`      INT            Artista relacionado (FK).
  `nome_rede`       VARCHAR(50)    Nome da rede social.
  `link_perfil`     VARCHAR(255)   Link do perfil do artista.

  A combinação entre artista e rede social é única, evitando cadastrar
  duas vezes a mesma plataforma para o mesmo artista.

### 4.6. `albuns`

Armazena os álbuns musicais cadastrados.

  Campo               Tipo           Descrição
  ------------------- -------------- ------------------------------------
  `id_album`          INT            Identificador único do álbum (PK).
  `titulo`            VARCHAR(150)   Título do álbum.
  `data_lancamento`   DATE           Data de lançamento.
  `capa_url`          VARCHAR(500)   Link da imagem da capa.

### 4.7. `album_artista`

Relaciona os álbuns aos artistas responsáveis por eles.

  Campo          Tipo   Descrição
  -------------- ------ -------------------------------------
  `id_album`     INT    Identificador do álbum (PK e FK).
  `id_artista`   INT    Identificador do artista (PK e FK).

### 4.8. `musicas`

Armazena as informações das músicas disponíveis.

  Campo                Tipo           Descrição
  -------------------- -------------- -------------------------------------
  `id_musica`          INT            Identificador único da música (PK).
  `id_album`           INT            Álbum relacionado (FK, opcional).
  `titulo`             VARCHAR(150)   Título da música.
  `duracao_segundos`   INT            Duração em segundos.
  `data_lancamento`    DATE           Data de lançamento.
  `arquivo_url`        VARCHAR(500)   Link do arquivo de áudio.

### 4.9. `musica_artista`

Relaciona as músicas aos artistas responsáveis por sua criação ou
interpretação.

  Campo          Tipo   Descrição
  -------------- ------ -------------------------------------
  `id_musica`    INT    Identificador da música (PK e FK).
  `id_artista`   INT    Identificador do artista (PK e FK).

### 4.10. `playlists`

Armazena as playlists criadas pelos usuários.

  Campo               Tipo           Descrição
  ------------------- -------------- -----------------------------------------
  `id_playlist`       INT            Identificador único da playlist (PK).
  `id_usuario`        INT            Usuário responsável pela playlist (FK).
  `nome_playlist`     VARCHAR(100)   Nome da playlist.
  `descricao`         TEXT           Descrição da playlist.
  `data_criacao`      DATE           Data de criação.

### 4.11. `playlist_musica`

Armazena as músicas adicionadas às playlists e suas posições.

  -----------------------------------------------------------------------
  Campo                   Tipo                    Descrição
  ----------------------- ----------------------- -----------------------
  `id_playlist`           INT                     Identificador da
                                                  playlist (PK e FK).

  `id_musica`             INT                     Identificador da música
                                                  (PK e FK).

  `posicao`               INT                     Posição da música na
                                                  playlist.

  `data_adicao`           DATETIME                Data e hora em que a
                                                  música foi adicionada.
  -----------------------------------------------------------------------

### 4.12. `favoritos`

Armazena as músicas favoritas dos usuários.

  -----------------------------------------------------------------------
  Campo                   Tipo                    Descrição
  ----------------------- ----------------------- -----------------------
  `id_usuario`            INT                     Identificador do
                                                  usuário (PK e FK).

  `id_musica`             INT                     Identificador da música
                                                  (PK e FK).

  `data_favorito`         DATETIME                Data e hora em que a
                                                  música foi favoritada.
  -----------------------------------------------------------------------

### 4.13. `historico_reproducao`

Registra as reproduções realizadas pelos usuários.

  Campo             Tipo       Descrição
  ----------------- ---------- -----------------------------------------
  `id_reproducao`   INT        Identificador único da reprodução (PK).
  `id_usuario`      INT        Usuário que reproduziu a música (FK).
  `id_musica`       INT        Música reproduzida (FK).
  `data_hora`       DATETIME   Data e hora da reprodução.

**Legenda:** - **PK (Primary Key):** chave primária que identifica um
registro. - **FK (Foreign Key):** chave estrangeira que relaciona uma
tabela a outra.

------------------------------------------------------------------------



## 📐 5. Aplicação das Formas Normais

A normalização organiza os dados para reduzir repetições desnecessárias
e evitar problemas de inserção, atualização e exclusão.

No projeto NOIR, a estrutura das tabelas busca aplicar as quatro
primeiras Formas Normais.

### 5.1. 1FN --- Primeira Forma Normal

**Objetivo:** garantir que cada campo armazene um único valor, sem
listas de informações na mesma coluna.

**Aplicação no NOIR:** os gêneros dos artistas, as redes sociais e as
músicas das playlists são organizados em tabelas específicas.

**Benefício:** dados mais organizados e fáceis de consultar.

### 5.2. 2FN --- Segunda Forma Normal

**Objetivo:** garantir que os atributos não chave dependam da chave
primária completa, sem dependências parciais.

**Aplicação no NOIR:** a tabela `musica_artista` utiliza uma chave
primária composta por `id_musica` e `id_artista`. O título da música e o
nome artístico permanecem em suas respectivas tabelas.

**Benefício:** redução de redundâncias e melhor organização das
informações.

### 5.3. 3FN --- Terceira Forma Normal

**Objetivo:** evitar dependências transitivas inadequadas entre
atributos não chave.

**Aplicação no NOIR:** os dados dos artistas são armazenados na tabela
`artistas`, enquanto os nomes e as descrições dos gêneros ficam na
tabela `generos`.

**Benefício:** menor risco de inconsistências e manutenção facilitada.

### 5.4. 4FN --- Quarta Forma Normal

**Objetivo:** evitar redundâncias causadas por informações
multivaloradas independentes.

**Aplicação no NOIR:** os gêneros dos artistas são armazenados na tabela
`artista_genero`, enquanto as redes sociais ficam na tabela
`artista_redes_sociais`.

**Benefício:** evita combinações redundantes entre gêneros musicais e
redes sociais.

### Resumo da Normalização

  -----------------------------------------------------------------------
  Forma Normal            Aplicação no NOIR       Benefício
  ----------------------- ----------------------- -----------------------
  **1FN**                 Armazenamento           Organização dos dados.
                          individual das          
                          informações.            

  **2FN**                 Separação dos atributos Redução de
                          de músicas e artistas.  redundâncias.

  **3FN**                 Separação das           Maior consistência.
                          informações de artistas 
                          e gêneros.              

  **4FN**                 Separação dos gêneros e Menos combinações
                          das redes sociais.      redundantes.
  -----------------------------------------------------------------------

> **Observação:** a confirmação de cada Forma Normal depende da análise
> das dependências funcionais e multivaloradas do modelo. A separação
> das tabelas contribui para a normalização, mas não substitui essa
> verificação.

------------------------------------------------------------------------



------------------------------------------------------------------------

## 6. Consultas SQL

As consultas abaixo representam situações do cotidiano da plataforma NOIR. Elas permitem pesquisar o catálogo, relacionar artistas e gêneros, acompanhar reproduções e analisar músicas favoritas.

> **Importante:** as consultas foram elaboradas com base na estrutura descrita neste README. Os resultados dependem dos registros cadastrados no banco; execute cada consulta no MySQL Workbench para conferir os valores reais.

### 6.1. Listar músicas e seus álbuns

**Contexto:** a plataforma precisa exibir o catálogo musical e informar a qual álbum cada música pertence.

```sql
USE noir;

SELECT m.id_musica,
       m.titulo AS musica,
       a.titulo AS album,
       m.data_lancamento,
       m.duracao_segundos
FROM musicas AS m
LEFT JOIN albuns AS a ON m.id_album = a.id_album
ORDER BY m.titulo;
```

**Resposta/resultado:** apresenta o título de cada música, seu álbum (quando houver), a data de lançamento e a duração. O `LEFT JOIN` mantém no resultado músicas que ainda não estejam associadas a um álbum.

### 6.2. Pesquisar artistas pelo nome

**Contexto:** um usuário deseja localizar artistas pelo nome artístico, mesmo sem saber o nome completo.

```sql
SELECT id_artista, nome_artistico, pais_origem
FROM artistas
WHERE nome_artistico LIKE '%a%'
ORDER BY nome_artistico;
```

**Resposta/resultado:** retorna os artistas cujo nome artístico contém a letra “a”. O termo entre os sinais `%` pode ser alterado para outra busca.

### 6.3. Consultar os gêneros associados a cada artista

**Contexto:** a NOIR precisa apresentar os gêneros musicais relacionados aos artistas cadastrados.

```sql
SELECT ar.nome_artistico, g.nome_genero
FROM artistas AS ar
INNER JOIN artista_genero AS ag
        ON ar.id_artista = ag.id_artista
INNER JOIN generos AS g
        ON ag.id_genero = g.id_genero
ORDER BY ar.nome_artistico, g.nome_genero;
```

**Resposta/resultado:** mostra o nome artístico e os gêneros associados a ele. O `INNER JOIN` retorna somente as associações existentes nas tabelas relacionadas.

### 6.4. Contar artistas por gênero musical

**Contexto:** a equipe deseja descobrir quantos artistas estão associados a cada gênero.

```sql
SELECT g.nome_genero,
       COUNT(ag.id_artista) AS quantidade_artistas
FROM generos AS g
LEFT JOIN artista_genero AS ag
       ON g.id_genero = ag.id_genero
GROUP BY g.id_genero, g.nome_genero
ORDER BY quantidade_artistas DESC, g.nome_genero;
```

**Resposta/resultado:** apresenta cada gênero e a quantidade de artistas relacionados. O `COUNT` realiza a contagem e o `GROUP BY` agrupa os registros por gênero.

### 6.5. Consultar usuários nascidos a partir do ano 2000

**Contexto:** a plataforma deseja filtrar os usuários pela data de nascimento.

```sql
SELECT id_usuarios, nome, email, data_nascimento
FROM usuarios
WHERE data_nascimento >= '2000-01-01'
ORDER BY data_nascimento;
```

**Resposta/resultado:** lista os usuários nascidos em 1º de janeiro de 2000 ou depois dessa data.

### 6.6. Consultar o histórico de reprodução

**Contexto:** a NOIR deseja visualizar quais músicas foram reproduzidas e por quais usuários.

```sql
SELECT u.nome AS usuario,
       m.titulo AS musica,
       h.data_hora
FROM historico_reproducao AS h
INNER JOIN usuarios AS u
        ON h.id_usuario = u.id_usuarios
INNER JOIN musicas AS m
        ON h.id_musica = m.id_musica
ORDER BY h.data_hora DESC;
```

**Resposta/resultado:** apresenta o nome do usuário, o título da música e a data e hora da reprodução, da mais recente para a mais antiga.

### 6.7. Contar reproduções por usuário

**Contexto:** a equipe deseja identificar quantas reproduções estão registradas para cada usuário.

```sql
SELECT u.nome AS usuario,
       COUNT(h.id_reproducao) AS total_reproducoes
FROM usuarios AS u
LEFT JOIN historico_reproducao AS h
       ON u.id_usuarios = h.id_usuario
GROUP BY u.id_usuarios, u.nome
ORDER BY total_reproducoes DESC, u.nome;
```

**Resposta/resultado:** mostra cada usuário e a quantidade de reproduções registradas. O `LEFT JOIN` também mantém usuários que ainda não possuem reproduções.

### 6.8. Identificar as músicas mais reproduzidas

**Contexto:** a NOIR deseja descobrir quais músicas possuem maior número de reproduções.

```sql
SELECT m.titulo AS musica,
       COUNT(h.id_reproducao) AS total_reproducoes
FROM musicas AS m
LEFT JOIN historico_reproducao AS h
       ON m.id_musica = h.id_musica
GROUP BY m.id_musica, m.titulo
ORDER BY total_reproducoes DESC, m.titulo;
```

**Resposta/resultado:** apresenta as músicas em ordem decrescente de reproduções, permitindo identificar as mais ouvidas.

### 6.9. Filtrar reproduções por período

**Contexto:** a equipe deseja consultar as reproduções registradas durante o ano de 2026.

```sql
SELECT id_reproducao, id_usuario, id_musica, data_hora
FROM historico_reproducao
WHERE data_hora BETWEEN '2026-01-01 00:00:00'
                    AND '2026-12-31 23:59:59'
ORDER BY data_hora;
```

**Resposta/resultado:** retorna as reproduções realizadas entre o início de 2026 e o fim do dia 31 de dezembro de 2026. O `BETWEEN` considera os dois limites informados.

### 6.10. Listar as músicas favoritas dos usuários

**Contexto:** a plataforma deseja consultar quais músicas foram adicionadas aos favoritos por cada usuário.

```sql
SELECT u.nome AS usuario,
       m.titulo AS musica,
       f.data_favorito
FROM favoritos AS f
INNER JOIN usuarios AS u
        ON f.id_usuario = u.id_usuarios
INNER JOIN musicas AS m
        ON f.id_musica = m.id_musica
ORDER BY u.nome, m.titulo;
```

**Resposta/resultado:** mostra o usuário, a música favoritada e a data em que ela foi adicionada à lista de favoritos.

### 6.11. Contar favoritos por música

**Contexto:** a NOIR deseja descobrir quais músicas são mais adicionadas aos favoritos.

```sql
SELECT m.titulo AS musica,
       COUNT(f.id_usuario) AS total_favoritos
FROM musicas AS m
LEFT JOIN favoritos AS f
       ON m.id_musica = f.id_musica
GROUP BY m.id_musica, m.titulo
ORDER BY total_favoritos DESC, m.titulo;
```

**Resposta/resultado:** apresenta cada música e a quantidade de usuários que a favoritaram, começando pelas mais favoritada.

### 6.12. Encontrar músicas com mais de três minutos

**Contexto:** um usuário deseja encontrar músicas com duração superior a três minutos.

```sql
SELECT titulo, duracao_segundos
FROM musicas
WHERE duracao_segundos > 180
ORDER BY duracao_segundos DESC;
```

**Resposta/resultado:** lista as músicas com mais de 180 segundos de duração, da mais longa para a mais curta.

### 6.13. Contar músicas por álbum

**Contexto:** a plataforma deseja apresentar quantas músicas estão cadastradas em cada álbum.

```sql
SELECT a.titulo AS album,
       COUNT(m.id_musica) AS quantidade_musicas
FROM albuns AS a
LEFT JOIN musicas AS m
       ON a.id_album = m.id_album
GROUP BY a.id_album, a.titulo
ORDER BY quantidade_musicas DESC, a.titulo;
```

**Resposta/resultado:** mostra o nome de cada álbum e a quantidade de músicas associadas a ele, inclusive álbuns sem músicas cadastradas.

### 6.14. Somar o tempo de músicas reproduzidas por usuário

**Contexto:** a NOIR deseja estimar o tempo total das músicas registradas no histórico de cada usuário.

```sql
SELECT u.nome AS usuario,
       COALESCE(SUM(m.duracao_segundos), 0) AS total_segundos_reproduzidos
FROM usuarios AS u
LEFT JOIN historico_reproducao AS h
       ON u.id_usuarios = h.id_usuario
LEFT JOIN musicas AS m
       ON h.id_musica = m.id_musica
GROUP BY u.id_usuarios, u.nome
ORDER BY total_segundos_reproduzidos DESC;
```

**Resposta/resultado:** apresenta o tempo total, em segundos, das músicas registradas no histórico de cada usuário. O `SUM` soma as durações e o `COALESCE` retorna zero quando não há reproduções.

### 6.15. Encontrar usuários sem reproduções registradas

**Contexto:** a equipe deseja identificar usuários que ainda não possuem nenhuma reprodução no histórico.

```sql
SELECT u.id_usuarios, u.nome, u.email
FROM usuarios AS u
LEFT JOIN historico_reproducao AS h
       ON u.id_usuarios = h.id_usuario
WHERE h.id_reproducao IS NULL
ORDER BY u.nome;
```

**Resposta/resultado:** lista os usuários que não possuem registros na tabela `historico_reproducao`.

### Recursos SQL utilizados

As consultas utilizam `SELECT`, `WHERE`, `LIKE`, `INNER JOIN`, `LEFT JOIN`, `GROUP BY`, `ORDER BY`, `BETWEEN`, `COUNT`, `SUM`, `COALESCE` e `IS NULL`.

> **Sobre as respostas:** os textos acima descrevem o resultado que cada consulta deve apresentar. Para documentar as respostas com valores reais, execute os comandos depois de inserir os dados e registre os resultados exibidos pelo MySQL Workbench. Não foram inventados números ou nomes de resultados.

------------------------------------------------------------------------


## 🏁 7. Conclusão

O projeto **NOIR** demonstra como um banco de dados relacional pode
organizar as informações de uma plataforma de streaming musical.

Com 13 tabelas, o modelo contempla usuários, artistas, gêneros musicais,
redes sociais de artistas, álbuns, músicas, playlists, favoritos e
histórico de reprodução.

A utilização de chaves primárias, chaves estrangeiras e técnicas de
normalização contribui para a integridade, a consistência e a
organização dos dados.

Dessa forma, o NOIR apresenta uma estrutura preparada para representar
as principais funcionalidades de uma plataforma musical e servir como
base para uma futura aplicação desenvolvida em Java e integrada ao
MySQL.

------------------------------------------------------------------------

**NOIR --- Música organizada, dados conectados.**
# Atividade III - SEDUC DEST2

### Planejar, criar e testar um banco de dados para um domínio qualquer.

#  NOIR

**Banco de Dados para uma Plataforma de Streaming Musical**

------------------------------------------------------------------------

##  1. Contextualização

O **NOIR** é um projeto de banco de dados para uma plataforma fictícia
de streaming musical. O sistema organiza informações sobre usuários,
artistas, gêneros musicais, álbuns, músicas, playlists, favoritos e
histórico de reprodução.

O projeto utiliza um banco de dados relacional desenvolvido em MySQL,
com o propósito de manter as informações estruturadas, facilitar
consultas e garantir maior consistência dos dados.

##  2. Problemas sem um Banco de Dados

Sem um Sistema Gerenciador de Banco de Dados (SGBD) relacional, a
plataforma poderia enfrentar problemas como:

-   **Desorganização:** informações armazenadas de maneira dispersa.
-   **Duplicidade:** registros repetidos de usuários, artistas e
    músicas.
-   **Perda de informações:** dificuldade para manter os dados seguros.
-   **Consultas difíceis:** maior dificuldade para localizar músicas e
    playlists.
-   **Inconsistência:** informações divergentes entre registros.
-   **Manutenção complicada:** dificuldade para atualizar e administrar
    os dados.

##  3. Melhorias com um Banco de Dados Relacional

Com o uso do MySQL, o NOIR passa a contar com uma estrutura organizada e
integrada, proporcionando:

-   **Organização:** informações distribuídas em tabelas específicas.
-   **Integridade:** chaves primárias e estrangeiras para manter a
    consistência dos relacionamentos.
-   **Redução de redundâncias:** menos repetições desnecessárias.
-   **Consultas eficientes:** facilidade para pesquisar músicas,
    artistas, álbuns e playlists.
-   **Histórico de reprodução:** registro das músicas reproduzidas pelos
    usuários.
-   **Manutenção facilitada:** maior controle sobre os dados
    armazenados.

##  4. Estrutura do Banco de Dados

O banco de dados NOIR é composto por **13 tabelas**, cada uma responsável por armazenar um conjunto específico de informações.

### 4.1. `usuarios`

Armazena os dados dos usuários cadastrados na plataforma.

  Campo               Tipo           Descrição
  ------------------- -------------- --------------------------------------
  `id_usuarios`       INT            Identificador único do usuário (PK).
  `nome`              VARCHAR(250)   Nome completo.
  `email`             VARCHAR(150)   E-mail do usuário.
  `senha`             CHAR(50)       Senha armazenada no cadastro.
  `data_nascimento`   DATE           Data de nascimento.

  **Observação:** esta descrição segue o script `noir_usuarios.sql` enviado.

### 4.2. `artistas`

Armazena as informações dos artistas disponíveis na plataforma.

  Campo              Tipo           Descrição
  ------------------ -------------- --------------------------------------
  `id_artista`       INT            Identificador único do artista (PK).
  `nome_artistico`   VARCHAR(120)   Nome artístico.
  `biografia`        VARCHAR(150)   Biografia do artista.
  `pais_origem`      VARCHAR(80)    País de origem.

### 4.3. `generos`

Armazena os gêneros musicais disponíveis.

  Campo           Tipo           Descrição
  --------------- -------------- -------------------------------------
  `id_genero`     INT            Identificador único do gênero (PK).
  `nome_genero`   VARCHAR(80)    Nome do gênero musical.
  `descricao`     VARCHAR(255)   Descrição do gênero.

### 4.4. `artista_genero`

Relaciona artistas aos seus respectivos gêneros musicais.

  Campo          Tipo   Descrição
  -------------- ------ -------------------------------------
  `id_artista`   INT    Identificador do artista (PK e FK).
  `id_genero`    INT    Identificador do gênero (PK e FK).

### 4.5. `artista_redes_sociais`

Armazena os links das redes sociais dos artistas.

  Campo             Tipo           Descrição
  ----------------- -------------- ------------------------------------
  `id_rede`         INT            Identificador da rede social (PK).
  `id_artista`      INT            Artista relacionado (FK).
  `nome_rede`       VARCHAR(50)    Nome da rede social.
  `link_perfil`     VARCHAR(255)   Link do perfil do artista.

  A combinação entre artista e rede social é única, evitando cadastrar
  duas vezes a mesma plataforma para o mesmo artista.

### 4.6. `albuns`

Armazena os álbuns musicais cadastrados.

  Campo               Tipo           Descrição
  ------------------- -------------- ------------------------------------
  `id_album`          INT            Identificador único do álbum (PK).
  `titulo`            VARCHAR(150)   Título do álbum.
  `data_lancamento`   DATE           Data de lançamento.
  `capa_url`          VARCHAR(500)   Link da imagem da capa.

### 4.7. `album_artista`

Relaciona os álbuns aos artistas responsáveis por eles.

  Campo          Tipo   Descrição
  -------------- ------ -------------------------------------
  `id_album`     INT    Identificador do álbum (PK e FK).
  `id_artista`   INT    Identificador do artista (PK e FK).

### 4.8. `musicas`

Armazena as informações das músicas disponíveis.

  Campo                Tipo           Descrição
  -------------------- -------------- -------------------------------------
  `id_musica`          INT            Identificador único da música (PK).
  `id_album`           INT            Álbum relacionado (FK, opcional).
  `titulo`             VARCHAR(150)   Título da música.
  `duracao_segundos`   INT            Duração em segundos.
  `data_lancamento`    DATE           Data de lançamento.
  `arquivo_url`        VARCHAR(500)   Link do arquivo de áudio.

### 4.9. `musica_artista`

Relaciona as músicas aos artistas responsáveis por sua criação ou
interpretação.

  Campo          Tipo   Descrição
  -------------- ------ -------------------------------------
  `id_musica`    INT    Identificador da música (PK e FK).
  `id_artista`   INT    Identificador do artista (PK e FK).

### 4.10. `playlists`

Armazena as playlists criadas pelos usuários.

  Campo               Tipo           Descrição
  ------------------- -------------- -----------------------------------------
  `id_playlist`       INT            Identificador único da playlist (PK).
  `id_usuario`        INT            Usuário responsável pela playlist (FK).
  `nome_playlist`     VARCHAR(100)   Nome da playlist.
  `descricao`         TEXT           Descrição da playlist.
  `data_criacao`      DATE           Data de criação.

### 4.11. `playlist_musica`

Armazena as músicas adicionadas às playlists e suas posições.

  -----------------------------------------------------------------------
  Campo                   Tipo                    Descrição
  ----------------------- ----------------------- -----------------------
  `id_playlist`           INT                     Identificador da
                                                  playlist (PK e FK).

  `id_musica`             INT                     Identificador da música
                                                  (PK e FK).

  `posicao`               INT                     Posição da música na
                                                  playlist.

  `data_adicao`           DATETIME                Data e hora em que a
                                                  música foi adicionada.
  -----------------------------------------------------------------------

### 4.12. `favoritos`

Armazena as músicas favoritas dos usuários.

  -----------------------------------------------------------------------
  Campo                   Tipo                    Descrição
  ----------------------- ----------------------- -----------------------
  `id_usuario`            INT                     Identificador do
                                                  usuário (PK e FK).

  `id_musica`             INT                     Identificador da música
                                                  (PK e FK).

  `data_favorito`         DATETIME                Data e hora em que a
                                                  música foi favoritada.
  -----------------------------------------------------------------------

### 4.13. `historico_reproducao`

Registra as reproduções realizadas pelos usuários.

  Campo             Tipo       Descrição
  ----------------- ---------- -----------------------------------------
  `id_reproducao`   INT        Identificador único da reprodução (PK).
  `id_usuario`      INT        Usuário que reproduziu a música (FK).
  `id_musica`       INT        Música reproduzida (FK).
  `data_hora`       DATETIME   Data e hora da reprodução.

**Legenda:** - **PK (Primary Key):** chave primária que identifica um
registro. - **FK (Foreign Key):** chave estrangeira que relaciona uma
tabela a outra.

------------------------------------------------------------------------



## 📐 5. Aplicação das Formas Normais

A normalização organiza os dados para reduzir repetições desnecessárias
e evitar problemas de inserção, atualização e exclusão.

No projeto NOIR, a estrutura das tabelas busca aplicar as quatro
primeiras Formas Normais.

### 5.1. 1FN --- Primeira Forma Normal

**Objetivo:** garantir que cada campo armazene um único valor, sem
listas de informações na mesma coluna.

**Aplicação no NOIR:** os gêneros dos artistas, as redes sociais e as
músicas das playlists são organizados em tabelas específicas.

**Benefício:** dados mais organizados e fáceis de consultar.

### 5.2. 2FN --- Segunda Forma Normal

**Objetivo:** garantir que os atributos não chave dependam da chave
primária completa, sem dependências parciais.

**Aplicação no NOIR:** a tabela `musica_artista` utiliza uma chave
primária composta por `id_musica` e `id_artista`. O título da música e o
nome artístico permanecem em suas respectivas tabelas.

**Benefício:** redução de redundâncias e melhor organização das
informações.

### 5.3. 3FN --- Terceira Forma Normal

**Objetivo:** evitar dependências transitivas inadequadas entre
atributos não chave.

**Aplicação no NOIR:** os dados dos artistas são armazenados na tabela
`artistas`, enquanto os nomes e as descrições dos gêneros ficam na
tabela `generos`.

**Benefício:** menor risco de inconsistências e manutenção facilitada.

### 5.4. 4FN --- Quarta Forma Normal

**Objetivo:** evitar redundâncias causadas por informações
multivaloradas independentes.

**Aplicação no NOIR:** os gêneros dos artistas são armazenados na tabela
`artista_genero`, enquanto as redes sociais ficam na tabela
`artista_redes_sociais`.

**Benefício:** evita combinações redundantes entre gêneros musicais e
redes sociais.

### Resumo da Normalização

  -----------------------------------------------------------------------
  Forma Normal            Aplicação no NOIR       Benefício
  ----------------------- ----------------------- -----------------------
  **1FN**                 Armazenamento           Organização dos dados.
                          individual das          
                          informações.            

  **2FN**                 Separação dos atributos Redução de
                          de músicas e artistas.  redundâncias.

  **3FN**                 Separação das           Maior consistência.
                          informações de artistas 
                          e gêneros.              

  **4FN**                 Separação dos gêneros e Menos combinações
                          das redes sociais.      redundantes.
  -----------------------------------------------------------------------

> **Observação:** a confirmação de cada Forma Normal depende da análise
> das dependências funcionais e multivaloradas do modelo. A separação
> das tabelas contribui para a normalização, mas não substitui essa
> verificação.

------------------------------------------------------------------------



------------------------------------------------------------------------

## 6. Consultas SQL

As consultas abaixo representam situações do cotidiano da plataforma NOIR. Elas permitem pesquisar o catálogo, relacionar artistas e gêneros, acompanhar reproduções e analisar músicas favoritas.

> **Importante:** as consultas foram elaboradas com base na estrutura descrita neste README. Os resultados dependem dos registros cadastrados no banco; execute cada consulta no MySQL Workbench para conferir os valores reais.

### 6.1. Listar músicas e seus álbuns

**Contexto:** a plataforma precisa exibir o catálogo musical e informar a qual álbum cada música pertence.

```sql
USE noir;

SELECT m.id_musica,
       m.titulo AS musica,
       a.titulo AS album,
       m.data_lancamento,
       m.duracao_segundos
FROM musicas AS m
LEFT JOIN albuns AS a ON m.id_album = a.id_album
ORDER BY m.titulo;
```

**Resposta/resultado:** apresenta o título de cada música, seu álbum (quando houver), a data de lançamento e a duração. O `LEFT JOIN` mantém no resultado músicas que ainda não estejam associadas a um álbum.

### 6.2. Pesquisar artistas pelo nome

**Contexto:** um usuário deseja localizar artistas pelo nome artístico, mesmo sem saber o nome completo.

```sql
SELECT id_artista, nome_artistico, pais_origem
FROM artistas
WHERE nome_artistico LIKE '%a%'
ORDER BY nome_artistico;
```

**Resposta/resultado:** retorna os artistas cujo nome artístico contém a letra “a”. O termo entre os sinais `%` pode ser alterado para outra busca.

### 6.3. Consultar os gêneros associados a cada artista

**Contexto:** a NOIR precisa apresentar os gêneros musicais relacionados aos artistas cadastrados.

```sql
SELECT ar.nome_artistico, g.nome_genero
FROM artistas AS ar
INNER JOIN artista_genero AS ag
        ON ar.id_artista = ag.id_artista
INNER JOIN generos AS g
        ON ag.id_genero = g.id_genero
ORDER BY ar.nome_artistico, g.nome_genero;
```

**Resposta/resultado:** mostra o nome artístico e os gêneros associados a ele. O `INNER JOIN` retorna somente as associações existentes nas tabelas relacionadas.

### 6.4. Contar artistas por gênero musical

**Contexto:** a equipe deseja descobrir quantos artistas estão associados a cada gênero.

```sql
SELECT g.nome_genero,
       COUNT(ag.id_artista) AS quantidade_artistas
FROM generos AS g
LEFT JOIN artista_genero AS ag
       ON g.id_genero = ag.id_genero
GROUP BY g.id_genero, g.nome_genero
ORDER BY quantidade_artistas DESC, g.nome_genero;
```

**Resposta/resultado:** apresenta cada gênero e a quantidade de artistas relacionados. O `COUNT` realiza a contagem e o `GROUP BY` agrupa os registros por gênero.

### 6.5. Consultar usuários nascidos a partir do ano 2000

**Contexto:** a plataforma deseja filtrar os usuários pela data de nascimento.

```sql
SELECT id_usuarios, nome, email, data_nascimento
FROM usuarios
WHERE data_nascimento >= '2000-01-01'
ORDER BY data_nascimento;
```

**Resposta/resultado:** lista os usuários nascidos em 1º de janeiro de 2000 ou depois dessa data.

### 6.6. Consultar o histórico de reprodução

**Contexto:** a NOIR deseja visualizar quais músicas foram reproduzidas e por quais usuários.

```sql
SELECT u.nome AS usuario,
       m.titulo AS musica,
       h.data_hora
FROM historico_reproducao AS h
INNER JOIN usuarios AS u
        ON h.id_usuario = u.id_usuarios
INNER JOIN musicas AS m
        ON h.id_musica = m.id_musica
ORDER BY h.data_hora DESC;
```

**Resposta/resultado:** apresenta o nome do usuário, o título da música e a data e hora da reprodução, da mais recente para a mais antiga.

### 6.7. Contar reproduções por usuário

**Contexto:** a equipe deseja identificar quantas reproduções estão registradas para cada usuário.

```sql
SELECT u.nome AS usuario,
       COUNT(h.id_reproducao) AS total_reproducoes
FROM usuarios AS u
LEFT JOIN historico_reproducao AS h
       ON u.id_usuarios = h.id_usuario
GROUP BY u.id_usuarios, u.nome
ORDER BY total_reproducoes DESC, u.nome;
```

**Resposta/resultado:** mostra cada usuário e a quantidade de reproduções registradas. O `LEFT JOIN` também mantém usuários que ainda não possuem reproduções.

### 6.8. Identificar as músicas mais reproduzidas

**Contexto:** a NOIR deseja descobrir quais músicas possuem maior número de reproduções.

```sql
SELECT m.titulo AS musica,
       COUNT(h.id_reproducao) AS total_reproducoes
FROM musicas AS m
LEFT JOIN historico_reproducao AS h
       ON m.id_musica = h.id_musica
GROUP BY m.id_musica, m.titulo
ORDER BY total_reproducoes DESC, m.titulo;
```

**Resposta/resultado:** apresenta as músicas em ordem decrescente de reproduções, permitindo identificar as mais ouvidas.

### 6.9. Filtrar reproduções por período

**Contexto:** a equipe deseja consultar as reproduções registradas durante o ano de 2026.

```sql
SELECT id_reproducao, id_usuario, id_musica, data_hora
FROM historico_reproducao
WHERE data_hora BETWEEN '2026-01-01 00:00:00'
                    AND '2026-12-31 23:59:59'
ORDER BY data_hora;
```

**Resposta/resultado:** retorna as reproduções realizadas entre o início de 2026 e o fim do dia 31 de dezembro de 2026. O `BETWEEN` considera os dois limites informados.

### 6.10. Listar as músicas favoritas dos usuários

**Contexto:** a plataforma deseja consultar quais músicas foram adicionadas aos favoritos por cada usuário.

```sql
SELECT u.nome AS usuario,
       m.titulo AS musica,
       f.data_favorito
FROM favoritos AS f
INNER JOIN usuarios AS u
        ON f.id_usuario = u.id_usuarios
INNER JOIN musicas AS m
        ON f.id_musica = m.id_musica
ORDER BY u.nome, m.titulo;
```

**Resposta/resultado:** mostra o usuário, a música favoritada e a data em que ela foi adicionada à lista de favoritos.

### 6.11. Contar favoritos por música

**Contexto:** a NOIR deseja descobrir quais músicas são mais adicionadas aos favoritos.

```sql
SELECT m.titulo AS musica,
       COUNT(f.id_usuario) AS total_favoritos
FROM musicas AS m
LEFT JOIN favoritos AS f
       ON m.id_musica = f.id_musica
GROUP BY m.id_musica, m.titulo
ORDER BY total_favoritos DESC, m.titulo;
```

**Resposta/resultado:** apresenta cada música e a quantidade de usuários que a favoritaram, começando pelas mais favoritada.

### 6.12. Encontrar músicas com mais de três minutos

**Contexto:** um usuário deseja encontrar músicas com duração superior a três minutos.

```sql
SELECT titulo, duracao_segundos
FROM musicas
WHERE duracao_segundos > 180
ORDER BY duracao_segundos DESC;
```

**Resposta/resultado:** lista as músicas com mais de 180 segundos de duração, da mais longa para a mais curta.

### 6.13. Contar músicas por álbum

**Contexto:** a plataforma deseja apresentar quantas músicas estão cadastradas em cada álbum.

```sql
SELECT a.titulo AS album,
       COUNT(m.id_musica) AS quantidade_musicas
FROM albuns AS a
LEFT JOIN musicas AS m
       ON a.id_album = m.id_album
GROUP BY a.id_album, a.titulo
ORDER BY quantidade_musicas DESC, a.titulo;
```

**Resposta/resultado:** mostra o nome de cada álbum e a quantidade de músicas associadas a ele, inclusive álbuns sem músicas cadastradas.

### 6.14. Somar o tempo de músicas reproduzidas por usuário

**Contexto:** a NOIR deseja estimar o tempo total das músicas registradas no histórico de cada usuário.

```sql
SELECT u.nome AS usuario,
       COALESCE(SUM(m.duracao_segundos), 0) AS total_segundos_reproduzidos
FROM usuarios AS u
LEFT JOIN historico_reproducao AS h
       ON u.id_usuarios = h.id_usuario
LEFT JOIN musicas AS m
       ON h.id_musica = m.id_musica
GROUP BY u.id_usuarios, u.nome
ORDER BY total_segundos_reproduzidos DESC;
```

**Resposta/resultado:** apresenta o tempo total, em segundos, das músicas registradas no histórico de cada usuário. O `SUM` soma as durações e o `COALESCE` retorna zero quando não há reproduções.

### 6.15. Encontrar usuários sem reproduções registradas

**Contexto:** a equipe deseja identificar usuários que ainda não possuem nenhuma reprodução no histórico.

```sql
SELECT u.id_usuarios, u.nome, u.email
FROM usuarios AS u
LEFT JOIN historico_reproducao AS h
       ON u.id_usuarios = h.id_usuario
WHERE h.id_reproducao IS NULL
ORDER BY u.nome;
```

**Resposta/resultado:** lista os usuários que não possuem registros na tabela `historico_reproducao`.

### Recursos SQL utilizados

As consultas utilizam `SELECT`, `WHERE`, `LIKE`, `INNER JOIN`, `LEFT JOIN`, `GROUP BY`, `ORDER BY`, `BETWEEN`, `COUNT`, `SUM`, `COALESCE` e `IS NULL`.

> **Sobre as respostas:** os textos acima descrevem o resultado que cada consulta deve apresentar. Para documentar as respostas com valores reais, execute os comandos depois de inserir os dados e registre os resultados exibidos pelo MySQL Workbench. Não foram inventados números ou nomes de resultados.

------------------------------------------------------------------------


## 🏁 7. Conclusão

O projeto **NOIR** demonstra como um banco de dados relacional pode
organizar as informações de uma plataforma de streaming musical.

Com 13 tabelas, o modelo contempla usuários, artistas, gêneros musicais,
redes sociais de artistas, álbuns, músicas, playlists, favoritos e
histórico de reprodução.

A utilização de chaves primárias, chaves estrangeiras e técnicas de
normalização contribui para a integridade, a consistência e a
organização dos dados.

Dessa forma, o NOIR apresenta uma estrutura preparada para representar
as principais funcionalidades de uma plataforma musical e servir como
base para uma futura aplicação desenvolvida em Java e integrada ao
MySQL.

------------------------------------------------------------------------

**NOIR --- Música organizada, dados conectados.**
