# Base de Conhecimento

## Dados Utilizados

A SIA utiliza uma base de conhecimento estruturada em arquivos JSON para fornecer respostas sobre educação financeira. Além disso, arquivos CSV são utilizados como dados de exemplo para simular cenários de uso e testes da aplicação.


| Arquivo                      | Formato | Utilização no Agente                                                                                                                           |
| ---------------------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `conceitos_financeiros.json` | JSON    | Base de conceitos de educação financeira, utilizada para responder perguntas sobre orçamento, investimentos, crédito e indicadores econômicos. |
| `perfil_investidor.json`     | JSON    | Contém os perfis de investidor (conservador, moderado e arrojado), utilizados para contextualizar respostas relacionadas a investimentos.      |
| `produtos_financeiros.json`  | JSON    | Armazena informações sobre produtos financeiros, como poupança, CDB, Tesouro Selic, LCI, LCA, ETFs e ações.                                    |
| `perguntas_frequentes.json`  | JSON    | Reúne perguntas frequentes e seus respectivos conceitos relacionados, auxiliando na geração de respostas rápidas e consistentes.               |
| `historico_atendimento.csv`  | CSV     | Utilizado para simular históricos de atendimento e testar interações da assistente.                                                            |
| `transacoes.csv`             | CSV     | Contém exemplos de transações financeiras para demonstração e testes da aplicação.                                                             |

---

## Adaptações nos Dados

Os arquivos originalmente disponibilizados no desafio foram reorganizados para atender ao contexto da SIA. Foi criada uma base de conhecimento própria, composta por arquivos JSON estruturados contendo conceitos financeiros, perfis de investidor, produtos financeiros e perguntas frequentes.

Também foi realizada a organização dos arquivos em diretórios específicos, separando a base de conhecimento dos dados de exemplo utilizados durante os testes da aplicação.

---

## Estratégia de Integração

### Como os dados são carregados?

Os arquivos JSON e CSV são carregados pela aplicação durante sua inicialização. Após a leitura, seus conteúdos permanecem disponíveis em memória para consulta durante toda a sessão, reduzindo a necessidade de múltiplas leituras dos arquivos.

### Como os dados são usados no prompt?

Os dados não são incorporados integralmente ao system prompt. A aplicação identifica a intenção da pergunta do usuário e consulta dinamicamente a base de conhecimento correspondente, utilizando apenas as informações relevantes para construir o contexto enviado ao modelo de linguagem. Essa abordagem reduz o volume de contexto enviado ao LLM e facilita a manutenção e expansão da base de conhecimento.

---

## Exemplo de Contexto Montado


```
Pergunta do usuário:
"Qual a diferença entre renda fixa e renda variável?"

Contexto recuperado:

Conceito: Renda Fixa
- Investimentos cuja remuneração segue regras previamente definidas.
- Menor previsibilidade de risco.

Conceito: Renda Variável
- Investimentos cujo retorno depende das oscilações do mercado.
- Maior potencial de rentabilidade, acompanhado de maior risco.

Conceitos relacionados:
- Liquidez
- Risco
- Perfil do Investidor
```
