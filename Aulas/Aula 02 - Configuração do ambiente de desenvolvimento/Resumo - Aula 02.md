# Resumo da aula — Versionamento

## Comparação entre Versionamento e Backup

### Versionamento

- É o processo de **registrar e identificar as diferentes versões** de um documento ou software.
- Cada alteração pode ser acompanhada ao longo do tempo.
- Permite saber:
  - **O que** foi alterado;
  - **Quem** alterou;
  - **Quando** alterou;
  - **Por que** foi alterado.
- Permite voltar para versões anteriores de forma mais específica.
- Facilita a colaboração entre vários desenvolvedores.

### Backup

- É uma **cópia de segurança** de um arquivo ou projeto em determinado momento.
- Representa um **estado pontual** do projeto.
- Não possui necessariamente informações sobre:
  - Quem fez a alteração;
  - Quando fez;
  - Por que fez.
- Normalmente, a recuperação consiste em restaurar uma cópia completa.

> **Resumo:** Backup protege contra perda de dados; versionamento permite **acompanhar, comparar e recuperar o histórico de alterações**.

---

## Caos que aconteceria sem versionamento

Sem um sistema de versionamento, o projeto poderia ficar desorganizado e difícil de controlar.

- Arquivos duplicados e sem contexto:
  - `versao_final.zip`
  - `versao_final_agora_sim.zip`
  - `versao_final_agora_sim2.zip`
- **Código perdido:** uma alteração pode apagar dias de trabalho.
- **Conflitos entre desenvolvedores:** dois programadores podem editar o mesmo arquivo ao mesmo tempo.
- **Sem histórico:** não é possível saber facilmente o que mudou e quando.
- Dificuldade para recuperar uma versão específica do projeto.

---

## Benefícios do Versionamento

- **Trabalho simultâneo**
   Vários desenvolvedores podem trabalhar no mesmo projeto.

- **Menos retrabalho**  
    Conflitos podem ser identificados antes de causarem grandes perdas.

- **Auditoria e rastreabilidade**  
    É possível saber quem alterou determinada parte do projeto, quando e o que foi alterado.

- **Recuperação de versões**  
    Permite retornar para uma versão anterior caso alguma alteração cause problemas.

- **Controle de mudanças**  
    Facilita a integração das alterações feitas pelos membros da equipe.

- **Colaboração**  
    Permite utilizar branches para desenvolver novas funcionalidades sem afetar diretamente a versão principal.

- **Qualidade**  
    Permite testar alterações antes de disponibilizá-las na versão final.

- **Aprimoramento contínuo**  
    O histórico permite acompanhar a evolução do projeto.

---

# O que é Versionamento?

- **Versionamento** é o processo de atribuir um identificador para cada versão de um documento ou software.
- Cada versão representa um determinado estado do projeto.
- Pode utilizar:
  - **Números:** `v1.0`, `v1.1`, `v2.0`
  - **Datas:** `2023-10-01`
- Registra as mudanças realizadas ao longo do tempo.
- Facilita:
  - Organização;
  - Colaboração;
  - Rastreamento das alterações;
  - Recuperação de versões anteriores;
  - Auditoria.

---

# O que é SemVer?

**SemVer** significa **Semantic Versioning (Versionamento Semântico)**.

- É uma convenção para definir **como os números das versões de um software devem ser organizados**.
- O objetivo é deixar claro, apenas olhando para o número da versão, **qual foi o tipo de mudança realizada**.
- Utiliza o padrão:

```text
MAJOR.MINOR.PATCH
```

Exemplo:

```text
2.1.3
```

Cada número possui um significado diferente.

---

# MAJOR . MINOR . PATCH

## MAJOR

```text
2.0.0
```

- Indica uma **mudança incompatível** com versões anteriores.
- Pode fazer com que códigos que funcionavam na versão anterior precisem ser modificados.

### Exemplo

```text
1.0.0 → 2.0.0
```

A nova versão possui uma alteração que **quebra a compatibilidade** com a anterior.

---

## MINOR

```text
1.1.0
```

- Indica a **adição de uma nova funcionalidade**.
- A nova funcionalidade deve manter a compatibilidade com versões anteriores.

### Exemplo

```text
1.0.0 → 1.1.0
```

Foi adicionada uma funcionalidade, mas o que já funcionava continua funcionando.

---

## PATCH

```text
1.0.1
```

- Indica uma **correção de bug**.
- Não deve quebrar a compatibilidade existente.

### Exemplo

```text
1.1.0 → 1.1.1
```

Foi encontrado um erro e ele foi corrigido, sem adicionar uma nova funcionalidade significativa.

---

# Exemplos de Versionamento Semântico

