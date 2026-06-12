# Convenções de estilo da doc Credify

Regras extraídas do padrão consolidado em `paths/veiculototal.yaml`. Siga-as
para que endpoints novos pareçam parte do mesmo produto.

## Idioma e tom
- Tudo em **português do Brasil**. Frases diretas, voltadas ao desenvolvedor que
  vai integrar.
- Nome comercial do produto sempre em **negrito** na abertura
  (ex: "A **Consulta Veículo Total** entrega...").
- Nomes técnicos de bases/integrações em `código` e MAIÚSCULAS
  (ex: `VEICULARBNACIONAL`, `PRECIFICADORFIPE`).

## Emojis por integração (reutilize os mesmos para a mesma base)
Mantêm a leitura escaneável e criam memória visual entre endpoints.

| Base | Emoji |
|------|-------|
| VEICULARBNACIONAL (dados fabris) | 🏭 |
| HISTORICOPROPRIETARIO | 👥 |
| VEICULOSBDRP (débitos/restrições) | 📋 |
| PRECIFICADORFIPE | 💰 |
| INDICIOSINISTROVEICULAR | ⚠️ |
| HISTORICOROUBOFURTO | 🚨 |
| LEILAOCONJUGADO | 🏷️ |
| RECALL | 🔔 |

Para bases novas, escolha um emoji semântico e registre-o aqui para reuso.
Nos Tabs de exemplo use ✅ (sucesso) e ❌ (não encontrado).

## Tabelas
- **Requisição:** colunas `Campo | Descrição | Formato | Obrigatório`, com os
  nomes de campo em **negrito**, alinhamento padrão (sem `:---`).
- **Resposta (dentro dos accordions):** colunas `Campo | Descrição | Formato`,
  com alinhamento à esquerda (`|:----------|:--------------|:------------|`).
- Use o **caminho completo** do campo na coluna Campo
  (ex: `VEICULOSBDRP.RETORNO.DEBIPVA`), não só o nome final.
- Registros repetíveis: documente como `REGISTRO_1` quando há um exemplo
  concreto e `REGISTRO_N` quando o bloco é genérico/repetível.

## Accordions
- O primeiro accordion é **sempre** `Cabeçalho da Resposta — CONSULTA`.
- Um accordion por bloco de resposta, na **mesma ordem** da tabela de
  integrações.
- Título do accordion: `<emoji> <Título legível> — <NOMEBASE>`.

## Formatos de dados nos exemplos (realistas, nunca "string")
- **Placa:** `ABC1234` (antiga) ou `ABC1A34` (Mercosul).
- **CPF:** 11 dígitos sem máscara nos exemplos de JSON (`12345678900`).
- **CNPJ:** 14 dígitos (`98765432000110`).
- **Datas:** variam por base — `01/01/2026 10:00:00`, `15/03/2015`, `15-MAR-15`.
  Espelhe o formato que a base realmente retorna; não normalize.
- **Valores monetários:** string no padrão BR `"32.500,00"`.
- **Booleans de débito/restrição:** texto descritivo, não `true/false`
  (ex: `"NAO EXISTE DEBITO DE IPVA"`, `"NADA CONSTA"`).
- **Vetor de status `RESPOSTA.CODIGO`:** array de strings `["1","2",...]`, uma
  posição por integração, na ordem dos accordions.

## Códigos de status (sempre os mesmos três)
`1` = sucesso com dados · `2` = não encontrado · `3` = erro no retorno.

## Coerência requestBody ↔ responses
- O `example` de cada campo do `requestBody` deve casar com o `IDCONSULTA`/dados
  usados nos `examples` da resposta (ex: `IdConsulta: "467"` nos dois lados).
- Os `examples` nomeados em `responses.200` devem refletir exatamente os `<Tab>`
  da seção "Exemplos de Resposta" (um para encontrado, um para não encontrado).

## Tags devem ser ASCII (gotcha real)
A `tag:` do OpenAPI **não pode ter acento ou cedilha**. Se tiver, o Fern pula a
API Reference inteira na publicação (`Skipping API ... non-ASCII characters`).
Use a tag sem acento (ex: `Autenticacao`) e deixe o título bonito com acento no
`section:` do `docs.yml`.

## Erros padrão
Inclua sempre `400` ("Requisição inválida — verifique o body enviado.") e `401`
("Token inválido ou expirado. Renove o token JWT via `/auth`.").
