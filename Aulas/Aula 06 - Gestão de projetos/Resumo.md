# Resumo completo de estudo — Aula 06: Gestão de Projetos de Software

Este resumo aborda as práticas fundamentais de gestão de projetos aplicadas ao desenvolvimento de software, com foco no ciclo de vida de aplicações web, levantamento e estruturação de requisitos, histórias de usuário, quebra em tarefas operacionais, critérios de qualidade (DoD) e aplicação prática dos frameworks ágeis Scrum e Kanban.

---

## 1. O que é Gestão de Projetos de Software?

A **Gestão de Projetos** é a aplicação sistemática de conhecimentos, habilidades, ferramentas e técnicas às atividades de um projeto com o objetivo de atender ou superar as expectativas das partes interessadas (*stakeholders*), entregando valor de negócio de forma previsível e sustentável.

No contexto de engenharia de software e desenvolvimento front-end, a gestão não se resume a cronogramas estáticos: ela organiza o fluxo de trabalho de desenvolvedores, designers e clientes, garantindo que o produto certo seja construído com qualidade técnica e entregue dentro de prazos e recursos viáveis.

---

## 2. Problemas Comuns em Projetos sem Gestão Adequada

Projetos de software executados sem processos estruturados enfrentam gargalos recorrentes que comprometem a saúde do time e a entrega do produto:

- **Conflitos Graves de Código no Git (*Merge Conflicts*):** Vários desenvolvedores editando simultaneamente os mesmos arquivos sem divisão clara de módulos, ramos (*branches*) padronizados ou comunicação constante, resultando em horas perdidas resolvendo conflitos manuais.
- **Prazos Ultrapassados (*Deadlines Perdidas*):** Falta de visibilidade sobre o esforço real exigido por cada funcionalidade, gerando atrasos em cascata e entregas sob estresse.
- **Escopo Descontrolado (*Scope Creep*):** Inclusão contínua de novas ideias e alterações no meio do desenvolvimento sem replanejamento de prazo ou capacidade da equipe.
- **Falta de Priorização e Retrabalho:** Desenvolvedores gastando energia em recursos secundários enquanto fluxos críticos de negócio continuam incompletos ou mal especificados.
- **Acúmulo de Débito Técnico:** Ausência de padrões de qualidade, testes automatizados e code review, transformando o código em uma estrutura frágil e propensa a falhas em produção.

---

## 3. Engenharia de Requisitos: Funcionais vs. Não-Funcionais

**Requisitos** definem o que o sistema deve fazer e quais restrições operacionais deve respeitar:

### Requisitos Funcionais (RF)
Descrevem as **ações, comportamentos e funcionalidades diretas** que o sistema deve oferecer aos usuários:
- *Exemplo 1:* "O usuário deve ser capaz de criar uma conta informando nome, e-mail e senha."
- *Exemplo 2:* "A aplicação front-end deve exibir uma listagem paginada das notas cadastradas."
- *Exemplo 3:* "O sistema deve permitir a exclusão de registros com confirmação prévia."

### Requisitos Não-Funcionais (RNF)
Descrevem os **atributos de qualidade, restrições técnicas, desempenho e segurança** da aplicação:
- *Desempenho:* "A página inicial deve carregar o conteúdo principal em menos de 1,5 segundos em conexões 4G."
- *Acessibilidade:* "A interface deve atender às diretrizes WCAG 2.1 nível AA, garantindo contraste adequado e navegação via teclado."
- *Responsividade:* "O layout deve se adaptar fluidamente a resoluções desde 360px (mobile) até 1920px (desktop)."
- *Segurança:* "Todas as comunicações com a API devem ser criptografadas via protocolo HTTPS."

---

## 4. Requisitos Iniciais do Projeto Integrador

Na etapa de concepção do projeto integrador da disciplina, realizou-se o levantamento inicial de requisitos, regras de negócio e mapeamento funcional preliminar da aplicação:

- **Planilha de Requisitos e Organização Inicial:**
  [📄 Book 3.xlsx](https://2rpnet-my.sharepoint.com/:x:/p/joao_junior/IQAVfcLito34QquhctpNVAPaAcvD_EJHTU2c5fPpm5AMNN8?e=iHIm4A)
  *(Documento central contendo o catálogo inicial de requisitos levantados, prioridades e estruturação dos módulos do projeto integrador).*

---

## 5. User Stories (Histórias de Usuário)

Uma **User Story** é uma descrição concisa e informal de uma funcionalidade do sistema escrita do ponto de vista do usuário final. Seu objetivo é manter o foco no valor de negócio entregue, e não em termos estritamente técnicos.

### O Formato Padrão

```text
Como [persona / tipo de usuário],
Eu quero [ação / objetivo],
Para que [benefício / valor de negócio gerado].
```

#### Exemplos Práticos:
- *Exemplo 1:*  
  **Como** um usuário cadastrado,  
  **Eu quero** filtrar minhas anotações por tags ou palavras-chave,  
  **Para que** eu encontre informações importantes com agilidade sem precisar percorrer toda a lista.
- *Exemplo 2:*  
  **Como** administrador do sistema,  
  **Eu quero** visualizar um painel gráfico com o número de usuários ativos por dia,  
  **Para que** eu possa acompanhar o crescimento da plataforma e planejar a infraestrutura.

### Critérios de Aceitação (*Acceptance Criteria*)
Toda User Story precisa de regras claras que definem quando ela é considerada aceita pelo Product Owner (PO). Utiliza-se com frequência o padrão **BDD (Given-When-Then / Dado-Quando-Então)**:
- **Dado que** o usuário está na tela de anotações e possui 10 notas cadastradas;
- **Quando** ele digita "reunião" no campo de busca;
- **Então** apenas as anotações contendo o termo "reunião" no título ou no corpo devem ser exibidas imediatamente na interface.

---

## 6. Quebra de Histórias em Tarefas Técnicas (*Tasks*)

Uma User Story costuma ser ampla demais para ser codificada como uma única unidade de trabalho. Por isso, a equipe de desenvolvimento a decompõe em **Tarefas Técnicas (Tasks)** menores e acionáveis:

### Exemplo de Decomposição:
Para a história *"Como usuário, eu quero poder editar uma nota existente..."*:
1. **Task Front-end (UI):** Desenvolver o modal de edição contendo campos pré-populados com os dados atuais da nota.
2. **Task Front-end (Integração):** Implementar chamada assíncrona `PUT /api/notes/:id` via `fetch` tratando respostas de sucesso e erro.
3. **Task Back-end (API):** Desenvolver rota `PUT /api/notes/:id` no Express validando os campos obrigatórios.
4. **Task Testes:** Escrever testes unitários para a validação dos campos e teste de integração no Postman.