```text
1.0.0 → Primeira versão estável
1.1.0 → Adição de uma nova funcionalidade compatível
1.1.1 → Correção de um bug
2.0.0 → Mudança incompatível com a versão anterior
```

### Versões `0.x.x`

- Versões como `0.1.0` e `0.2.0` indicam **desenvolvimento inicial**.
- A versão `1.0.0` marca o lançamento público estável do software.

---

# Tipos de Alterações no Código

- **Bug Fix**  
    Correção de erros no código.

- **New Feature**  
    Adição de uma nova funcionalidade.

- **Feature Enhancement**
    Melhoria de uma funcionalidade existente.

- **Refactoring**  
    Reorganização do código para deixá-lo mais limpo e eficiente, sem necessariamente alterar seu comportamento.

- **Performance**  
    Alterações para melhorar velocidade e eficiência.

- **Security Patch**  
    Correção de vulnerabilidades de segurança.

- **Dependency Update**  
    Atualização das bibliotecas e frameworks utilizados.

- **Adding Tests**  
    Adição de testes automatizados para verificar a qualidade do código.

---

# Por que usar SemVer?

- Facilita o **gerenciamento de dependências**.
- Ajuda desenvolvedores a entenderem o impacto de uma atualização.
- Dá mais **clareza** sobre o tipo de alteração realizada.
- Facilita a **manutenção** do software.
- Torna o comportamento das versões mais **previsível**.

### Forma rápida de lembrar

```text
MAJOR → Quebrou compatibilidade
MINOR → Nova funcionalidade
PATCH → Correção de bug
```

> **Exemplo:** `2.4.7`
>
> `2` = versão principal  
> `4` = novas funcionalidades  
> `7` = correções de bugs


---

# Ambiente de Desenvolvimento e Ferramentas

## Visual Studio Code (VS Code)

O **Visual Studio Code** é o editor de código-fonte mais utilizado no desenvolvimento web moderno. Desenvolvido pela Microsoft, é gratuito, de código aberto, multiplataforma (Windows, macOS, Linux) e altamente extensível.

### Editor de Código vs. IDE

- **Editor de Código (ex.: VS Code, Sublime Text):** Ferramenta focada em edição rápida de texto e código, leve, cujo ecossistema de funcionalidades (depuração, integração com controle de versão, suporte a linguagens) é habilitado sob demanda por meio de extensões e plugins.
- **IDE - Integrated Development Environment (ex.: WebStorm, Eclipse, Visual Studio):** Ambiente completo integrado que já vem de fábrica com compiladores, depuradores avançados, gerenciadores de banco de dados e ferramentas de automação, porém consome mais recursos de hardware.

### Recursos Essenciais do VS Code

- **Terminal Integrado:** Permite executar comandos do PowerShell, Bash ou Git Bash sem sair da janela do editor.
- **Controle de Versão Embutido:** Interface gráfica para monitorar mudanças, realizar commits, visualizar diffs e alternar branches.
- **IntelliSense:** Autocompletar inteligente baseado em tipos de variáveis, assinaturas de funções e módulos importados.
- **Depuração (Debugging):** Pontos de interrupção (breakpoints), inspeção de variáveis e pilha de chamadas diretamente no editor.

### Extensões Recomendadas para Front-end

1. **Prettier - Code Formatter:** Garante formatação consistente e padronizada automática do código (identação, aspas, ponto e vírgula).
2. **ESLint:** Analisador estático que identifica padrões problemáticos e erros de sintaxe em JavaScript/TypeScript.
3. **GitLens:** Enriquece a visualização do Git no editor, exibindo a autoria de cada linha de código (*git blame*), histórico de arquivos e commits.
4. **Live Server:** Inicia um servidor de desenvolvimento local com recarregamento em tempo real (*live reload*) para arquivos HTML/CSS/JS.
5. **Auto Rename Tag / Auto Close Tag:** Automatiza o fechamento e renomeação sincronizada de tags HTML e JSX.

---

# Git: Configuração, Tags e Boas Práticas

## Instalação e Configurações Globais

Após instalar o Git, a primeira etapa obrigatória é configurar a identidade do autor dos commits. Essas informações ficam gravadas permanentemente no histórico:

```bash
# Define o nome global de usuário
git config --global user.name "Seu Nome"

# Define o e-mail global associado à conta do GitHub
git config --global user.email "seu-email@exemplo.com"

# Verifica as configurações aplicadas
git config --list
```

## O que são Tags no Git?

**Tags** são marcadores específicos que apontam para pontos exatos no histórico de commits do repositório. São amplamente utilizadas para sinalizar **lançamentos de versões de software (releases)** de acordo com o padrão SemVer (ex.: `v1.0.0`, `v1.1.0`, `v2.0.0`).

