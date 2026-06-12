---
name: credify-fern-endpoint
description: >-
  Cria ou padroniza um arquivo de endpoint da API Credify em
  fern/openapi/paths/*.yaml no formato visual da documentação Credify (Fern):
  description rica em MDX com tabela de integrações, AccordionGroup por bloco de
  resposta, vetor de status, exemplos em Tabs, mais requestBody e responses
  OpenAPI. Use SEMPRE que o pedido envolver documentar, criar, adicionar,
  revisar ou padronizar um endpoint/consulta da Credify (ex: "documenta o
  /renavam", "cria a página do endpoint de score", "deixa o veiculodocumento no
  mesmo padrão do veiculototal", "adiciona um endpoint novo na doc"), mesmo que
  a palavra "Fern" não seja dita. Também aplica quando se pede para alinhar um
  arquivo de path ao padrão da casa.
---

# Documentar um endpoint da API Credify (Fern)

Esta skill produz arquivos de endpoint **consistentes com o restante da doc da
Credify**. O arquivo de referência canônico do padrão é
`fern/openapi/paths/veiculototal.yaml` — quando em dúvida sobre estilo, abra-o e
espelhe as decisões dele.

## Por que o padrão importa

O cliente da API lê dezenas de endpoints. Se cada um tiver uma estrutura
diferente, ele perde tempo se reorientando a cada página. O padrão Credify
resolve isso: o leitor sempre encontra a explicação do produto no topo, as
tabelas de campos dentro de accordions (para não poluir), o significado dos
códigos de status, e exemplos reais de JSON. Mantenha essa previsibilidade.

## Fluxo de trabalho

1. **Reúna o material de origem.** Você precisa de: caminho/método
   (`POST /endpoint`), nome comercial do produto, o que ele entrega, os campos
   de **requisição**, e o **JSON de resposta** real (de sucesso e de "não
   encontrado"). Se algo faltar, pergunte ao usuário em vez de inventar campos —
   campo errado na doc gera ticket de suporte.
2. **Decida o tipo de produto:**
   - **Produto de integração única** (ex: `/renavam`): pula a tabela "Integrações
     que compõem este produto" e os blocos `###` por integração. Vai direto para
     a tabela de requisição + accordions de resposta.
   - **Produto consolidado/multi-integração** (ex: `/veiculototal`): inclui a
     tabela de integrações e um bloco `###` por integração explicando o que cada
     base entrega.
3. **Leia `references/endpoint-template.yaml`** e use-o como esqueleto.
4. **Leia `references/credify-conventions.md`** para regras de estilo (emojis,
   nomes de campos, capitalização, formato de placa/CPF, etc.).
5. **Escreva o arquivo** em `fern/openapi/paths/<nome>.yaml`.
6. **Registre na navegação:** confirme que `POST /<nome>` está listado no
   `fern/docs.yml` dentro da seção correta. Para saber **em qual
   categoria/subcategoria** o endpoint se encaixa, consulte
   `references/navigation-taxonomy.md` (fonte única da verdade da estrutura).
   Crie a seção no `docs.yml` apenas quando ela ganhar o primeiro endpoint — o
   Fern quebra o build se uma seção apontar para algo inexistente. A ordem do
   `layout` é a ordem que o cliente vê.
7. **Valide o build:** rode `fern check` (e `fern docs dev` para preview visual)
   antes de considerar pronto. Reporte erros de schema/links quebrados.

## Anatomia do arquivo

Todo arquivo de path segue esta ordem de cima para baixo:

```
post:
  operationId: <camelCaseDescritivo>      # ex: consultarRenavam
  tags: [<Tag ASCII>]                      # ex: Consulta Veicular — SEM acento/cedilha
  summary: <Nome comercial curto>          # ex: Veículo Total
  description: |                           # bloco MDX — ver estrutura abaixo
    ...
  requestBody: ...                         # objeto Consulta
  responses: ...                           # 200 (com examples) + 400 + 401
```

### Estrutura do `description` (MDX) — siga nesta ordem

1. **Parágrafo de abertura** com o **nome do produto em negrito** e uma frase do
   que ele faz. Para produtos consolidados, diga quantas integrações reúne.
2. **`<Note>`** com os casos de uso indicados (vistoria, financiamento, seguro…).
3. *(só multi-integração)* **`## Integrações que compõem este produto`** — tabela
   `| Integração | O que entrega |` com uma linha por base, usando o nome técnico
   da base em `código`.
4. *(só multi-integração)* Um bloco **`### <emoji> <Título> — <NOMEBASE>`** por
   integração, com bullets do que aquela base traz.
5. **`## TABELA DE CAMPOS DE REQUISIÇÃO`** — tabela com colunas
   `Campo | Descrição | Formato | Obrigatório`.
6. **`<AccordionGroup>`** com um **`<Accordion title="...">`** por bloco de
   resposta. O primeiro é sempre o **"Cabeçalho da Resposta — CONSULTA"**; os
   seguintes, um por integração/bloco. Cada accordion contém uma tabela
   `Campo | Descrição | Formato`. Use o caminho completo do campo
   (ex: `VEICULARBNACIONAL.REGISTRO_1.CHASSI`).
7. **`## Lógica de Resposta (Vetor de Status)`** com um **`<Tip>`** explicando o
   array `RESPOSTA.CODIGO` e uma tabela traduzindo `1`/`2`/`3`.
8. **`## Exemplos de Resposta`** com **`<Tabs>`** contendo pelo menos
   `<Tab title="✅ ...Encontrado">` e `<Tab title="❌ Não Encontrado">`, cada um
   com um bloco ```json``` realista.

### `requestBody`

Sempre envelopado em um objeto raiz `Consulta` com `required`. Inclua
`description` e `example` em cada propriedade — o `example` alimenta o API
Explorer e os exemplos gerados por IA.

### `responses`

- `'200'`: `description` explicando os códigos, `schema` via `$ref` para
  `../openapi.yaml#/components/schemas/<SchemaDaResposta>`, e `examples` nomeados
  (`Veiculo Encontrado`, `Veiculo Nao Encontrado`) refletindo os Tabs.
- `'400'`: "Requisição inválida — verifique o body enviado."
- `'401'`: "Token inválido ou expirado. Renove o token JWT via `/auth`."

Se o schema da resposta ainda não existir em `fern/openapi/openapi.yaml`,
avise o usuário e ofereça criá-lo lá em `components/schemas`.

## Lembrete final

Antes de finalizar, releia o arquivo lado a lado com `veiculototal.yaml`: os
títulos de seção, os emojis e a ordem devem bater. Consistência é o produto.
