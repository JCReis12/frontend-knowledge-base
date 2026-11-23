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


---

## 4. Testes e Documentação de APIs com Postman

### O que é o Postman?

O **Postman** é a plataforma líder para projeto, documentação, testes e consumo de APIs. Ele permite enviar qualquer tipo de requisição HTTP (GET, POST, PUT, DELETE, PATCH), personalizar headers, parâmetros de consulta e payloads JSON antes mesmo de construir a interface do front-end.

### Coleções (*Collections*) e Pastas

- **Collections:** Permitem agrupar e organizar dezenas de requisições relacionadas a um mesmo projeto ou microsserviço.
- Facilitam a exportação e o compartilhamento da documentação viva da API entre membros da equipe de back-end e front-end.
- Permitem organizar subpastas temáticas (ex.: `Notas / Leitura`, `Notas / Escrita`).

### Variáveis de Ambiente e Globais

Em vez de digitar `http://localhost:3000` em cada requisição:
1. Criam-se ambientes no Postman (ex.: **Desenvolvimento Local** e **Produção no Render**).
2. Define-se a variável `base_url`:
   - No ambiente Local: `http://localhost:3000`
   - No ambiente de Produção: `https://minha-api-notas.onrender.com`
3. As requisições são chamadas usando chaves duplas: `{{base_url}}/api/notes`. Ao alternar o ambiente no canto superior do Postman, todas as URLs são atualizadas instantaneamente.

### Testes Automatizados no Postman

Na aba **Tests** de cada requisição, é possível escrever scripts em JavaScript para validar automaticamente o comportamento da resposta:

```javascript
// Valida se o status code é 200 OK
pm.test("Status code é 200", function () {
  pm.response.to.have.status(200);
});

// Valida se a resposta veio no formato JSON
pm.test("Retorno é um JSON válido", function () {
  pm.response.to.be.json;
});

// Valida se o tempo de resposta foi inferior a 500ms
pm.test("Tempo de resposta aceitável", function () {
  pm.expect(pm.response.responseTime).to.be.below(500);
});

// Valida campos específicos do corpo retornado
pm.test("A nota possui título e id", function () {
  const jsonData = pm.response.json();
  pm.expect(jsonData).to.have.property("id");
  pm.expect(jsonData).to.have.property("title");
});
```

### Automação com Newman e Mock Servers

- **Newman:** Ferramenta CLI oficial do Postman que permite rodar coleções de testes diretamente no terminal e em pipelines de integração contínua (CI/CD).
- **Mock Servers:** Recurso do Postman que simula o comportamento da API antes que o back-end esteja pronto. O desenvolvedor front-end pode começar a construir as telas e componentes consumindo a URL do Mock Server com dados fictícios acordados previamente.

---

## 5. Publicação da API no Render

O **Render** é uma plataforma em nuvem para hospedar aplicações web, bancos de dados e APIs com suporte nativo a Node.js e integração direta com o GitHub.

### Preparação do Projeto para Produção

1. **Configurar o script de inicialização no `package.json`:**
   ```json
   "scripts": {
     "start": "node server.js"
   }
   ```
2. **Definir a porta dinâmica:** Garantir que o servidor leia a variável de ambiente injetada pela plataforma de nuvem:
   ```javascript
   const PORT = process.env.PORT || 3000;
   ```

### Passo a Passo de Deploy no Render

