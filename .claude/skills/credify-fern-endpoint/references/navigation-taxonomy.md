# Taxonomia de navegação da doc Credify

> **Estrutura viva.** Definida pela liderança como o mapa-alvo da doc. A maioria
> dos endpoints ainda não existe — vão sendo criados aos poucos. Ao criar um
> endpoint novo, encaixe-o na categoria/subcategoria correta abaixo e crie a
> seção no `docs.yml` **só quando ela ganhar o primeiro endpoint** (o Fern
> quebra o build se uma seção apontar para endpoint/página inexistente).
>
> Esta é a **fonte única da verdade** da estrutura. Atualize aqui quando a
> liderança mudar algo.

## Convenções de seção no docs.yml
- Categoria de 1º nível: `section: "N. Nome"` (numerada).
- Subcategoria: `section: "N.M Nome"` aninhada em `contents`.
- Os **nomes dos endpoints** exibidos vêm do `summary` de cada arquivo de path,
  não do docs.yml. Garanta que o `summary` bata com o nome da lista abaixo.
- Tags de OpenAPI devem ser **ASCII** (sem acento/cedilha). O título com acento
  vai no `section:`; a `tag:` vai sem acento (ex: `Autenticacao`).

## Legenda
- ✅ = já implementado  ·  ⬜ = pendente (aguardando código)

## Árvore

### 1. Autenticação e Integração Técnica
- ✅ Auth — `/auth`
- ⬜ SSO
- ⬜ Webhook Decisionfy

### 2. Veículos e Mobilidade
**2.1 Consulta Veicular**
- ✅ Veículo Total — `/veiculototal`
- ✅ Veículos Agregados — `/veiculosagregados`
- ✅ Veículo por Documento — `/veiculodocumento`
- ✅ Veículo Documento Frota — `/veiculodocumentofrota`
- ✅ Veículo Proprietário Placa — `/veiculoproprietarioplaca`
- ✅ Veículo Proprietário Placa Histórico — `/veiculoproprietarioplacahistorico`
- ✅ Histórico de Proprietários — `/historicoproprietario`
- ✅ Histórico Roubo e Furto — `/historicoroubofurto`
- ✅ Débitos, Restrições e Proprietários — `/debitosrestricoesproprietarios`
- ✅ Veicular BNacional Online — `/veicularbnacionalonline`
- ✅ Renavam — `/renavam`
- ✅ Renavam Online — `/renavamonline`

**2.2 Restrições, Gravames e Órgãos Oficiais**
- ⬜ RENAJUD
- ⬜ Renainf
- ⬜ Gravame
- ⬜ ATPVe
- ⬜ ECRLV — Primeira Requisição
- ⬜ ECRLV — Segunda Requisição

**2.3 Risco, Sinistro, Leilão e Precificação**
- ⬜ Indício de Sinistro
- ⬜ Leilão Conjugado
- ⬜ Farol Leilão
- ⬜ Precificador FIPE
- ⬜ Recall

### 3. CNH e Condutores
- ⬜ API Flag CNH
- ⬜ CNH Documento
- ⬜ CNH Chave Dupla
- ⬜ CNH Documento Imagem
- ⬜ CNH Pontuação

### 4. Cadastral Pessoa Física
**4.1 Consulta e Enriquecimento PF**
- ⬜ PF Pesquisa — CPF
- ⬜ PF Nome
- ⬜ PF Telefone — CPF
- ⬜ PF Telefone
- ⬜ PF Email — CPF
- ⬜ PF Email
- ⬜ PF Parentesco

**4.2 Receita Federal e Dados Básicos PF**
- ⬜ PF Receita Federal — CPF
- ⬜ PF Receita Federal x PF Dados Básicos
- ⬜ PF Cadastral Dataset — Dados Básicos

**4.3 Scores, Ocupação e Indicadores PF**
- ⬜ PF Score Força Vínculo
- ⬜ API Ocupação PF
- ⬜ PF API Score Bancos e Financeiras
- ⬜ PF API Renda Presumida Bancos
- ⬜ API Renda Presumida PF Credify

### 5. Cadastral Pessoa Jurídica
**5.1 Consulta e Enriquecimento PJ**
- ⬜ PJ Pesquisa — CNPJ
- ⬜ PJ Razão Social
- ⬜ PJ Telefone — CNPJ
- ⬜ PJ Telefone
- ⬜ PJ Email — CNPJ
- ⬜ PJ Email

**5.2 Receita Federal e Dados Básicos PJ**
- ⬜ PJ Receita Federal — CNPJ
- ⬜ PJ Cadastral Dataset — Dados Básicos

**5.3 Quadro Societário e Beneficiário Final**
- ⬜ PJ API Quadro Societário
- ⬜ PJ Beneficiário Final

**5.4 Indicadores Comerciais e Fiscais PJ**
- ⬜ PJ API Score Bancos e Financeiras
- ⬜ Faturamento Presumido PJ
- ⬜ API Faturamento Presumido PJ Credify
- ⬜ Débitos Estaduais PJ
- ⬜ API Sintegra

### 6. Jurídico, Processos e Restrições
**6.1 Relatório Jurídico**
- ⬜ CPF / CNPJ Totalizador
- ⬜ Nome / Razão Totalizador
- ⬜ Detalhes do Processo — ID do Processo
- ⬜ Detalhes do Processo — Número do Processo

**6.2 Restrições e Apontamentos**
- ⬜ Mandados de Prisão
- ⬜ CCF — Cheques sem Fundos
- ⬜ Crednet Light
- ⬜ API Background Check PF — ver nota de duplicidade
- ⬜ API Background Check PJ — ver nota de duplicidade

### 7. KYC, Compliance e Background Check
**7.1 Produtos KYC**
- ⬜ KYC Compliance Sanções
- ⬜ KYC RH
- ⬜ KYC BET

**7.2 Exposição Pública e Compliance**
- ⬜ Exposição Pública PF
- ⬜ Exposição Pública PJ

**7.3 Background Check**
- ⬜ API Background Check PF
- ⬜ API Background Check PJ

> **Nota de duplicidade (Background Check):** as APIs de Background Check PF/PJ
> aparecem em 6.2 e em 7.3. Se o foco do material for comercial/produto, manter
> **apenas** em 7.3 (KYC/Background Check) e remover de 6.2 para evitar
> duplicidade. Confirmar com a liderança antes de listar nos dois lugares.

### 8. Antifraude, Validações e Autenticação de Dados
**8.1 Validação Cadastral e Vínculo**
- ⬜ Validação Cadastral
- ⬜ Proprietário Telefone Operadora
- ⬜ Validação de Telefone por Documento
- ⬜ Validação de WhatsApp
- ⬜ Autentica Email
- ⬜ Autentica Email IP Endereço
- ⬜ Email History Risk

**8.2 Cartão, BIN e Dados Financeiros**
- ⬜ Autentica Titular Cartão
- ⬜ API Valida BIN

**8.3 Biometria Facial**
- ⬜ Validação Biometria Facial 1x1
- ⬜ Validação Biométrica Facial 1xN
- ⬜ Biometria Facial — Datavalid

**8.4 Documentoscopia**
- ⬜ Documentoscopia Digital
- ⬜ Documentoscopia de Documentos de Identificação

### 9. Marketing, Prospecção e Leads
- ⬜ Gera Leads CEP
- ⬜ Gera Leads UF / Município
- ⬜ Gera Leads Detalhes
- ⬜ Gera Leads Detalhes — Lote
