# Aula 03 – Projetos com Frameworks Front-end

## Objetivo da Aula

A terceira aula teve como objetivo apresentar o ecossistema dos **Frameworks Front-end**, discutindo sua importância no desenvolvimento moderno, as diferenças conceituais entre bibliotecas e frameworks, as características arquiteturais das principais ferramentas do mercado (**React**, **Angular**, **Vue.js** e **Next.js**), além de instruir a criação prática de projetos, a compreensão de suas estruturas de arquivos e o fluxo de trabalho com versionamento no Git e GitHub.

---

# Introdução aos Frameworks Front-end

Um **framework front-end** é um conjunto integrado de ferramentas, bibliotecas, padrões e convenções que padronizam e organizam o desenvolvimento de interfaces web. Ele fornece uma arquitetura pré-definida, acelerando consideravelmente a concepção de aplicações complexas e escaláveis.

### Comparação: Vanilla JS vs. Frameworks Front-end

* **Desenvolvimento Puro (Vanilla JS):**
  * Construção e manipulação manual de elementos no DOM;
  * Maior propensão a código repetitivo e desorganizado;
  * Dificuldade no rastreamento de estados compartilhados;
  * Manutenção complexa à medida que a aplicação cresce.

* **Desenvolvimento com Frameworks:**
  * Arquitetura modular baseada em **componentes reutilizáveis**;
  * **Gerenciamento de estado** reativo e centralizado;
  * Atualizações eficientes da interface de usuário (UI);
  * Facilidade de manutenção, separação de responsabilidades e escalabilidade.

---

# Diferenças entre Framework e Biblioteca

Compreender a diferença entre biblioteca (*library*) e framework é um conceito clássico e fundamental na engenharia de software front-end:

### Biblioteca (*Library*)
* **Você controla o fluxo**: O código da aplicação decide quando e onde importar e chamar as funções ou classes da biblioteca.
* **Flexibilidade máxima**: Não impõe uma estrutura rígida para o projeto nem dita a arquitetura global.
* **Exemplos**: **React**, jQuery, Lodash, Axios.
* *Exemplo prático*: Você decide quando e onde invocar `ReactDOM.createRoot()` ou chamar componentes específicos.

### Framework
* **Inversão de Controle (*Inversion of Control - IoC*)**: O framework dita e controla o ciclo de vida e o fluxo de execução da aplicação; ele chama o seu código nos momentos adequados.
* **Estrutura definida e padronizada**: Impõe convenções, organização de pastas e padrões arquiteturais obrigatórios.
* **Exemplos**: **Angular**, **Vue.js**, **Next.js**.
* *Exemplo prático*: O Angular define exatamente quando renderizar componentes, injetar dependências e disparar eventos do ciclo de vida.

---

# Por que Utilizar um Framework?

O uso de frameworks modernos consolidou-se como padrão de mercado devido a vantagens determinantes:

1. **Produtividade Aumentada**: Elimina a necessidade de "reinventar a roda", disponibilizando soluções prontas e testadas para roteamento, controle de estado, requisições HTTP e renderização.
2. **Melhores Práticas**: Estimula a organização orientada a componentes desacoplados, design patterns reconhecidos e separação lógica de responsabilidades.
3. **Manutenção Facilitada**: Implementa mecanismos avançados de atualização visual, como o **Virtual DOM** (React/Vue) e **Change Detection** (Angular), reduzindo bugs de sincronização.
4. **Comunidade e Suporte**: Ampla documentação oficial, vasta quantidade de pacotes/plugins disponíveis e ecossistemas ativos para resolução de problemas cotidianos.

> **Conceito de Stack**: Refere-se ao conjunto articulado de linguagens, bibliotecas, frameworks e ferramentas empregadas em conjunto para construir e executar uma aplicação completa.

---

# Características Fundamentais dos Frameworks Front-end

Os frameworks modernos compartilham um conjunto de características técnicas essenciais:

