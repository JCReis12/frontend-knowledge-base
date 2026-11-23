# Resumo completo de estudo — Aula 05: Criando APIs para o Front-end

Este resumo aborda o desenvolvimento de APIs próprias com Node.js e Express, o tratamento de requisições e respostas HTTP, a configuração de CORS, a implementação de um CRUD completo com persistência em arquivos JSON e as melhores práticas de documentação e publicação de serviços web para consumo no front-end.

---

## 1. Fundamentos de APIs e Comunicação Cliente-Servidor

### O que é uma API e API REST?

- **API (*Application Programming Interface*):** Conjunto padronizado de rotinas, protocolos e ferramentas que permite a integração entre diferentes sistemas sem expor sua lógica interna.
- **API REST (*Representational State Transfer*):** Modelo arquitetural que utiliza o protocolo HTTP como base de comunicação. Uma API REST se organiza em torno de recursos identificados por URIs (ex.: `/api/notes`), opera de forma **stateless** (sem retenção de estado de sessão no servidor entre requisições) e transfere dados em representações estruturadas, tipicamente JSON.

### Protocolo HTTP e o Ciclo Requisição-Resposta

O protocolo HTTP rege a troca de mensagens na Web através de um ciclo bem definido:
1. **Requisição (Request):** Enviada pelo cliente (navegador/front-end). Contém o método HTTP, a URL de destino (endpoint), cabeçalhos (*headers*) de metadados e opcionalmente um corpo de dados (*body*).
2. **Processamento:** O servidor identifica a rota, executa regras de negócio, valida dados e interage com camadas de armazenamento.
3. **Resposta (Response):** Devolvida pelo servidor ao cliente contendo um código de status HTTP (ex.: 200 OK, 201 Created, 404 Not Found), cabeçalhos de resposta e os dados solicitados no corpo.

### Métodos HTTP e Convenções REST

| Método | Finalidade | Idempotente? | Seguro? | Código de Sucesso Padrão |
| --- | --- | --- | --- | --- |
| `GET` | Recuperar dados ou listar recursos | Sim | Sim | `200 OK` |
| `POST` | Criar um novo recurso | Não | Não | `201 Created` |
| `PUT` | Substituir integralmente um recurso existente | Sim | Não | `200 OK` ou `204 No Content` |
| `PATCH` | Atualizar parcialmente campos de um recurso | Depende | Não | `200 OK` |
| `DELETE` | Remover um recurso específico | Sim | Não | `200 OK` ou `204 No Content` |

### O Formato JSON (*JavaScript Object Notation*)

O JSON é o padrão universal para tráfego de dados em APIs REST devido à sua leveza e facilidade de leitura tanto por humanos quanto por máquinas. Suas principais regras de formatação incluem:
- Chaves (*keys*) sempre delimitadas por aspas duplas: `"titulo": "Minha Nota"`.
- Suporte a tipos primitivos: strings, números (inteiros e ponto flutuante), booleanos (`true`/`false`) e `null`.
- Suporte a estruturas compostas: objetos aninhados `{}` e arrays `[]`.
- Proibição de vírgulas sobrando (*trailing commas*) e comentários.

---

## 2. O Framework Express.js e o Middleware CORS

### Por que usar o Express.js?

Embora o Node.js venha de fábrica com o módulo nativo `http`, criar uma API REST profissional com ele exige dezenas de linhas de código repetitivas para tratar URLs manualmente, manipular buffers de stream para ler o body da requisição e tratar tipos de conteúdo (*MIME types*).

O **Express.js** é um framework minimalista e altamente performático que simplifica o desenvolvimento de APIs ao fornecer:
- Sistema limpo e declarativo de definição de rotas e métodos (`app.get()`, `app.post()`, etc.).
- Suporte nativo ao ecossistema de **Middlewares** (funções encadeadas que interceptam a requisição antes de chegar ao controlador final).
- Métodos facilitadores de resposta, como `res.json()`, `res.status()` e `res.send()`.

### O que são Middlewares no Express?

Middlewares são funções intermediárias executadas sequencialmente durante o ciclo de vida da requisição. Cada middleware recebe os objetos `req` (requisição), `res` (resposta) e a função `next()`:
- `express.json()`: Intercepta requisições com cabeçalho `Content-Type: application/json`, faz o parse do corpo da mensagem e o disponibiliza pronto no objeto `req.body`.
- Funções de log, autenticação via token e tratamento centralizado de erros são implementadas como middlewares.

### O Mecanismo CORS (*Cross-Origin Resource Sharing*)

O **CORS** é uma política de segurança executada pelos navegadores para restringir requisições HTTP assíncronas (como as feitas por `fetch` ou `axios`) originadas de um domínio, porta ou protocolo diferente daquele onde a API está hospedada.

