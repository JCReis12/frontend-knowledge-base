# Resumo completo de estudo — Aula 04: Consumindo APIs no Front-end

Este resumo reúne os conceitos de comunicação entre front-end e back-end, APIs REST, protocolo HTTP, endpoints e JSON, além da criação e publicação de uma API com Express. O objetivo é entender o caminho percorrido pelos dados entre a interface, o servidor e eventuais serviços externos.

## 1. API e API REST

**API** (*Application Programming Interface*, ou Interface de Programação de Aplicações) é um conjunto de regras e recursos que permite que componentes ou sistemas diferentes se comuniquem. Ela define como solicitar funcionalidades ou dados sem que o consumidor precise conhecer todos os detalhes internos do sistema que os fornece.

**REST** (*Representational State Transfer*) é um estilo arquitetural usado com frequência para construir APIs web. Uma API REST organiza a comunicação em torno de recursos identificados por URIs, utiliza os métodos HTTP de forma padronizada, troca representações desses recursos (comumente JSON) e mantém as requisições independentes umas das outras (*stateless*). Portanto, API é um conceito amplo; REST é uma das formas de projetar uma API.

## 2. Protocolo HTTP e comunicação cliente-servidor

**HTTP** (*Hypertext Transfer Protocol*) é o protocolo que define como clientes e servidores trocam mensagens na web. O navegador ou aplicação front-end atua como cliente: envia uma requisição a um servidor e aguarda uma resposta. O servidor pode executar regras de negócio, consultar ou atualizar dados e devolver o resultado ao cliente.

HTTP é *stateless*: cada requisição deve trazer as informações necessárias para ser processada, pois o protocolo não pressupõe que o servidor se lembre automaticamente de requisições anteriores. Uma requisição pode incluir método, URL, cabeçalhos e, quando necessário, um corpo com dados; a resposta inclui um código de status, cabeçalhos e, frequentemente, um corpo com os dados ou uma mensagem.

### Fluxo de uma requisição

1. A pessoa interage com a página, por exemplo, clicando em um botão.
2. O front-end envia uma requisição HTTP para um endpoint.
3. O servidor recebe a requisição, identifica a rota e executa a lógica necessária.
4. Se necessário, o servidor consulta um banco de dados ou outro serviço.
5. O servidor envia uma resposta, muitas vezes em JSON.
6. O front-end interpreta o resultado e atualiza a interface ou apresenta uma mensagem.

O front-end não precisa acessar diretamente a implementação interna do servidor: a API funciona como a interface de comunicação entre as partes.

## 3. Métodos HTTP

Os métodos indicam a intenção da requisição em relação a um recurso. O comportamento final depende da implementação da API, mas uma API REST normalmente segue estas convenções:

| Método | Uso comum | Observação |
| --- | --- | --- |
| `GET` | Consultar ou recuperar dados. | É seguro (não deve alterar o recurso) e idempotente. |
| `POST` | Enviar dados ou criar um recurso. | Repetir a requisição pode criar vários recursos; não é idempotente por padrão. |
| `PUT` | Criar ou substituir por completo um recurso conhecido. | É usado para atualização completa e é idempotente por definição. |
| `PATCH` | Alterar parcialmente um recurso. | Envia apenas as mudanças desejadas; a idempotência depende da operação definida pela API. |
| `DELETE` | Remover um recurso. | Repetir a operação mantém o recurso removido; por isso, é idempotente, ainda que a resposta possa variar. |

### Idempotência e segurança

Uma operação é **idempotente** quando repeti-la produz o mesmo estado final no servidor que executá-la uma vez. Isso não significa necessariamente que todas as respostas sejam iguais. Uma operação **segura** não deve modificar dados. `GET` é seguro e idempotente; `POST` normalmente não é idempotente. Esses termos ajudam a prever como uma API se comporta diante de uma repetição de requisição.

## 4. Endpoint

Um **endpoint** é um endereço específico pelo qual o cliente acessa um recurso ou uma funcionalidade da API. Em geral, combina a URL/base da API com um caminho; o método HTTP usado também define a ação solicitada. Por exemplo, `GET /usuarios` pode listar usuários, enquanto `POST /usuarios` pode criar um usuário.

Exemplo de endereço: `https://api.exemplo.com/usuarios/42?ativo=true`. Nesse caso, `/usuarios/42` identifica o recurso e `ativo=true` é um parâmetro de consulta. O servidor precisa documentar quais rotas, métodos e formatos de dados aceita.

