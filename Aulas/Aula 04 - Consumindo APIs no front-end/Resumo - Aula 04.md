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