- **Cenário típico de bloqueio:** O front-end React roda em `http://localhost:3000`, e a API Express roda em `http://localhost:5000`. Sem a configuração de CORS, o navegador bloqueia a leitura da resposta por medidas de segurança de mesma origem (*Same-Origin Policy*).
- **Solução no Express:** Instalação e ativação do middleware `cors`:
  ```bash
  npm install cors
  ```
  ```javascript
  const cors = require("cors");
  app.use(cors()); // Habilita o cabeçalho 'Access-Control-Allow-Origin: *' permitindo requisições de qualquer origem
  ```

---

## 3. Projeto Prático: API de Bloco de Notas (CRUD Completo)

### Inicialização e Estrutura de Arquivos

Para estruturar a API de notas apresentada na aula:

```bash
# 1. Cria a pasta e inicializa o projeto Node.js
mkdir api-notas
cd api-notas
npm init -y

# 2. Instala as dependências de produção
npm install express cors body-parser
```

A estrutura do projeto consiste em:
```text
api-notas/
├── data.json       # Arquivo de persistência local das notas
├── package.json    # Manifesto do projeto e dependências
└── server.js       # Código do servidor Express e rotas CRUD
```

### Arquivo de Persistência Inicial (`data.json`)

```json
[
  {
    "id": 1,
    "title": "Primeira Nota",
    "content": "Conteúdo de exemplo da primeira nota."
  }
]
```

### Código Completo do Servidor (`server.js`)

O código abaixo implementa todos os métodos fundamentais do CRUD com leitura e gravação no arquivo `data.json` através do módulo nativo `fs` (*File System*):

```javascript
const express = require("express");
const cors = require("cors");
const bodyParser = require("body-parser");
const fs = require("fs");
const path = require("path");

const app = express();
const DATA_FILE = path.join(__dirname, "data.json");

// Middlewares
app.use(cors());
app.use(bodyParser.json());

// Função utilitária para ler as notas do arquivo JSON
function readNotes() {
  try {
    const data = fs.readFileSync(DATA_FILE, "utf-8");
    return JSON.parse(data);
  } catch (err) {
    return [];
  }
}

// Função utilitária para salvar as notas no arquivo JSON
function writeNotes(notes) {
  fs.writeFileSync(DATA_FILE, JSON.stringify(notes, null, 2), "utf-8");
}

// 1. ROTA GET /api/notes - Listar todas as notas
app.get("/api/notes", (req, res) => {
  const notes = readNotes();
  res.status(200).json(notes);
});

// 2. ROTA GET /api/notes/:id - Obter uma nota específica por ID
app.get("/api/notes/:id", (req, res) => {
  const notes = readNotes();
  const noteId = parseInt(req.params.id, 10);
  const note = notes.find((n) => n.id === noteId);

  if (!note) {
    return res.status(404).json({ message: "Nota não encontrada." });
  }

  res.status(200).json(note);
});

// 3. ROTA POST /api/notes - Criar uma nova nota
app.post("/api/notes", (req, res) => {
  const { title, content } = req.body;

  if (!title || !content) {
    return res.status(400).json({ message: "Título e conteúdo são obrigatórios." });
  }

  const notes = readNotes();
  const newNote = {
    id: Date.now(), // Gera identificador único baseado em timestamp
    title,
    content
  };

  notes.push(newNote);
  writeNotes(notes);

  res.status(201).json(newNote);
});

// 4. ROTA PUT /api/notes/:id - Atualizar uma nota existente por completo
app.put("/api/notes/:id", (req, res) => {
  const noteId = parseInt(req.params.id, 10);
  const { title, content } = req.body;
  const notes = readNotes();

  const noteIndex = notes.findIndex((n) => n.id === noteId);
  if (noteIndex === -1) {
    return res.status(404).json({ message: "Nota não encontrada para atualização." });
  }

  notes[noteIndex] = {
    id: noteId,
    title: title || notes[noteIndex].title,
    content: content || notes[noteIndex].content
  };

  writeNotes(notes);
  res.status(200).json(notes[noteIndex]);
});

// 5. ROTA DELETE /api/notes/:id - Excluir uma nota
app.delete("/api/notes/:id", (req, res) => {
  const noteId = parseInt(req.params.id, 10);
  const notes = readNotes();

  const filteredNotes = notes.filter((n) => n.id !== noteId);
  if (filteredNotes.length === notes.length) {
    return res.status(404).json({ message: "Nota não encontrada para exclusão." });
  }

  writeNotes(filteredNotes);
  res.status(200).json({ message: "Nota removida com sucesso." });
});

// Inicialização do servidor na porta definida pelo ambiente ou porta padrão 3000
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Servidor rodando com sucesso na porta ${PORT}`);
});
```