Ao contrário das branches, que se movem a cada novo commit, **tags são estáticas e permanentes**, representando o estado congelado do projeto em uma entrega oficial.

### Tipos de Tags

O Git oferece dois tipos principais de tags:

1. **Tags Leves (Lightweight Tags):**
   - Funcionam apenas como um ponteiro direto (atalho) para um commit específico.
   - Não armazenam informações extras como autor, data ou mensagem de lançamento.
   - Criação:
     ```bash
     git tag v1.0.0
     ```

2. **Tags Anotadas (Annotated Tags) — Recomendado para Releases:**
   - São armazenadas como objetos completos no banco de dados do Git.
   - Contêm a data de criação, o nome e e-mail do autor da tag, uma mensagem explicativa de release e possuem verificação de integridade (checksum).
   - Criação:
     ```bash
     git tag -a v1.0.0 -m "Release da versão 1.0.0 - Lançamento da primeira versão estável"
     ```

### Comandos Essenciais para Gerenciar Tags

| Comando | Descrição |
| --- | --- |
| `git tag` | Lista todas as tags disponíveis no repositório local. |
| `git show v1.0.0` | Exibe os detalhes da tag (autor, data, mensagem) e o commit ao qual está vinculada. |
| `git push origin v1.0.0` | Envia uma tag específica para o repositório remoto (o `git push` padrão não envia tags). |
| `git push origin --tags` | Envia todas as tags locais pendentes de uma só vez para o servidor remoto. |
| `git tag -d v1.0.0` | Deleta uma tag do repositório local. |
| `git push origin --delete v1.0.0` | Remove uma tag do repositório remoto. |

## Boas Práticas no Controle de Versão

- **Commits Atômicos:** Cada commit deve conter apenas uma única mudança lógica ou correção específica. Evite agrupar várias alterações desconexas em um mesmo commit massivo.
- **Mensagens Claras e Semânticas:** Utilize convenções reconhecidas (ex.: [Conventional Commits](https://www.conventionalcommits.org/)) com prefixos padronizados:
  - `feat:` para novas funcionalidades.
  - `fix:` para correções de bugs.
  - `docs:` para alterações em documentação.
  - `refactor:` para refatorações que não alteram o comportamento externo.
  - `chore:` para atualizações de dependências e configurações de build.
- **Uso Estratégico de Branches:** Nunca desenvolva código instável diretamente na branch principal (`main`/`master`). Utilize branches de funcionalidade (`feature/nome-da-feature`) ou correção (`fix/nome-do-bug`).
- **Testes Antes do Merge:** Assegure-se de que a aplicação compila e passa nos testes automatizados antes de mesclar alterações na branch principal.

---

# Node.js e NPM: Ecossistema de Execução

## O que é o Node.js?

O **Node.js** é um ambiente de execução (runtime) JavaScript assíncrono e orientado a eventos, construído sobre o motor V8 da Google (o mesmo utilizado no navegador Google Chrome).

### Importância no Front-end Moderno

Tradicionalmente, o JavaScript só podia ser executado dentro dos navegadores. Com a criação do Node.js:
- O JavaScript passou a ser executado diretamente no sistema operacional do servidor e na máquina do desenvolvedor.
- Unificou a linguagem em toda a stack de desenvolvimento (front-end, back-end e automação de tarefas).
- Viabilizou a criação de ferramentas modernas de compilação, minificação, testes automatizados e servidores de desenvolvimento (Webpack, Vite, Babel, ESLint, Create React App).

## O que é o NPM (Node Package Manager)?

O **NPM** é o gerenciador de pacotes padrão que acompanha o Node.js. Ele é composto por duas partes:
1. **Registro Público (NPM Registry):** O maior catálogo mundial de bibliotecas e módulos de código aberto reutilizáveis.
2. **Interface de Linha de Comando (CLI):** Ferramenta no terminal para instalar, atualizar e gerenciar pacotes locais e globais em projetos.

### Arquivos Principais do Ecossistema

- **`package.json`:** Arquivo manifesto localizado na raiz do projeto. Contém metadados da aplicação (nome, versão, autor, licença), scripts de automação (`start`, `build`, `test`) e a lista declarativa de dependências necessárias.
- **`package-lock.json`:** Gerado automaticamente pelo NPM para registrar com precisão matemática a árvore exata de versões e hashes de cada biblioteca instalada. Garante que qualquer membro da equipe ou servidor de CI/CD reproduza exatamente o mesmo ambiente de dependências.
- **Pasta `node_modules/`:** Diretório onde ficam baixados os arquivos das bibliotecas instaladas. Por ser muito pesado e redundante, deve ser sempre ignorado pelo Git através do `.gitignore`.
