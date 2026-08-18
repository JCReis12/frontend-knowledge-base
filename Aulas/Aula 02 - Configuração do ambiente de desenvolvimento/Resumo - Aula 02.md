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
  - Vários desenvolvedores podem trabalhar no mesmo projeto.

- **Menos retrabalho**
  - Conflitos podem ser identificados antes de causarem grandes perdas.

- **Auditoria e rastreabilidade**
  - É possível saber quem alterou determinada parte do projeto, quando e o que foi alterado.

- **Recuperação de versões**
  - Permite retornar para uma versão anterior caso alguma alteração cause problemas.

- **Controle de mudanças**
  - Facilita a integração das alterações feitas pelos membros da equipe.

- **Colaboração**
  - Permite utilizar branches para desenvolver novas funcionalidades sem afetar diretamente a versão principal.

- **Qualidade**
  - Permite testar alterações antes de disponibilizá-las na versão final.

- **Aprimoramento contínuo**
  - O histórico permite acompanhar a evolução do projeto.

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
  - Correção de erros no código.

- **New Feature**
  - Adição de uma nova funcionalidade.

- **Feature Enhancement**
  - Melhoria de uma funcionalidade existente.

- **Refactoring**
  - Reorganização do código para deixá-lo mais limpo e eficiente, sem necessariamente alterar seu comportamento.

- **Performance**
  - Alterações para melhorar velocidade e eficiência.

- **Security Patch**
  - Correção de vulnerabilidades de segurança.

- **Dependency Update**
  - Atualização das bibliotecas e frameworks utilizados.

- **Adding Tests**
  - Adição de testes automatizados para verificar a qualidade do código.

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
