# Artigo "DeFiLang: Uma Taxonomia Sociolinguística para Proteção do Consumidor em Finanças Descentralizadas"

Repositório de artefatos, taxonomias, _prompts_ e materiais suplementares do artigo.

## Arquivos do repositório

### Taxonomia (resultado principal)

| Arquivo | Conteúdo |
|---|---|
| [`taxonomy.md`](taxonomy.md) | Versão legível da taxonomia final: meta-característica, tabelas de dimensões por perspectiva e definições completas de cada dimensão e característica, com as regras de aplicação. **Comece por aqui.** |
| [`taxonomy.json`](taxonomy.json) | Versão estruturada (máquina) da taxonomia final. Inclui os dados de entrada (fenômeno, usuários, propósitos, domínio, perspectivas, palavras-chave), a meta-característica, as dimensões e características com origem (empírica/conceitual), marcação de negação e contagem de objetos, as condições objetivas e subjetivas, o plano de avaliação, o resultado da avaliação e o total de tokens. |

### Objetos classificados

| Arquivo | Conteúdo |
|---|---|
| [`objects.json`](objects.json) | Os 60 termos (objetos) com identificador, nome, variantes (*aliases*), descrição, número de menções, iteração de origem, papel (`building` para construção ou `evaluation` para avaliação), **trechos de evidência** com documento de origem e página, e a classificação em cada dimensão (`cells`). Além das características, uma célula pode conter `misfit` (o objeto não cabe em nenhuma característica) ou `no_information` (as fontes não informam a dimensão). |
| [`objects_matrix.csv`](objects_matrix.csv) | Matriz plana objeto × dimensão (60 linhas × 8 colunas: `object_id`, `object`, `role` e uma coluna por dimensão D1–D5). Ideal para análise em planilha, R ou pandas. |

### Processo de desenvolvimento

| Arquivo | Conteúdo |
|---|---|
| [`iterations.json`](iterations.json) | Registro detalhado de cada iteração: tipo (*e*, *c* ou *r*), motivo, consultas, documentos usados, novos objetos, códigos e conceitos, tentativas de proposta e violações de regras, operações aplicadas, verificação das condições objetivas e subjetivas (com justificativas), avaliação, ponto de saída e reentrada no processo, e tokens consumidos. |
| [`operations.json`](operations.json) | Log das 8 operações aplicadas à taxonomia (`add_dimension`, `rename`), com iteração, elementos criados ou alterados, evidências (objetos `O…`, conceitos `K…` ou problemas `I…`) e justificativa. Permite rastrear a origem de cada dimensão e característica. |
| [`audit.json`](audit.json) | Resumo de auditoria por iteração (contagens em vez de listas) e consumo de tokens por etapa do método e por tarefa (extração de objetos, classificação, extração de conceitos, avaliação subjetiva etc.). |
| [`run.log`](run.log) | Log textual da execução com data e hora: etapas percorridas, buscas realizadas (incluindo avisos de limite de requisições HTTP 429), documentos obtidos, propostas e correções, condições verificadas e decisões de saída e reentrada. |

### Fontes

| Arquivo | Conteúdo |
|---|---|
| [`sources.json`](sources.json) | Catálogo de todos os documentos consultados, com identificador, tipo (`scholarly` para artigos acadêmicos, `web` para páginas web e `llm` para definições geradas pelo modelo para os termos), título, URL, DOI, ano, consulta de origem, iteração e status (`processed` quando lido, `no_fulltext` quando o texto integral não estava disponível). |

### Configuração e estado

| Arquivo | Conteúdo |
|---|---|
| [`config.json`](config.json) | Parâmetros da execução: modelo de linguagem, embeddings, provedores de busca acadêmica e web, tamanho de *chunks* de documentos, parâmetros do método (mínimos de dimensões e características, tamanho de lote de classificação, abordagem simbólica e verificação de operações), metas de avaliação e limites (máximo de 15 iterações). O e-mail de contato é um *placeholder* (`you@example.com`). |
| [`state.json`](state.json) | Estado completo e final da execução (*checkpoint*): entrada, meta-característica, taxonomia, todos os objetos, registro de documentos, iterações, log de operações, avaliação, contadores internos e consumo de tokens. Contém em um único arquivo tudo o que está nos demais JSON e serve para retomar ou reproduzir a execução. |

### Exemplos de aplicação

| Arquivo | Conteúdo |
|---|---|
| [`Prompts.txt`](Prompts.txt) | _Prompt_ para Anthropic Claude Opus 5.5 ou outra ferramenta de inteligência artificial generativa visando exemplificar o uso da taxonomia DeFiLang. Anexar arquivos [`taxonomy.json`](taxonomy.json) e [`objects.json`](objects.json). |

---

## Uso rápido

```python
import json
import pandas as pd

# Taxonomia
tax = json.load(open("taxonomy.json", encoding="utf-8"))
for d in tax["dimensions"]:
    print(d["id"], d["name"], [c["name"] for c in d["characteristics"]])

# Matriz de classificação
m = pd.read_csv("objects_matrix.csv")
print(m.groupby("D3 Discourse register").size())
```

---