* **Estrutura de Código Organizada**: Separação clara entre lógica, estrutura e apresentação, permitindo componentização eficiente e manutenção sustentável.
* **Componentização**: Divisão da interface em blocos autônomos, reutilizáveis e com encapsulamento de lógica e estilo, garantindo que alterações isoladas não causem efeitos colaterais indesejados.
* **Programação Reativa**: A interface de usuário (UI) reflete e sincroniza automaticamente qualquer alteração no estado da aplicação, eliminando a manipulação direta e imperativa do DOM.
* **Ferramentas de Build e Bundling**: Mecanismos integrados para transpilação (TypeScript/Babel), minificação, empacotamento (*bundling*) e otimização para navegadores.
* **Sistema de Rotas**: Suporte nativo ou via biblioteca oficial para **Single Page Applications (SPAs)**, possibilitando transição fluida entre telas sem recarregamento da página.
* **Integração com APIs**: Estruturas facilitadas para chamadas assíncronas (REST/GraphQL) e sincronização de dados externos com a UI.
* **Padrões de Design e Acessibilidade**: Bibliotecas e convenções que promovem diretrizes de acessibilidade (a11y) e boas práticas de UX/UI.
* **Suporte a Testes**: Ferramentas e utilitários integrados para execução de testes unitários, testes de componentes e testes de integração.

---

# Introdução ao React

Criado pelo **Facebook** em 2013, o **React** é uma biblioteca JavaScript focada na construção de interfaces de usuário dinâmicas e reativas baseadas em componentes.

### Fundamentos Técnicos do React

#### 1. DOM Tradicional vs. Virtual DOM
* **DOM (Document Object Model)**: Estrutura em formato de árvore gerada pelo navegador para representar o HTML. Alterar elementos diretamente no Real DOM com frequência pode gerar perda significativa de desempenho devido ao recálculo constante de layout e repintura de tela (*reflow* e *repaint*).
* **Virtual DOM**: Cópia leve e rápida do DOM mantida em memória pelo React. Quando o estado muda, o React gera um novo Virtual DOM, compara-o com a versão anterior (processo denominado **Diffing / Reconciliação**) e calcula o conjunto mínimo de alterações necessárias para aplicar de forma pontual no Real DOM.

#### 2. JSX (JavaScript XML)
Extensão de sintaxe que permite escrever código visual semelhante a HTML diretamente dentro do JavaScript/TypeScript:
* Expressões JavaScript são interpoladas entre chaves `{}`;
* Atributos seguem o padrão *camelCase* (ex.: `className` ao invés de `class`, `htmlFor` ao invés de `for`);
* Todas as tags devem ser estritamente fechadas (ex.: `<img />`, `<input />`).

#### 3. React Hooks
Funções especiais introduzidas para permitir o controle de estado e ciclo de vida em componentes funcionais:
* **`useState`**: Declara e manipula variáveis de estado reativo dentro do componente funcional.
* **`useEffect`**: Executa e controla efeitos colaterais na aplicação, tais como requisições a APIs externas, manipuladores de eventos globais e subscrições.

#### 4. Gerenciamento de Estado
* **Context API**: Mecanismo nativo do React para compartilhar dados entre múltiplos componentes sem a necessidade de repassar propriedades manualmente em vários níveis (*prop drilling*), ideal para escopos pequenos e médios.
* **Redux / Bibliotecas de Estado Global**: Soluções robustas indicadas para aplicações de grande porte com fluxos complexos de compartilhamento de dados globais.

---

# Angular: Criação e Estrutura de Projetos

O **Angular** é um framework completo e opinativo mantido pelo **Google**, projetado para o desenvolvimento de Single Page Applications (SPAs) corporativas e de grande porte.

### Destaques e Requisitos
* **Pré-requisitos**: Node.js instalado e conceitos de Programação Orientada a Objetos (POO);
* **Solução Completa ("Baterias Inclusas")**: Fornece nativamente roteamento, cliente HTTP, formulários reativos e injeção de dependências;
* **TypeScript Nativo**: Forte tipagem estática que previne erros em tempo de compilação;
* **Arquitetura Baseada em Componentes / MVC**: Separação estruturada de responsabilidades;
* **Angular CLI**: Linha de comando poderosa para automação de tarefas de criação, compilação e testes.

### Conceitos Fundamentais
* **`@Component`**: Decorator que acopla a classe TypeScript, o template HTML e os estilos CSS;
* **`@NgModule`**: Agrupamento funcional de componentes, diretivas, pipes e serviços relacionados;
* **`@Injectable`**: Declara serviços reutilizáveis injetáveis via Injeção de Dependências (*Dependency Injection*);
* **Data Binding**: Interpolação textual com `{{ }}`, vinculação de propriedades `[propriedade]`, eventos `(evento)` e *Two-Way Data Binding* com `[(ngModel)]`;
* **Roteamento**: Gerenciado pelo módulo oficial `RouterModule`.

