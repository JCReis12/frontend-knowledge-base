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


---

## 7. Gestão de Tarefas e Priorização de Backlog

O **Backlog do Produto** é a lista viva e dinâmica de tudo o que pode ser necessário no produto (novas funcionalidades, melhorias de infraestrutura, correções de bugs e pesquisas técnicas). 

Como o tempo e a capacidade da equipe são limitados, a priorização é fundamental. Dois métodos amplamente utilizados são:

### 1. Método MoSCoW
Classifica os itens do backlog em quatro categorias de urgência:
- **Must Have (Obrigatório):** Itens essenciais sem os quais o produto não funciona ou não atende a regulações legais mínimas.
- **Should Have (Importante):** Itens de alto valor de negócio que agregam bastante, mas que possuem contornos provisórios se necessário.
- **Could Have (Desejável):** Pequenas melhorias e refinamentos que só são desenvolvidos se sobrar tempo e capacidade.
- **Won't Have (Não prioritário no momento):** Itens acordados formalmente como fora do escopo do ciclo atual, podendo ser reavaliados no futuro.

### 2. Matriz de Impacto vs. Esforço
Auxilia na tomada de decisão rápida:
- **Alto Impacto e Baixo Esforço (*Quick Wins*):** Devem ser priorizados imediatamente.
- **Alto Impacto e Alto Esforço (*Projetos Estratégicos*):** Planejados com cuidado e divididos em entregas menores.
- **Baixo Impacto e Baixo Esforço (*Preenchedores*):** Executados apenas em lacunas de tempo.
- **Baixo Impacto e Alto Esforço (*Ralos de Tempo*):** Devem ser descartados ou repensados.

---

## 8. Critérios de Qualidade: Definition of Ready (DoR) e Definition of Done (DoD)

Para evitar ambiguidades entre o que está pronto para ser desenvolvido e o que está pronto para ser entregue aos usuários, utilizam-se acordos explícitos:

### Definition of Ready (DoR - Definição de Preparado)
Critérios que uma User Story deve cumprir **antes de entrar na Sprint ou começar a ser codificada**:
- Descrição clara com persona, ação e benefício.
- Critérios de aceitação definidos e aprovados pelo PO.
- Dependências técnicas mapeadas e resolvidas.
- Estimativa de complexidade realizada pelo time técnico.
- Protótipos de tela (wireframes/Figma) disponíveis para consulta.

### Definition of Done (DoD - Definição de Pronto)
Critérios de qualidade que garantem que uma tarefa está **100% finalizada e pronta para produção**:
- Código-fonte escrito e revisado por pares via *Pull Request* (*Code Review* aprovado).
- Testes unitários e de integração executados com sucesso sem regressões.
- Padrões de código e linting atendidos (sem warnings graves do ESLint/Prettier).
- Build executado com sucesso e homologado em ambiente de testes/staging.
- Documentação atualizada (ex.: README, Swagger ou Postman).

---

## 9. O Framework Ágil Scrum

O **Scrum** é um framework leve e iterativo para o desenvolvimento e sustentação de produtos complexos, estruturado em três pilares fundamentais: **Transparência, Inspeção e Adaptação**.

### Papéis no Scrum (*Scrum Roles*)
1. **Product Owner (PO):** Representa os clientes e o negócio. É o responsável único por maximizar o valor do produto e gerenciar o Product Backlog (priorizando o que traz maior retorno).
2. **Scrum Master (SM):** Líder facilitador e guardião do processo Scrum. Atua removendo impedimentos técnicos e organizacionais que bloqueiam o time e garantindo que os princípios ágeis sejam compreendidos e aplicados.
3. **Developers (Time de Desenvolvimento):** Equipe multidisciplinar e auto-organizável de profissionais (engenheiros front-end, back-end, QA, designers) responsáveis por transformar os itens do backlog em um incremento funcional utilizável a cada iteração.

### Ciclos e Cerimônias do Scrum
O trabalho é executado em blocos temporais fixos denominados **Sprints** (geralmente com duração de 1 a 4 semanas):

- **Sprint Planning (Planejamento da Sprint):** O PO apresenta os itens prioritários do Product Backlog, o time discute o escopo técnico e seleciona o conjunto de itens que comporá o **Sprint Backlog**, definindo o objetivo da Sprint (*Sprint Goal*).
- **Daily Scrum (Reunião Diária):** Reunião diária de alinhamento de 15 minutos onde cada desenvolvedor compartilha:
  - O que concluiu ontem para ajudar no objetivo da Sprint?
  - O que pretende realizar hoje?
  - Existe algum bloqueio ou impedimento no caminho?
