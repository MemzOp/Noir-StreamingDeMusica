# Atividade III - SEDUC DEST2

### Planejar, criar e testar um banco de dados para um domínio qualquer.

# 🎧 NOIR

**Banco de Dados para uma Plataforma de Streaming Musical**

------------------------------------------------------------------------

## 📌 1. Contextualização

O **NOIR** é um projeto de banco de dados para uma plataforma fictícia
de streaming musical. O sistema organiza informações sobre usuários,
artistas, gêneros musicais, álbuns, músicas, playlists, favoritos e
histórico de reprodução.

O projeto utiliza um banco de dados relacional desenvolvido em MySQL,
com o propósito de manter as informações estruturadas, facilitar
consultas e garantir maior consistência dos dados.

## ⚠️ 2. Problemas sem um Banco de Dados

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

## ✅ 3. Melhorias com um Banco de Dados Relacional

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

## 🗄️ 4. Estrutura do Banco de Dados

O banco de dados NOIR é composto por **13 tabelas**, cada uma
responsável por armazenar um conjunto específico de informações.

### 4.1. `usuarios`

Armazena os dados dos usuários cadastrados na plataforma.

  Campo               Tipo           Descrição
  ------------------- -------------- --------------------------------------
  `id_usuario`        INT            Identificador único do usuário (PK).
  `nome`              VARCHAR(100)   Nome completo.
  `email`             VARCHAR(150)   E-mail único para identificação.
  `senha_hash`        VARCHAR(255)   Hash da senha do usuário.
  `data_nascimento`   DATE           Data de nascimento.
  `data_cadastro`     DATETIME       Data e hora do cadastro.

### 4.2. `artistas`

Armazena as informações dos artistas disponíveis na plataforma.

  Campo              Tipo           Descrição
  ------------------ -------------- --------------------------------------
  `id_artista`       INT            Identificador único do artista (PK).
  `nome_artistico`   VARCHAR(120)   Nome artístico.
  `biografia`        TEXT           Biografia do artista.
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

  Campo          Tipo           Descrição
  -------------- -------------- ------------------------------------
  `id_rede`      INT            Identificador da rede social (PK).
  `id_artista`   INT            Artista relacionado (FK).
  `plataforma`   VARCHAR(50)    Nome da rede social.
  `url`          VARCHAR(500)   Link do perfil.

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

  Campo            Tipo           Descrição
  ---------------- -------------- -----------------------------------------
  `id_playlist`    INT            Identificador único da playlist (PK).
  `id_usuario`     INT            Usuário responsável pela playlist (FK).
  `nome`           VARCHAR(120)   Nome da playlist.
  `descricao`      VARCHAR(255)   Descrição da playlist.
  `data_criacao`   DATETIME       Data e hora da criação.

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
  `id_reproducao`   BIGINT     Identificador único da reprodução (PK).
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

## 🏁 6. Conclusão

O projeto **NOIR** demonstra como um banco de dados relacional pode
organizar as informações de uma plataforma de streaming musical.

Com 13 tabelas, o modelo contempla usuários, artistas, gêneros musicais,
álbuns, músicas, playlists, favoritos e histórico de reprodução.

A utilização de chaves primárias, chaves estrangeiras e técnicas de
normalização contribui para a integridade, a consistência e a
organização dos dados.

Dessa forma, o NOIR apresenta uma estrutura preparada para representar
as principais funcionalidades de uma plataforma musical e servir como
base para uma futura aplicação desenvolvida em Java e integrada ao
MySQL.

------------------------------------------------------------------------

**NOIR --- Música organizada, dados conectados.**