### Passo a Passo de Criação
```bash
# 1. Instalar o Angular CLI globalmente
npm install -g @angular/cli

# 2. Criar um novo projeto Angular
ng new meu-app-angular

# 3. Entrar na pasta do projeto criado
cd meu-app-angular

# 4. Abrir no editor de código
code .

# 5. Iniciar o servidor de desenvolvimento local (porta padrão 4200)
ng serve
```

### Estrutura de Pastas e Arquivos
* **`node_modules/`**: Pacotes e dependências externas instaladas;
* **`public/`**: Recursos estáticos públicos (imagens, ícones, arquivos independentes de build);
* **`src/`**: Diretório principal do código-fonte:
  * **`app/`**: Componentes, módulos, serviços e rotas centrais da aplicação;
  * **`index.html`**: Arquivo HTML raiz contendo o elemento de entrada `<app-root>`;
  * **`main.ts`**: Ponto de entrada do script que inicializa a aplicação no DOM;
  * **`styles.css`**: Estilos globais da aplicação;
  * **`main.server.ts` e `server.ts`**: Pontos de entrada e configuração para Angular Universal (SSR - Server-Side Rendering);
* **`.angular/` e `.vscode/`**: Configurações de cache e ambiente de desenvolvimento (ignoradas no versionamento);
* **`angular.json`**: Arquivo mestre de configuração do projeto, compilação e rotinas do CLI;
* **`tsconfig.json` (e variantes `tsconfig.app.json`, `tsconfig.spec.json`)**: Configurações do compilador TypeScript.

---

# Vue.js: Criação e Estrutura de Projetos

O **Vue.js** é um framework progressivo criado por Evan You, projetado para ser adotado incrementalmente e com excelente curva de aprendizado.

### Destaques e Requisitos
* **Pré-requisitos**: Node.js instalado e conhecimento sólido de HTML, CSS e JavaScript/TypeScript;
* **Framework Progressivo**: Pode atuar desde uma simples biblioteca importada via CDN até uma base completa para SPAs avançadas;
* **Single-File Components (SFC)**: Componentes armazenados em arquivos `.vue` únicos, contendo `<template>`, `<script>` e `<style>` organizados e escopados;
* **Reatividade Transparente**: Sistema nativo de reatividade automática e de alto desempenho;
* **Build com Vite**: Inicialização ultrarrápida do ambiente de desenvolvimento.

### Passo a Passo de Criação
```bash
# 1. Criar o projeto utilizando o scaffold oficial do Vue baseado em Vite
npm create vue@latest

# 2. Navegar até o diretório gerado
cd meu-projeto-vue

# 3. Instalar as dependências do projeto
npm install

# 4. Abrir no VS Code
code .

# 5. Executar o servidor de desenvolvimento (porta padrão 5173)
npm run dev
```

### Estrutura de Pastas e Arquivos
* **`node_modules/`**: Bibliotecas e dependências gerenciadas pelo npm;
* **`public/`**: Arquivos estáticos que não sofrem processamento pelo Vite (ex.: `favicon.ico`, `robots.txt`);
* **`src/`**: Diretório principal de desenvolvimento:
  * **`assets/`**: Estilos globais, fontes e imagens processados pelo empacotador;
  * **`components/`**: Componentes reutilizáveis do projeto;
  * **`App.vue`**: Componente raiz da aplicação que orquestra a estrutura geral;
  * **`main.js`**: Ponto de entrada que instancia o Vue, registra plugins e monta a aplicação no DOM;
* **`index.html`**: Arquivo HTML único contendo a div contêiner `<div id="app"></div>`;
* **`vite.config.js`**: Arquivo de configurações do Vite (plugins, aliases de caminhos e portas);
* **`package.json`**: Metadados, scripts operacionais e dependências do projeto.

---

# Next.js: Criação e Estrutura de Projetos

O **Next.js** é um framework de produção construído sobre o **React**, desenvolvido pela Vercel, projetado para criar aplicações web modernas e full-stack com alto desempenho e SEO otimizado.

### Diferenciais em Relação ao React Puro
* **Roteamento Baseado em Sistema de Arquivos (*App Router*)**: Diretórios e arquivos definem rotas de forma declarativa e automática;
* **Renderização Híbrida e SSR**: Suporte nativo a *Server-Side Rendering* (SSR) e *Static Site Generation* (SSG);
* **React Server Components (RSC)**: Componentes processados diretamente no servidor, reduzindo o envio de JavaScript para o cliente;
* **Otimização Nativa de Recursos**: Componentes inteligentes para fontes, scripts e imagens;
* **Camada de API Backend Integrada**: Capacidade de criar *Route Handlers* e endpoints de backend no mesmo projeto.

