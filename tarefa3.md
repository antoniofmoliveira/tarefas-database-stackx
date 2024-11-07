## -- tarefa 3 - item de um CRUD

```sql
CREATE TABLE IF NOT EXISTS usuarios (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    senha VARCHAR(255) NOT NULL
);
```

```sql
-- Create
INSERT INTO usuarios (id, nome, email, senha)
VALUES (1, 'Antonio', 'G4TqD@example.com', 'hash');
```

```sql
-- Read all
SELECT *
FROM usuarios;
```

```sql
-- Read one
SELECT nome,
    email
FROM usuarios
WHERE email = 'G4TqD@example.com';
```

```sql
-- Update
UPDATE usuarios
SET nome = 'Jose'
WHERE id = 1;
```

```sql
-- Delete
DELETE FROM usuarios
WHERE id = 1;
```
