
-- tarefa 2 -- tabelas em query

```sql
CREATE TABLE aluno (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    data_nascimento DATE NOT NULL
);
```

```sql
CREATE TABLE professor (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    data_nascimento DATE NOT NULL
);
```

```sql
CREATE TABLE materia (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    id_professor INTEGER NOT NULL,
    FOREIGN KEY (id_professor) REFERENCES professor (id)
);
```

```sql
CREATE TABLE IF NOT EXISTS provas (
    id_aluno INTEGER NOT NULL,
    id_materia INTEGER NOT NULL,
    nota DECIMAL(2, 2) NOT NULL,
    data_da_prova DATE NOT NULL,
    PRIMARY KEY (id_aluno, id_materia, data_da_prova),
    FOREIGN KEY (id_aluno) REFERENCES aluno (id),
    FOREIGN KEY (id_materia) REFERENCES materia (id)
);
```

```sql
-- criar 3 alunos
INSERT INTO aluno (id, nome, data_nascimento)
VALUES (1, 'Antonio', '2000-01-01'),
    (2, 'Maria', '2001-01-01'),
    (3, 'Jose', '2002-01-01');
```

```sql
-- criar 1 professor
INSERT INTO professor (id, nome, data_nascimento)
VALUES (1, 'Joaquim', '1990-01-01');
```

```sql
-- criar 1 materia
INSERT INTO materia (id, nome, id_professor)
VALUES (1, 'Matematica', 1);
```

```sql
-- criar 1 prova para cada aluno nessa materia
INSERT INTO provas (id_aluno, id_materia, nota, data_da_prova)
VALUES (1, 1, 10.0, '2022-01-01'),
    (2, 1, 9.1, '2022-01-01'),
    (3, 1, 8.2, '2022-01-01');
```

```sql
-- dia que nota eles tiraram
SELECT a.nome,
    b.nome as materia,
    c.nota,
    c.data_da_prova
FROM aluno a
    JOIN provas c ON c.id_aluno = a.id
    JOIN materia b ON b.id = c.id_materia
WHERE c.data_da_prova = '2022-01-01';
```

Alteramos os tipo de dado para `DATE` nos campos `data_nascimento` porque não cabia usar `numero` conforme proposto pela tarefa.
