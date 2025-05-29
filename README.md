# Sistema de Gestão de Professores e Disciplinas

Este repositório contém um sistema básico de gestão de professores e disciplinas, onde você pode adicionar, editar e consultar informações relacionadas a professores e suas disciplinas. A API foi construída com Express e MongoDB para armazenar os dados.

## Endpoints Disponíveis

1. **/professor**
   - `POST`: Adicionar um novo professor
   - `GET`: Obter a lista de todos os professores
   - `PUT`: Atualizar as informações de um professor
2. **/disciplina**
   - `POST`: Adicionar uma nova disciplina
   - `GET`: Obter a lista de todas as disciplinas
3. **/professor_has_disciplina**
   - `POST`: Associar um professor a uma disciplina

## Como Rodar o Sistema

### Pré-requisitos

- Node.js
- MongoDB

### Passos para rodar o sistema

1. Clone o repositório.
2. Instale as dependências com `npm install`.
3. Inicie o servidor com `npm start`.
4. A API ficará disponível em `http://localhost:3001`.

## Comandos Executados e Saídas

### 1. Adicionando Professores

#### Comando:
```bash
curl -X POST http://localhost:3001/professor -H "Content-Type: application/json" -d "{\"nome\": \"Henrique Louro\", \"email\": \"henrique.louro@fatec.sp.gov.br\", \"cpf\": \"07494812857\"}"
````

#### Saída:

```json
{
  "nome": "Henrique Louro",
  "email": "henrique.louro@fatec.sp.gov.br",
  "cpf": "07494812857",
  "_id": "6838df7aa87d4d0ccce106ac",
  "__v": 0
}
```

#### Comando:

```bash
curl -X POST http://localhost:3001/professor -H "Content-Type: application/json" -d "{\"nome\": \"Carlos Silva\", \"email\": \"carlos.silva@fatec.sp.gov.br\", \"cpf\": \"63479695051\"}"
```

#### Saída:

```json
{
  "nome": "Carlos Silva",
  "email": "carlos.silva@fatec.sp.gov.br",
  "cpf": "63479695051",
  "_id": "6838e018a87d4d0ccce106ae",
  "__v": 0
}
```

#### Comando:

```bash
curl -X POST http://localhost:3001/professor -H "Content-Type: application/json" -d "{\"nome\": \"Odete Roitman\", \"email\": \"odete.roitman@fatec.sp.gov.br\", \"cpf\": \"32082128016\"}"
```

#### Saída:

```json
{
  "nome": "Odete Roitman",
  "email": "odete.roitman@fatec.sp.gov.br",
  "cpf": "32082128016",
  "_id": "6838e02ca87d4d0ccce106b0",
  "__v": 0
}
```

#### Comando com CPF ou E-mail já existente:

```bash
curl -X POST http://localhost:3001/professor -H "Content-Type: application/json" -d "{\"nome\": \"Henrique Louro\", \"email\": \"henrique.louro@fatec.sp.gov.br\", \"cpf\": \"07494812857\"}"
```

#### Saída:

```json
{
  "message": "CPF ou e-Mail já em uso"
}
```

#### Comando com CPF inválido:

```bash
curl -X POST http://localhost:3001/professor -H "Content-Type: application/json" -d "{\"nome\": \"Henrique Louro\", \"email\": \"henrique.louro@fatec.sp.gov.br\", \"cpf\": \"12345678910\"}"
```

#### Saída:

```json
{
  "message": "12345678910 não é um CPF válido"
}
```

#### Comando com E-mail inválido:

```bash
curl -X POST http://localhost:3001/professor -H "Content-Type: application/json" -d "{\"nome\": \"Henrique Louro\", \"email\": \"henrique.louro@fatec\", \"cpf\": \"12345678910\"}"
```

#### Saída:

```json
{
  "message": "henrique.louro@fatec não é um formato de e-mail válido"
}
```

### 2. Consultando Professores

#### Comando:

```bash
curl -X GET http://localhost:3001/professor
```

#### Saída:

```json
[
  {
    "_id": "6838df7aa87d4d0ccce106ac",
    "nome": "Henrique Louro",
    "email": "henrique.louro@fatec.sp.gov.br",
    "cpf": "07494812857",
    "__v": 0
  },
  {
    "_id": "6838e018a87d4d0ccce106ae",
    "nome": "Carlos Silva",
    "email": "carlos.silva@fatec.sp.gov.br",
    "cpf": "63479695051",
    "__v": 0
  },
  {
    "_id": "6838e02ca87d4d0ccce106b0",
    "nome": "Odete Roitman",
    "email": "odete.roitman@fatec.sp.gov.br",
    "cpf": "32082128016",
    "__v": 0
  }
]
```

### 3. Atualizando um Professor

#### Comando:

```bash
curl -X PUT http://localhost:3001/professor -H "Content-Type: application/json" -d "{\"id\":\"6835017c642961ce1b3edb31\",\"nome\": \"Odetinha Roitman\", \"email\": \"odetinha.roitman@fatec.sp.gov.br\", \"cpf\": \"32082128016\"}"
```

#### Saída:

```json
{
  "message": "Professor inexistente"
}
```

### 4. Adicionando uma Disciplina

#### Comando:

```bash
curl -X POST http://localhost:3001/disciplina -H "Content-Type: application/json" -d "{\"descricao\": \"Lógica de Programação\"}"
```

#### Saída:

```json
{
  "descricao": "Lógica de Programação",
  "_id": "6838e0c3a87d4d0ccce106b9",
  "__v": 0
}
```

#### Comando para Consultar Disciplinas:

```bash
curl -X GET http://localhost:3001/disciplina
```

#### Saída:

```json
[
  {
    "_id": "6838e0c3a87d4d0ccce106b9",
    "descricao": "Lógica de Programação",
    "__v": 0
  }
]
```

### 5. Associando Professor a Disciplina

#### Comando com IDs incorretos:

```bash
curl -X POST http://localhost:3001/professor_has_disciplina -H "Content-Type: application/json" -d "{\"professor\": \"6834ff01642961ce1b3edb2d\", \"disciplina\": \"68350d5e642961ce1b3edb3c\"}"
```

#### Saída:

```json
{
  "message": "O ID do professor fornecido não existe"
}
```

#### Comando para Consultar Associações:

```bash
curl -X GET http://localhost:3001/professor_has_disciplina
```

#### Saída:

```json
[]
```

## Conclusão

O sistema permite a gestão de professores e disciplinas através de uma API RESTful, onde é possível adicionar, consultar e associar professores a disciplinas.

### Observações

* O sistema valida CPF e e-mail ao tentar cadastrar um novo professor.
* As associações de professores a disciplinas são realizadas através de IDs válidos de professores e disciplinas.

---

Feito por Victor Carbajo

```
