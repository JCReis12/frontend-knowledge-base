 # Pesquisa: projetos front-end que utilizam APIs

 > **Tema:** consumo de APIs no front-end  
 > **Objetivo:** observar como projetos reais usam dados e serviços externos para criar interfaces mais completas.

 ## Visão geral

 Uma API (*Application Programming Interface*) é um contrato que permite a comunicação entre aplicações. No front-end, ela costuma ser acessada com `fetch`, Axios ou bibliotecas especializadas. A resposta geralmente vem em JSON e é usada para atualizar a interface sem recarregar toda a página.

 Nesta seleção, as APIs representam assuntos diferentes: gerenciamento de tarefas, rede social, hospedagem, mapas, autenticação, clima, livros, filmes, notícias e dados de teste.

 ## Comparativo rápido

 | # | Repositório | API utilizada | Finalidade | Front-end |
 | ---: | --- | --- | --- | --- |
 | 1 | [Jira Clone](https://github.com/oldboyxx/jira_clone) | API REST própria | Projetos, tarefas, usuários e comentários | React |
 | 2 | [React Redux RealWorld](https://github.com/gothinkster/react-redux-realworld-example-app) | RealWorld/Conduit API | Artigos, comentários, favoritos e autenticação | React + Redux + Create React App |
 | 3 | [Fullstack GraphQL Airbnb Clone](https://github.com/benawad/fullstack-graphql-airbnb-clone) | GraphQL próprio + Google Maps API | Anúncios de hospedagem, localização e mapas | React |
 | 4 | [Hackathon Starter](https://github.com/sahat/hackathon-starter) | GitHub, Google, GIPHY, Stripe, Twilio e outras | Login, mapas, pagamentos, mensagens e mídia | Pug + Bootstrap |
 | 5 | [30 Days of React](https://github.com/Asabeneh/30-Days-Of-React) | APIs de projetos didáticos | Exercícios de busca de dados e uso de hooks | React |
 | 6 | [30 Days of JavaScript](https://github.com/Asabeneh/30-Days-Of-JavaScript) | APIs públicas em projetos práticos | Clima, países, GitHub e outros dados | JavaScript, HTML e CSS |
 | 7 | [Vanilla Web Projects](https://github.com/bradtraversy/vanillawebprojects) | APIs públicas em pequenos projetos | Clima, câmbio, filmes e busca de dados | JavaScript, HTML e CSS |
 | 8 | [Bulletproof React](https://github.com/alan2207/bulletproof-react) | API REST simulada com MSW | Demonstração de camada de dados, cache e estados | React + TypeScript |
 | 9 | [JSONPlaceholder](https://github.com/typicode/jsonplaceholder) | JSONPlaceholder | Dados fictícios para testar protótipos e telas | Compatível com React, Angular, Vue e outros |
 | 10 | [React Redux Universal Hot Example](https://github.com/erikras/react-redux-universal-hot-example) | API própria de exemplo | Buscar dados no servidor e no cliente | React + Redux + Express |

 ---

 ## Análise dos repositórios

 ### 1. Jira Clone

 **Repositório:** [oldboyxx/jira_clone](https://github.com/oldboyxx/jira_clone)  
 **API utilizada:** API REST própria, criada com Node.js, TypeScript e TypeORM.  
 **Para que serve:** fornece os dados do clone do Jira: projetos, tarefas, usuários, prioridades, comentários e relacionamentos entre itens. O cliente faz requisições para a API e transforma as respostas em uma interface de gerenciamento de projetos.  
 **Framework front-end:** React, com componentes funcionais e hooks.  
 **O que observar:** a separação entre as pastas `client` e `api` mostra claramente a comunicação entre front-end e back-end.

 ### 2. React Redux RealWorld

 **Repositório:** [gothinkster/react-redux-realworld-example-app](https://github.com/gothinkster/react-redux-realworld-example-app)  
 **API utilizada:** [RealWorld/Conduit API](https://github.com/gothinkster/realworld).  
 **Para que serve:** alimenta uma rede social de artigos, com cadastro, login, JWT, publicação, comentários, favoritos, tags e seguidores.  
 **Framework front-end:** React com Redux, iniciado com Create React App.  
 **O que observar:** o arquivo `src/agent.js` concentra a URL da API e as ações Redux organizam os estados de carregamento, sucesso e erro.

 ### 3. Fullstack GraphQL Airbnb Clone

 **Repositório:** [benawad/fullstack-graphql-airbnb-clone](https://github.com/benawad/fullstack-graphql-airbnb-clone)  
 **API utilizada:** servidor GraphQL próprio e [Google Maps JavaScript API](https://developers.google.com/maps/documentation/javascript/overview).  
 **Para que serve:** o GraphQL gerencia autenticação, anúncios, criação e visualização de hospedagens e chat; o Google Maps permite trabalhar com localização e mapa no anúncio.  
 **Framework front-end:** React para a versão web, além de React Native para o aplicativo.  
 **O que observar:** o repositório separa os pacotes `web`, `app`, `server`, `common` e `controller`, mostrando o compartilhamento de dados entre plataformas.

 ### 4. Hackathon Starter

 **Repositório:** [sahat/hackathon-starter](https://github.com/sahat/hackathon-starter)  
 **APIs utilizadas:** GitHub e Google OAuth, Google Maps, GIPHY, Stripe, Twilio, Twitch, Trakt, Foursquare e outras integrações.  
 **Para que serve:** oferece exemplos de login social, mapas, GIFs, pagamentos, SMS, filmes, música, jogos, finanças e comunicação.  
 **Framework front-end:** Pug para os templates, com Bootstrap 5.3 para a interface.  
 **O que observar:** é um bom catálogo de integrações. As chaves ficam em variáveis de ambiente, evitando que segredos sejam enviados ao repositório.

 ### 5. 30 Days of React

 **Repositório:** [Asabeneh/30-Days-Of-React](https://github.com/Asabeneh/30-Days-Of-React)  
 **APIs utilizadas:** APIs públicas usadas nos projetos e exercícios do desafio, especialmente nas partes sobre `fetch`, Axios e busca de dados com hooks.  
 **Para que serve:** praticar requisições assíncronas, renderização de listas, tratamento de carregamento e atualização do estado a partir de respostas externas.  
 **Framework front-end:** React.  
 **O que observar:** as seções [Fetch and Axios](https://github.com/Asabeneh/30-Days-Of-React/tree/master/18_Fetch_And_Axios) e [Fetching Data Using Hooks](https://github.com/Asabeneh/30-Days-Of-React/tree/master/23_Fetching_Data_Using_Hooks) são as mais relacionadas ao tema.

 ### 6. 30 Days of JavaScript

 **Repositório:** [Asabeneh/30-Days-Of-JavaScript](https://github.com/Asabeneh/30-Days-Of-JavaScript)  
 **APIs utilizadas:** APIs públicas em projetos de clima, países, GitHub e outras interfaces do desafio.  
 **Para que serve:** exercitar `fetch`, `async/await`, leitura de JSON, busca por parâmetros e exibição de dados vindos da internet sem usar um framework.  
 **Framework front-end:** não utiliza framework; usa JavaScript, HTML e CSS.  
 **O que observar:** é uma comparação útil com os exemplos em React, pois o conceito de consumo da API continua o mesmo, mudando apenas a forma de atualizar a interface.

 ### 7. Vanilla Web Projects

 **Repositório:** [bradtraversy/vanillawebprojects](https://github.com/bradtraversy/vanillawebprojects)  
 **APIs utilizadas:** APIs públicas em projetos como previsão do tempo, cotação de moedas, filmes e busca de dados.  
 **Para que serve:** criar pequenos projetos completos com dados reais, praticando requisições HTTP, parâmetros, respostas JSON e mensagens de erro.  
 **Framework front-end:** nenhum; utiliza JavaScript, HTML e CSS puros.  
 **O que observar:** os projetos pequenos permitem isolar cada etapa do fluxo: solicitar dados, aguardar a resposta, montar os elementos e tratar falhas.

 ### 8. Bulletproof React

 **Repositório:** [alan2207/bulletproof-react](https://github.com/alan2207/bulletproof-react)  
 **API utilizada:** camada de API REST simulada com [Mock Service Worker (MSW)](https://mswjs.io/), usada para imitar respostas do servidor durante o desenvolvimento.  
 **Para que serve:** demonstrar uma arquitetura organizada para requisições, cache, estados de carregamento, erros e invalidação de dados, sem depender de um back-end real para executar o exemplo.  
 **Framework front-end:** React com TypeScript; o repositório também possui versões com Vite e Next.js.  
 **O que observar:** a documentação de [API Layer](https://github.com/alan2207/bulletproof-react/blob/master/docs/api-layer.md) mostra como manter a comunicação com a API separada da apresentação.

 ### 9. JSONPlaceholder

 **Repositório:** [typicode/jsonplaceholder](https://github.com/typicode/jsonplaceholder)  
 **API utilizada:** [JSONPlaceholder](https://jsonplaceholder.typicode.com/), uma API REST falsa para testes e prototipação.  
 **Para que serve:** disponibilizar recursos como posts, usuários, comentários, álbuns e tarefas para que um front-end pratique `GET`, `POST`, `PUT`, `PATCH` e `DELETE` sem criar um back-end próprio.  
 **Framework front-end:** o serviço é compatível com React, Angular, Vue, Ember e outros; o repositório da API em si é um servidor Express/JSON Server.  
 **O que observar:** é uma opção segura para aprender o fluxo de uma requisição antes de integrar uma API de produção.

 ### 10. React Redux Universal Hot Example

 **Repositório:** [erikras/react-redux-universal-hot-example](https://github.com/erikras/react-redux-universal-hot-example)  
 **API utilizada:** API própria de exemplo, que retorna dados em JSON, como o horário atual; o projeto também demonstra um cliente de API compartilhado entre servidor e navegador.  
 **Para que serve:** carregar dados no servidor e no cliente, manter o estado no Redux e renderizar a aplicação com dados já disponíveis no primeiro carregamento.  
 **Framework front-end:** React + Redux, com React Router; o servidor usa Express e Webpack.  
 **O que observar:** o exemplo é histórico e o próprio README recomenda não usá-lo em novos projetos, mas ele é didático para compreender renderização universal e busca de dados.

 ---

 ## O que esses exemplos ensinam

 1. **A API define o contrato de dados:** o front-end precisa conhecer endpoints, parâmetros, métodos HTTP e formato da resposta.
 2. **O estado da interface acompanha a requisição:** uma boa tela prevê carregamento, sucesso, resposta vazia e erro.
 3. **A camada de acesso deve ficar organizada:** separar chamadas de API, regras de estado e componentes facilita a manutenção.
 4. **Nem toda API é externa:** um projeto pode consumir uma API própria, uma API simulada ou APIs nativas do navegador.
 5. **Segredos não devem ficar no front-end:** chaves privadas devem ser protegidas no servidor e configuradas por variáveis de ambiente.

 ## Conclusão

 Os repositórios mostram que consumir uma API não significa apenas executar um `fetch`. É necessário interpretar a resposta, controlar o estado da aplicação, informar o usuário durante o carregamento, tratar erros e proteger credenciais. A escolha do framework muda a organização do código, mas o fluxo fundamental permanece: **requisição → resposta → estado → interface**.

 > **Nota da pesquisa:** repositórios e documentações podem ser atualizados, arquivados ou ter APIs descontinuadas. Os links acima apontam para as páginas oficiais consultadas em **26/08/2026**; antes de executar algum projeto, confira o README e os requisitos atuais.
