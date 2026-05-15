# Framework de Análise de Editais — Lei 14.133/2021

## Contexto operacional

Este repositório contém um framework multi-agente para análise sistemática de editais de licitação regidos pela Lei n.º 14.133/2021 (Nova Lei de Licitações e Contratos Administrativos), com foco no setor de *resíduos sólidos urbanos (RSU) e limpeza urbana*.

O objetivo é produzir um *relatório exaustivo de vulnerabilidades, riscos e oportunidades* a partir do edital, seus anexos e documentos complementares (Termo de Referência, Estudo Técnico Preliminar, Matriz de Riscos, Minuta de Contrato, Planilhas de Custos, Caderno de Encargos).

## Legislação-base obrigatória

Toda análise deve estar ancorada nos seguintes diplomas (considerar sempre a redação vigente):

|Diploma            |Escopo                                                           |
|-------------------|-----------------------------------------------------------------|
|Lei 14.133/2021    |Licitações e contratos administrativos                           |
|Lei 8.987/1995     |Concessões de serviço público (aplicável quando o edital remeter)|
|Lei 11.079/2004    |PPPs (aplicável quando o edital remeter)                         |
|Lei 12.305/2010    |Política Nacional de Resíduos Sólidos                            |
|Lei 11.445/2007    |Marco Legal do Saneamento Básico                                 |
|Decreto 11.462/2023|Regulamentação da Lei 14.133                                     |
|LC 214/2025        |Reforma Tributária (IBS/CBS sobre serviços públicos)             |
|IN RFB 1.700/2017  |Vida útil de bens para fins fiscais                              |
|Normas do TCU      |Instruções Normativas, Súmulas e jurisprudência                  |
|Normas dos TCEs    |TCE-SP, TCE-MG, TCE-BA, TCM-BA, TCM-SP (conforme jurisdição)     |

## Arquitetura de agentes

O framework opera com *5 agentes especializados*, cada um com escopo delimitado e instruções detalhadas em arquivo próprio na pasta /agentes/.

|#|Agente                                  |Arquivo                       |Escopo                                                                                                                       |
|-|----------------------------------------|------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
|1|Edital e Termo de Referência            |01-edital-tr.md             |Objeto, modalidade, parcelamento, prazos, subcontratação, consórcio, sustentabilidade, ETP, orçamento estimado               |
|2|Habilitação e Qualificação              |02-habilitacao.md           |Jurídica, fiscal/trabalhista, econômico-financeira, técnica (atestados), vedações, consórcio                                 |
|3|Julgamento e Proposta                   |03-julgamento-proposta.md   |Critério de julgamento, modo de disputa, exequibilidade, planilha de custos, BDI, encargos sociais, fase recursal            |
|4|Contrato e Alocação de Riscos           |04-contrato-riscos.md       |Cláusulas obrigatórias, garantias, reajuste/repactuação, matriz de riscos, equilíbrio econômico-financeiro, sanções, extinção|
|5|Vícios, Inconsistências e Direcionamento|05-vicios-inconsistencias.md|Contradições internas, restrição à competitividade, erros materiais, direcionamento, incompatibilidades legais               |

## Regras de execução

### Fluxo obrigatório

1. *Leitura integral* — Ler o edital e TODOS os anexos disponíveis antes de iniciar qualquer análise. Não iniciar análise parcial de um agente sem ter feito a leitura completa do documento.
1. *Execução sequencial por agente* — Executar UM agente por vez, em documento/tarefa separada. Não executar múltiplos agentes simultaneamente (causa timeout por idle da stream).
1. *Varredura exaustiva primeiro, jurisprudência depois* — Cada agente deve primeiro completar a varredura documental (o que o edital diz ou deixa de dizer). A pesquisa jurisprudencial é feita APENAS em fase posterior, somente para os achados selecionados pelo usuário.
1. *Relatório por agente* — Cada agente produz seu relatório independente. A consolidação é feita ao final, pelo usuário.

### Regras invioláveis

- *Não inventar jurisprudência.* Se não tiver certeza de que um acórdão existe, escrever “verificar existência” ou buscar na web. Jamais fabricar número, ementa ou relatoria.
- *Não inferir conteúdo de anexos não fornecidos.* Se o edital remete a um anexo que não está disponível, registrar como lacuna: “Anexo [X] não disponível para análise — verificar conteúdo”.
- *Não classificar teses.* Trazer os achados com seus fundamentos legais. Não rotular como “forte”, “razoável” ou “arriscada”. O usuário decide a classificação.
- *Não editoralizar.* Não adicionar obrigações, boas práticas ou recomendações estratégicas que não estejam no documento. Se a análise sair do texto do edital, sinalizar explicitamente: “⚠️ OBSERVAÇÃO FORA DO DOCUMENTO”.
- *Ancoragem obrigatória.* Toda afirmação deve citar: (i) o artigo/cláusula do edital ou anexo; E (ii) o dispositivo legal correspondente. Sem dupla ancoragem, a afirmação não entra no relatório.
- *Confidencialidade.* Nos outputs, usar termos genéricos (“a licitante”, “o grupo”, “a concessionária”). Não mencionar nomes de empresas, clientes ou detalhes comerciais.
- *Formato de citação.* Legislação: “art. XX, § Y.º, inciso Z, da Lei n.º XXXXX/XXXX”. Jurisprudência TCU: “Acórdão XXXX/XXXX-TCU-Plenário (Rel. Min. [Nome])”.

### Formato do relatório de cada agente


# AGENTE [N] — [NOME DO AGENTE]
## Edital: [identificação do edital]
## Data da análise: [data]

---

### ACHADO [N.1] — [Título descritivo curto]

**Localização no edital:** [Cláusula/item/anexo + página, se disponível]

**Descrição do achado:**
[Descrição objetiva do que o edital prevê ou deixa de prever]

**Fundamento legal:**
[Dispositivo(s) legal(is) que fundamenta(m) a irregularidade, omissão ou risco]

**Impacto:**
[Consequência concreta: nulidade, restrição à competitividade, risco financeiro, risco operacional, etc.]

**Contra-argumento provável da Administração:**
[O que a Administração ou o Tribunal de Contas provavelmente diria em defesa da previsão editalícia]

---

### ACHADO [N.2] — [...]
[...]

---

## LACUNAS DOCUMENTAIS
[Lista de anexos ou informações referenciados no edital mas não disponíveis para análise]

## ALERTAS DE PRAZO
[Prazos relevantes identificados no edital: impugnação, esclarecimento, sessão, recursos]


### Comando de execução

Para executar um agente específico:


Executar Agente [N] para o edital [identificação]. O edital e anexos estão em [caminho/dos/arquivos].


Para executar todos os agentes sequencialmente:


Executar análise completa do edital [identificação]. Agentes 1 a 5, um por vez. Arquivos em [caminho].


## Estrutura de arquivos esperada


/licitacao-14133/
├── CLAUDE.md                          ← Este arquivo (orquestrador)
├── agentes/
│   ├── 01-edital-tr.md               ← Agente 1: Edital e TR
│   ├── 02-habilitacao.md             ← Agente 2: Habilitação
│   ├── 03-julgamento-proposta.md     ← Agente 3: Julgamento e Proposta
│   ├── 04-contrato-riscos.md         ← Agente 4: Contrato e Riscos
│   └── 05-vicios-inconsistencias.md  ← Agente 5: Vícios e Inconsistências
└── editais/                           ← PDFs dos editais e anexos (por licitação)
    └── [pasta-por-edital]/