1. Suba o código do projeto para um repositório no GitHub (`git push -u origin main`).
2. Acesse o painel do [Render](https://render.com) e clique em **New → Web Service**.
3. Conecte sua conta do GitHub e selecione o repositório da API de Notas.
4. Preencha as configurações do serviço:
   - **Environment:** Node
   - **Build Command:** `npm install`
   - **Start Command:** `npm start` ou `node server.js`
   - **Plan:** Free
5. Clique em **Create Web Service**. O Render clonará o repositório, instalará as dependências e iniciará o servidor, disponibilizando uma URL pública segura com HTTPS (ex.: `https://api-notas-xyz.onrender.com`).

---

## 6. Questões para Refletir: Arquitetura, Segurança e Persistência

A aula traz discussões cruciais sobre a evolução de uma API básica para uma solução profissional:

### 1. Limitações de Persistência com Arquivo JSON (`fs`)
- **Concorrência e Locks:** Quando múltiplos usuários realizam requisições simultâneas de escrita (`POST`/`PUT`/`DELETE`), o uso de `fs.writeFileSync` pode causar corrupção de dados ou sobrescrita acidental de registros (*race conditions*).
- **Escala e Memória:** O método lê todo o arquivo para a memória RAM a cada requisição. Em bases com milhares de registros, isso causa gargalo de processamento.
- **Ambientes Efêmeros de Nuvem:** Plataformas como Render e Heroku utilizam contêineres que podem reiniciar ou entrar em hibernação, fazendo com que arquivos locais gravados no disco em tempo de execução sejam perdidos. Em produção real, é fundamental migrar para um **Banco de Dados Relacional (PostgreSQL, MySQL)** ou **NoSQL (MongoDB)**.

### 2. Boas Práticas de Segurança em APIs
- **Validação e Sanitização de Entrada:** Nunca confiar nos dados recebidos em `req.body`. Validar tipos, tamanhos de texto e caracteres especiais para evitar injeções maliciosas.
- **Restrição de CORS:** Em produção, substituir `app.use(cors())` por regras estritas permitindo apenas os domínios oficiais da sua aplicação front-end:
  ```javascript
  app.use(cors({ origin: "https://meu-app.vercel.app" }));
  ```
- **Rate Limiting:** Implementar limites de requisições por IP (ex.: biblioteca `express-rate-limit`) para prevenir ataques de negação de serviço (DDoS) ou força bruta.
- **Autenticação e Autorização:** Utilizar tokens de acesso (JWT - JSON Web Tokens) ou chaves de API (*API Keys*) para proteger rotas sensíveis contra acesso não autorizado.

---

## 7. Atividades Práticas da Aula 05

### Atividade 01: Desenvolvimento, Testes e Publicação da API de Notas

1. Implementar a API de Notas com Express e Node.js contendo as 5 operações do CRUD (`GET /api/notes`, `GET /api/notes/:id`, `POST /api/notes`, `PUT /api/notes/:id`, `DELETE /api/notes/:id`).
2. Configurar os middlewares de CORS e tratamento de JSON.
3. Criar uma Collection completa no Postman com todas as requisições configuradas e testes automatizados de status code.
4. Publicar a API como Web Service no Render e validar as chamadas com a URL pública.
5. Exportar a Collection do Postman e registrar evidências do deploy.

### Atividade 02: Consumo da API pelo Front-end

1. Desenvolver uma aplicação front-end (em React ou Vanilla JS) dedicada à exibição e manipulação das notas.
2. Implementar a interface de usuário com:
   - Formulário para criação de novas notas.
   - Listagem dinâmica das notas salvas consumindo o endpoint público do Render via `fetch`.
   - Botões de ação para exclusão e edição de notas.
3. Tratar estados assíncronos (carregamento, feedback de sucesso e mensagens amigáveis em caso de erro na comunicação).
4. Publicar o front-end na Vercel e disponibilizar ambos os repositórios (API no Render e Front-end na Vercel) com seus respectivos READMEs documentados.

---

## 8. Revisão Rápida e Perguntas de Fixação

- **Express.js:** Framework minimalista para Node.js que simplifica a criação de rotas, middlewares e envio de respostas JSON.
- **CORS:** Mecanismo do navegador que impede requisições entre origens diferentes a menos que o servidor explicitamente autorize através de cabeçalhos HTTP.
- **CRUD:** Conjunto das 4 operações essenciais de dados mapeadas para os verbos HTTP: Create (`POST`), Read (`GET`), Update (`PUT`/`PATCH`) e Delete (`DELETE`).
- **Postman:** Ferramenta indispensável para planejar, validar com testes automatizados e documentar APIs antes e durante a integração com o front-end.
- **Deploy no Render:** Publicação em nuvem com integração ao GitHub, exigindo porta dinâmica (`process.env.PORT`) e script de start.

### Perguntas para Testar o Conhecimento

1. Qual a diferença entre criar um servidor com o módulo nativo `http` do Node.js e utilizar o Express.js?
2. Por que o middleware `cors()` é necessário quando o front-end e o back-end rodam em portas diferentes na mesma máquina?
3. Qual é o papel da função `next()` dentro de um middleware do Express?
4. Quais são as principais desvantagens de utilizar um arquivo `data.json` local para armazenar dados em uma aplicação em produção?
5. Como as variáveis de ambiente no Postman facilitam a transição entre o desenvolvimento local e o ambiente de produção?