### Passo a Passo de Criação
```bash
# 1. Criar um projeto Next.js interativo com ferramentas pré-configuradas
npx create-next-app@latest meu-projeto

# 2. Acessar a pasta criada
cd meu-projeto

# 3. Abrir no VS Code
code .

# 4. Iniciar o servidor local (porta padrão 3000)
npm run dev
```

### Estrutura de Pastas e Arquivos (App Router)
* **`app/`**: Diretório central da aplicação:
  * **`page.js` / `page.tsx`**: Representa a interface visual correspondente à rota do diretório;
  * **`layout.js` / `layout.tsx`**: Define layouts reutilizáveis que preservam o estado entre navegações;
* **`public/`**: Recursos estáticos acessíveis diretamente pela URL raiz;
* **`.next/`**: Diretório gerado automaticamente contendo os artefatos de compilação e cache;
* **`next.config.ts` / `next.config.mjs`**: Arquivo de configurações avançadas do Next.js.

---

# Importando e Explorando Projetos Modelos (Templates)

Encontrar projetos modelos desenvolvidos em repositórios abertos acelera significativamente o desenvolvimento e possibilita o aprendizado de arquiteturas consolidadas:

* **GitHub**: Plataforma de busca de repositórios open-source para clonagem direta via comando `git clone <url>`.
* **Vercel Templates**: Catálogo de modelos pré-configurados prontos para deploy e estudo de boas práticas.
* **CodeSandbox**: Ambiente em nuvem para exploração, teste rápido e compartilhamento de templates front-end sem necessidade de configuração de máquina local.

---

# Versionamento e Boas Práticas com Git e GitHub

Durante a condução de projetos front-end em equipe, práticas sólidas de controle de versão são fundamentais:

* **Uso Rigoroso do `.gitignore`**: Garantir que diretórios pesados ou temporários como `node_modules/`, `.angular/`, `.next/` e arquivos de ambiente (`.env`) jamais sejam versionados;
* **Histórico de Commits Semântico**: Registrar a evolução funcional do projeto com commits pequenos, claros e objetivos;
* **Repositórios Independentes**: Manter cada tecnologia ou módulo isolado em seu próprio repositório para evitar conflitos de dependências e pipelines.

---

# Atividades Práticas da Aula

A atividade prática definida para a aula consiste em desenvolver projetos práticos em grupo aplicando as diferentes tecnologias apresentadas:

### Proposta
Desenvolver, em grupo, projetos web abordando o **mesmo tema**, explorando as especificidades e ecossistemas de cada solução. Cada aplicação deve conter uma página funcional, responsiva e estruturada a partir de componentes.

### Escopo das Entregas
1. **Projeto 01 — React**: Aplicação desenvolvida com a biblioteca React, explorando componentes funcionais e hooks.
2. **Projeto 02 — Vue.js**: Aplicação desenvolvida em Vue 3, utilizando Single-File Components (`.vue`).
3. **Projeto 03 — Angular**: Aplicação criada via Angular CLI, adotando TypeScript e separação de responsabilidades.
4. **Projeto 04 — Next.js**: Aplicação moderna desenvolvida com Next.js, explorando a estrutura do App Router.
5. **Projeto 05 — Cópia e Adaptação de Template**: Projeto obtido e customizado a partir de um repositório ou template de referência da comunidade.

### Requisitos Adicionais
* Todos os projetos devem ser versionados individualmente no GitHub com histórico contínuo de commits;
* Elaboração de uma **síntese comparativa** destacando as principais diferenças, vantagens, dificuldades e pontos fortes observados durante o desenvolvimento em cada uma das tecnologias.

---

# Conclusão

A Aula 03 estabeleceu uma base sólida sobre o ecossistema front-end contemporâneo, esclarecendo o papel de bibliotecas e frameworks na produtividade do desenvolvedor e na escalabilidade de software.

Ao contrastar a flexibilidade do **React**, a completude do **Angular**, a progressividade do **Vue.js** e o poder full-stack do **Next.js**, os alunos foram capacitados a inicializar projetos com as ferramentas oficiais de linha de comando, compreender a função de cada pasta e arquivo estrutural, e exercitar a criação de projetos reais com controle de versão e boas práticas de engenharia de software.