- **Sprint Review (Revisão da Sprint):** Demonstração prática do incremento de software funcional entregue aos *stakeholders*, coletando feedback real para os próximos ciclos.
- **Sprint Retrospective (Retrospectiva da Sprint):** Reunião interna da equipe focada em melhoria contínua de processos: avalia o que funcionou bem, o que falhou na comunicação ou ferramentas e define planos de ação para a Sprint seguinte.

---

## 10. O Método Kanban

O **Kanban** é uma metodologia visual de gestão de fluxo de trabalho originária do sistema Toyota de produção, adaptada para o desenvolvimento de software para promover um fluxo contínuo e equilibrado de entregas.

### Princípios Fundamentais do Kanban:
1. **Visualizar o Fluxo de Trabalho:** Tornar todas as tarefas visíveis em um quadro físico ou digital (*Kanban Board*).
2. **Limitar o Trabalho em Progresso (*WIP - Work In Progress*):** Estabelecer um número máximo de tarefas que podem estar em determinada coluna simultaneamente (ex.: no máximo 3 tarefas em "In Progress"). Evita a sobrecarga do time e combate o desperdício de iniciar muitas tarefas sem concluir nenhuma (*"Pare de começar, comece a terminar"*).
3. **Gerenciar e Otimizar o Fluxo:** Identificar gargalos rapidamente (ex.: acúmulo de tarefas na coluna de *Code Review*) e focar a equipe em desobstruí-los.

### Quadro Kanban Típico no Desenvolvimento Front-end

```text
┌──────────────┬──────────────┬──────────────┬──────────────┬──────────────┐
│   Backlog    │    To Do     │ In Progress  │ Code Review  │     Done     │
│              │              │  (WIP: 3)    │  (WIP: 2)    │              │
├──────────────┼──────────────┼──────────────┼──────────────┼──────────────┤
│ [Card #104]  │ [Card #102]  │ [Card #99]   │ [Card #97]   │ [Card #90]   │
│ [Card #105]  │ [Card #103]  │ [Card #100]  │ [Card #98]   │ [Card #91]   │
│              │              │ [Card #101]  │              │ [Card #92]   │
└──────────────┴──────────────┴──────────────┴──────────────┴──────────────┘
```

### Comparativo: Scrum vs. Kanban

| Critério | Scrum | Kanban |
| --- | --- | --- |
| **Cadência de Entrega** | Em lotes regulares ao fim de cada Sprint (1 a 4 semanas) | Fluxo contínuo sob demanda (deploy assim que pronto) |
| **Prazos e Escopo** | Timebox fixo; o escopo da Sprint não deve mudar após iniciado | Flexível; novos itens podem entrar assim que houver espaço no WIP |
| **Papéis Definidos** | PO, Scrum Master e Developers obrigatórios | Sem papéis prescritos (papéis adaptados conforme a equipe) |
| **Métrica Principal** | Velocidade da equipe (*Velocity* - pontos por Sprint) | *Lead Time* (tempo da ideia ao deploy) e *Cycle Time* (tempo de desenvolvimento ativo) |

---

## 11. Revisão Rápida da Aula 06

- **Gestão de Projetos:** Prática indispensável para mitigar conflitos de Git, atrasos de prazo e débito técnico no ciclo de software.
- **Requisitos:** Funcionais definem o comportamento do sistema; Não-Funcionais definem parâmetros técnicos de desempenho, acessibilidade e segurança.
- **User Story:** Narrativa focada em valor para o usuário final no padrão *"Como... Quero... Para..."*, acompanhada de critérios de aceitação objetivos.
- **DoD (Definition of Done):** Acordo explícito de qualidade que atesta que o código foi testado, revisado e está pronto para entrega.
- **Scrum:** Framework baseado em Sprints com papéis bem definidos (PO, SM, Time) e cerimônias focadas em inspeção e adaptação.
- **Kanban:** Gestão visual de fluxo contínuo focada no controle de limites de trabalho em progresso (WIP) e redução de gargalos.

---

## 12. Perguntas para Testar o Conhecimento

1. Por que a ausência de uma divisão estruturada de tarefas e branches pode causar conflitos graves no Git em equipes de front-end?
2. Qual a diferença prática entre um Requisito Funcional e um Requisito Não-Funcional? Dê um exemplo de cada aplicável a um projeto web.
3. Como a fórmula padrão das User Stories ajuda a evitar a criação de recursos desnecessários para o usuário?
4. O que diferencia o *Definition of Ready (DoR)* do *Definition of Done (DoD)*?
5. Qual é o principal benefício de aplicar limites de WIP (*Work in Progress*) em um quadro Kanban?