## 5. JSON

**JSON** (*JavaScript Object Notation*) é um formato leve de texto usado para representar e trocar dados. É fácil de ler por pessoas e pode ser gerado e interpretado por diferentes linguagens; apesar do nome, não é exclusivo de JavaScript. APIs frequentemente usam JSON no corpo das requisições e respostas.

JSON representa dados por meio de **objetos**, organizados em pares nome/valor, e **arrays**, que são listas ordenadas de valores. Também admite strings, números, valores booleanos (`true` e `false`) e `null`, além de objetos e arrays aninhados.

Exemplo de resposta JSON:

```json
{
  "id": 42,
  "nome": "Ana",
  "ativo": true,
  "interesses": ["front-end", "APIs"],
  "endereco": {
    "cidade": "São Paulo"
  }
}
```

Em JSON válido, nomes de propriedades e textos usam aspas duplas; comentários e vírgulas sobrando não são permitidos. Isso é importante ao construir ou interpretar o corpo de uma requisição.

## 6. Back-end e Web Service

O **back-end** é a parte da aplicação que processa requisições, aplica regras de negócio, gerencia dados e fornece recursos para clientes como navegadores e aplicativos. Ele pode armazenar ou recuperar dados em um banco e oferecer uma API para que outros sistemas acessem essas funcionalidades.

Um **Web Service** é um serviço acessível pela web que permite a comunicação entre sistemas, normalmente por HTTP/HTTPS. Ele possibilita que aplicações construídas com linguagens e plataformas diferentes se comuniquem usando um formato e um protocolo acordados. Uma API web pode ser oferecida por um serviço desse tipo.

## 7. Express.js

**Express.js** é um framework minimalista e flexível para Node.js que simplifica a criação de servidores web e APIs. Em comparação com o módulo HTTP nativo do Node.js, ele reduz o trabalho necessário para organizar rotas e processar requisições e respostas.

Rotas associam um caminho e um método HTTP a uma ação, como `GET /usuarios`. **Middlewares** são funções executadas durante o processamento da requisição e podem, por exemplo, registrar informações, interpretar dados recebidos, aplicar autenticação ou tratar erros. O Express é adequado para APIs REST e back-ends web; para comunicação em tempo real, WebSockets podem ser mais apropriados, enquanto processamento pesado costuma ser encaminhado a workers.

### Estrutura mínima de uma API

Para iniciar um projeto, crie uma pasta, inicialize o projeto Node.js e instale as dependências. Os comandos abaixo instalam o Express e o middleware `cors` usados no exemplo:

```bash
npm init -y
npm install express cors
```

Uma rota pode responder em JSON com `res.json(...)`. A porta usa `process.env.PORT` para funcionar em ambientes de hospedagem que definem a porta do serviço:

```js
const express = require("express");
const cors = require("cors");

const app = express();
app.use(cors());
app.use(express.json());

app.get("/api/data-hora", (req, res) => {
  res.json({ dataHora: new Date().toISOString() });
});

const port = process.env.PORT || 3000;
app.listen(port, () => console.log(`API disponível na porta ${port}`));
```

Salve o código em `api.js` e execute com `node api.js`. Depois, uma requisição `GET` para `/api/data-hora` recebe um objeto JSON com a data e hora.

### Consumindo a API no front-end

No navegador, `fetch` permite enviar uma requisição e aguardar a resposta. A conversão para JSON também é assíncrona; verifique `response.ok`, trate erros e atualize a interface somente depois de receber os dados:

```js
async function carregarDataHora() {
  try {
    const response = await fetch("http://localhost:3000/api/data-hora");
    if (!response.ok) {
      throw new Error(`Erro HTTP: ${response.status}`);
    }

    const dados = await response.json();
    document.querySelector("#data-hora").textContent = dados.dataHora;
  } catch (erro) {
    console.error("Não foi possível carregar a data e hora:", erro);
  }
}
```

Em uma aplicação real, apresente estados de carregamento e mensagens de erro compreensíveis, e use a URL pública da API após o deploy em vez do endereço local.

## 8. CORS

**CORS** (*Cross-Origin Resource Sharing*) é um mecanismo de segurança dos navegadores que controla requisições feitas entre origens diferentes. Uma origem é composta por esquema, host e porta; por isso, o front-end e a API executados em endereços diferentes podem precisar que o servidor autorize essa comunicação.

