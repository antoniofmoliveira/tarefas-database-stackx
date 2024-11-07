## tarefa 1 -- organização para banco de dados  

```sql
-- tabela de usuarios, email tem de ser único, permite homônimos
CREATE TABLE IF NOT EXISTS usuarios (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    data_nascimento DATE NOT NULL,
    telefone VARCHAR(255) NOT NULL,
    cpf VARCHAR(11) NOT NULL,
    endereco VARCHAR(255) NOT NULL,
    cidade VARCHAR(255) NOT NULL,
    uf VARCHAR(2) NOT NULL,
    pais VARCHAR(255) NOT NULL,
    cep VARCHAR(8) NOT NULL,
    senha VARCHAR(72) NOT NULL,
    created_at DATE NOT NULL,
    updated_at DATE NOT NULL,
    deleted_at DATE
);
```

```sql
-- tabela de lugares para se hospedar, nome tem de ser único
CREATE TABLE IF NOT EXISTS lugares (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(255) UNIQUE NOT NULL,
    descricao VARCHAR(255) NOT NULL,
    endereco VARCHAR(255) NOT NULL,
    cidade VARCHAR(255) NOT NULL,
    uf VARCHAR(2) NOT NULL,
    pais VARCHAR(255) NOT NULL,
    cep VARCHAR(8) NOT NULL,
    created_by INTEGER NOT NULL,
    created_at DATE NOT NULL,
    updated_at DATE NOT NULL,
    deleted_at DATE,
    FOREIGN KEY (created_by) REFERENCES usuarios (id)
);
```

```sql
-- tabela hospedagens, 
CREATE TABLE IF NOT EXISTS hospedagens (
    id SERIAL PRIMARY KEY,
    id_lugar INTEGER NOT NULL,
    id_usuario INTEGER NOT NULL,
    data_inicio DATE NOT NULL,
    data_fim DATE NOT NULL CHECK (data_fim > data_inicio),
    valor DECIMAL(10, 2) NOT NULL,
    no_show BOOLEAN NOT NULL,
    created_by INTEGER NOT NULL,
    created_at DATE NOT NULL,
    updated_at DATE NOT NULL,
    deleted_at DATE,
    FOREIGN KEY (id_lugar) REFERENCES lugares (id),
    FOREIGN KEY (id_usuario) REFERENCES usuarios (id),
    FOREIGN KEY (created_by) REFERENCES usuarios (id)
);
```

```sql
-- não permite registros de hospedagens duplicados
CREATE INDEX IF NOT EXISTS UNIQUE idx_hospedagens ON hospedagens (id_lugar, id_usuario, data_inicio, data_fim);
```

```sql
-- tabela avaliações, vincula avaliação a cada hospedagem
CREATE TABLE IF NOT EXISTS avaliacoes (
    id SERIAL PRIMARY KEY,
    id_hospedagens INTEGER NOT NULL,
    id_usuario INTEGER NOT NULL,
    estrelas INTEGER NOT NULL,
    comentario VARCHAR(255) NOT NULL,
    created_at DATE NOT NULL,
    updated_at DATE NOT NULL,
    deleted_at DATE,
    FOREIGN KEY (id_hospedagens) REFERENCES hospedagens (id),
    FOREIGN KEY (id_usuario) REFERENCES usuarios (id)
);
```

As tabelas foram criadas usando as regras básicas de normalização em SGDB.

As 3 últimas colunas de cada tabela preparam-nas para utilização em ORM.