No exemplo, `cors()` adiciona o middleware do Express para configurar essa política. Em aplicações publicadas, restrinja as origens permitidas conforme a necessidade: CORS não substitui autenticação nem autorização e não deve ser tratado como mecanismo para proteger dados sensíveis.

## 9. Publicação da API no Render

O Render foi apresentado como uma plataforma de hospedagem que integra com repositórios GitHub e pode publicar serviços Node.js. O fluxo trabalhado na aula é: enviar o projeto a um repositório, criar uma conta no Render, escolher **New → Web Service**, conectar o repositório e configurar os comandos de instalação e inicialização de acordo com o projeto.

Para o exemplo com `api.js`, uma configuração possível é usar `npm install` como comando de build e `node api.js` como comando de inicialização. A API deve escutar a porta fornecida pelo ambiente (`process.env.PORT`); depois do deploy, teste a URL pública terminada em `.onrender.com` e o endpoint criado. A aula também destaca deploy conectado ao GitHub e certificado SSL.

## 10. Atividade 01 — pesquisa de projetos que usam APIs

A atividade propõe pesquisar dez projetos no GitHub que utilizem APIs, clonar e analisar os repositórios e registrar os resultados em um arquivo Markdown. Para cada projeto, identifique o framework ou as tecnologias do front-end, quais APIs são consumidas e a finalidade de cada integração. Compare como os dados externos ou do back-end são usados pela aplicação.

O levantamento da atividade está organizado em [Pesquisa - Projetos com API](./Pesquisa%20-%20Projetos%20com%20API.md), com uma tabela comparativa e observações sobre os projetos selecionados.

## 11. Atividade 02 — API de data e hora

A segunda atividade propõe criar uma API com Express que disponibilize uma rota para consultar data e hora, publicar o serviço no Render e desenvolver uma aplicação front-end que consuma essa rota e apresente o resultado na tela. A publicação torna a API acessível por uma URL pública, que deve ser usada pelo cliente.

O enunciado também solicita separar front-end e API em repositórios distintos e reunir em um documento evidências do código, da aplicação em funcionamento, dos painéis do Render e da Vercel e os links dos repositórios no GitHub.

## 12. Interpretando o resultado da requisição

Além do corpo da resposta, verifique o **código de status HTTP** para entender o resultado: códigos `2xx` indicam sucesso; `4xx`, problemas relacionados à requisição ou à autorização do cliente; e `5xx`, falhas durante o processamento no servidor. No `fetch`, uma resposta HTTP de erro não rejeita automaticamente a promessa, por isso é importante testar `response.ok` antes de interpretar o JSON.

## Revisão rápida

- **API:** contrato de comunicação entre sistemas; **REST:** estilo arquitetural comum para APIs web.
- **HTTP:** protocolo usado para enviar requisições e receber respostas; os métodos comunicam a intenção da operação.
- **Endpoint:** endereço de acesso a um recurso ou funcionalidade; **JSON:** formato frequente para representar os dados trocados.
- **Back-end:** processa a lógica e os dados; **Express:** facilita a criação de rotas e servidores Node.js.
- **CORS:** política do navegador para requisições entre origens; o servidor configura quais origens podem acessar os recursos.
- **Fluxo completo:** interface solicita → API processa → servidor responde → front-end interpreta e atualiza a tela.

## Perguntas para testar o aprendizado

1. Qual é a diferença entre uma API e uma API REST?
2. O que significa dizer que HTTP é *stateless*?
3. Quando escolher `GET`, `POST`, `PUT`, `PATCH` ou `DELETE`?
4. O que é um endpoint e como o método HTTP muda a ação solicitada?
5. Quais estruturas e tipos de valor podem ser representados em JSON?
6. Que etapas acontecem entre a interação na página e a atualização da tela com dados da API?
7. Qual é o papel do Express e de um middleware como `cors`?
8. Por que o front-end deve tratar falhas HTTP e de conexão ao consumir uma API?
9. O que deve ser configurado para publicar e acessar uma API Node.js no Render?

## Onde encontrar APIs para praticar

Catálogos de APIs públicas reúnem serviços e fontes de dados que podem ser integrados a projetos de estudo. A aula cita o [Free Public APIs](https://www.freepublicapis.com/) como exemplo. Antes de escolher uma API, confira a documentação, os recursos disponíveis, os limites de uso e se é necessário obter uma chave de acesso.
