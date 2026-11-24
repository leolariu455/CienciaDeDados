# 📊 Consumo Digital na Europa: Tendências, Desigualdades e Oportunidades para o Marketing Digital

> **Objetivo geral:** Analisar a evolução das compras online em países europeus entre 2020 e 2025, investigando diferenças geográficas e demográficas no comportamento dos consumidores, a fim de identificar oportunidades para estratégias de Marketing Digital mais eficazes e inclusivas.

---

## 📌 Visão Geral do Projeto

O comércio eletrônico tem transformado os hábitos de consumo e ampliado as possibilidades de atuação das empresas no ambiente digital. Entretanto, a participação nas compras online não ocorre necessariamente da mesma maneira entre países e grupos de consumidores.

Este projeto utiliza dados públicos do **Eurostat**, referentes ao período de **2020 a 2025**, para investigar tendências de consumo digital em países europeus.

A análise busca compreender como a participação nas compras online evoluiu ao longo do tempo, identificar diferenças entre países e faixas etárias e examinar a frequência das compras realizadas pela internet.

O projeto foi desenvolvido em Python, no Google Colab, utilizando a metodologia **CRISP-DM (Cross-Industry Standard Process for Data Mining)**.

Além da análise estatística, são discutidas possíveis aplicações dos resultados em estratégias de Marketing Digital, incluindo oportunidades de segmentação, relacionamento com consumidores e inclusão digital.

### Perguntas de investigação

1. Como a participação nas compras online evoluiu entre 2020 e 2025?
2. Quais países apresentaram maiores e menores variações nesse período?
3. Como o comportamento de compra online varia entre diferentes faixas etárias?
4. Como se distribui a frequência de compras entre os consumidores digitais?
5. De que maneira os resultados podem contribuir para estratégias de Marketing Digital mais eficazes e inclusivas?

### Tecnologias utilizadas

- **Python:** linguagem utilizada para o tratamento e a análise dos dados.
- **Pandas:** manipulação, limpeza, organização e agregação dos dados.
- **Matplotlib:** construção de gráficos e visualizações.
- **Scikit-learn:** implementação e avaliação do modelo de regressão linear.
- **Google Colab:** ambiente de desenvolvimento e execução do projeto.
- **GitHub:** documentação e apresentação do projeto.

---

# 🛠️ Desenvolvimento do Projeto — Metodologia CRISP-DM

## 1. Entendimento do Negócio (Business Understanding)

### Problema de negócio

O crescimento do comércio eletrônico amplia as oportunidades para empresas que desejam alcançar consumidores por meio de canais digitais.

Entretanto, os hábitos de compra online variam entre países e grupos demográficos. Essas diferenças podem influenciar a escolha dos públicos, dos canais de comunicação e das estratégias de relacionamento utilizadas pelas organizações.

Para o Marketing Digital, compreender tais diferenças é importante para evitar estratégias excessivamente generalizadas e identificar oportunidades de atuação em mercados e segmentos específicos.

### Objetivo do projeto

Investigar a evolução e as diferenças no comportamento de compra online em países europeus, utilizando dados estatísticos para apoiar decisões de segmentação e planejamento de Marketing Digital.

### Objetivos específicos

- Analisar a evolução das compras online entre 2020 e 2025.
- Comparar o crescimento da participação nas compras online entre países.
- Identificar diferenças de participação entre faixas etárias.
- Investigar a frequência de compras entre consumidores digitais.
- Aplicar um modelo estatístico para representar a tendência temporal observada.
- Discutir oportunidades de Marketing Digital e possíveis contribuições para a inclusão digital.

### Solução proposta

Utilizar dados públicos do Eurostat, técnicas de análise exploratória, estatística descritiva, visualização de dados e regressão linear simples.

Os resultados serão interpretados sob a perspectiva do Marketing Digital, considerando tanto oportunidades de negócio quanto limitações dos dados e possíveis impactos sociais.

---

## 2. Entendimento dos Dados (Data Understanding)

### Fonte dos dados

Os dados foram obtidos no **Eurostat**, órgão responsável pela divulgação de estatísticas oficiais da União Europeia.

**Dataset:** `isoc_ec_ib20`

**Arquivo utilizado:** `isoc_ec_ib20_linear.csv.gz`

**Período analisado:** 2020 a 2025.

**Fonte:** [Eurostat — Base de dados estatísticos](https://ec.europa.eu/eurostat/data/database)

### Características do conjunto de dados

O arquivo original apresenta:

| Característica | Quantidade |
|---|---:|
| Registros | 558.750 |
| Colunas | 11 |
| Referências geográficas | 40 |
| Indicadores de comportamento digital | 13 |
| Categorias demográficas | 147 |
| Período | 2020–2025 |

As referências geográficas incluem países e agregados regionais.

O conjunto de dados contém **percentuais estatísticos agregados**, e não registros individuais de compras ou transações financeiras.

### Principais variáveis

| Variável | Descrição |
|---|---|
| `geo` | País ou agregado geográfico |
| `TIME_PERIOD` | Ano da observação |
| `ind_type` | Grupo populacional ou demográfico |
| `indic_is` | Indicador relacionado ao comportamento de compra online |
| `unit` | Unidade de medida e população utilizada como referência |
| `OBS_VALUE` | Valor percentual observado |
| `OBS_FLAG` | Informação complementar sobre a qualidade da observação |

### Análise exploratória inicial

Durante a exploração dos dados, foram investigados:

- Estrutura e tipos das variáveis.
- Valores ausentes.
- Existência de registros duplicados.
- Distribuição das informações por país e ano.
- Indicadores disponíveis.
- Categorias demográficas.
- Diferenças entre unidades de medida.

Foram identificados **27.912 registros sem valor em `OBS_VALUE`**, correspondentes a aproximadamente 5% do conjunto original.

Também foi constatado que alguns indicadores apresentam diferentes unidades de medida, exigindo atenção à população utilizada como denominador em cada percentual.

---

## 3. Preparação dos Dados (Data Preparation)

A preparação dos dados teve como objetivo organizar as informações e garantir maior consistência nas comparações.

### Limpeza e tratamento

Foram realizados os seguintes procedimentos:

1. Remoção da coluna `CONF_STATUS`, que não apresentava informações.
2. Exclusão de 27.912 registros sem valor na variável `OBS_VALUE`.
3. Verificação de duplicatas, sem identificação de registros duplicados na base tratada.
4. Preservação da coluna `OBS_FLAG`, que contém informações relacionadas à qualidade dos dados.
5. Remoção das colunas técnicas `DATAFLOW`, `LAST UPDATE` e `freq`, por apresentarem valores constantes.
6. Seleção de indicadores e unidades de medida compatíveis com cada análise.
7. Identificação das localidades com informações disponíveis durante todo o período de 2020 a 2025.
8. Separação dos países individuais dos agregados regionais da União Europeia e da zona do euro.

### Bases utilizadas

| Base | Registros | Finalidade |
|---|---:|---|
| `df` | 558.750 | Conjunto original |
| `df_tratado` | 530.838 | Base limpa para diferentes análises |
| `df_analise` | 221 | Indicador geral de compras online |
| `df_temporal` | 198 | Localidades com cobertura temporal completa |
| `df_paises` | 186 | Comparação de 31 países entre 2020 e 2025 |

As bases `df_idades` e `df_frequencia` também foram criadas para investigar grupos etários e frequência de compras.

### Critérios de seleção

Para a análise temporal e a comparação entre países, foi utilizado o indicador:

**Last online purchase: in the last 3 months**

A unidade selecionada foi:

**Percentage of individuals**

Esse recorte representa o percentual de indivíduos cuja última compra online ocorreu nos três meses anteriores.

Para a análise da frequência de compras, foi utilizada outra unidade:

**Percentage of individuals who purchased online in the last 3 months**

Essa distinção é necessária porque os indicadores possuem populações de referência diferentes.

A seleção dos 31 países com dados completos permitiu acompanhar o mesmo conjunto de localidades ao longo dos seis anos.

---

## 4. Modelagem (Modeling)

### Técnica utilizada

Foi aplicada uma **regressão linear simples**, utilizando a biblioteca Scikit-learn.

O objetivo foi representar estatisticamente a tendência temporal da média de participação nas compras online entre os 31 países analisados.

### Variáveis do modelo

- **Variável independente (X):** ano, de 2020 a 2025.
- **Variável dependente (y):** média anual dos percentuais de participação nas compras online.

A média foi calculada atribuindo o mesmo peso a cada país, independentemente de sua população.

### Resultados da modelagem

| Indicador | Resultado |
|---|---:|
| Variação anual estimada | +2,17 pontos percentuais |
| Coeficiente de determinação (R²) | 0,9251 |

O coeficiente da regressão indica uma tendência linear positiva de aproximadamente **2,17 pontos percentuais por ano**.

O R² de **0,9251** indica que a reta ajustada representa aproximadamente **92,51% da variação observada nas seis médias anuais**.

### Limitações da modelagem

O modelo foi ajustado com apenas seis observações anuais agregadas.

Embora apresente bom ajuste aos valores históricos, não considera diferenças individuais entre países, características demográficas ou fatores externos que possam influenciar as compras online.

Por isso, a regressão foi utilizada como ferramenta **exploratória e descritiva**, sem finalidade de previsão precisa ou identificação de relações causais.

---

## 5. Avaliação (Evaluation)

A avaliação considerou o ajuste estatístico do modelo e sua utilidade para os objetivos do projeto.

### Métrica utilizada

Foi calculado o **Erro Absoluto Médio (MAE)**, por meio da biblioteca Scikit-learn.

| Métrica | Resultado |
|---|---:|
| R² | 0,9251 |
| MAE | 0,76 ponto percentual |

O MAE de **0,76 ponto percentual** indica que a diferença absoluta média entre os valores observados e os estimados foi relativamente pequena.

Entretanto, a avaliação foi realizada com os mesmos seis valores utilizados no ajuste da regressão.

Portanto, o resultado representa o **erro de ajuste histórico**, não uma avaliação independente da capacidade preditiva do modelo.

### Avaliação em relação ao objetivo de negócio

A regressão contribuiu para representar a tendência geral de crescimento das compras online.

Contudo, as análises por país, faixa etária e frequência de compra são fundamentais para interpretar diferenças entre mercados e consumidores.

Assim, o modelo estatístico complementa a análise exploratória, mas não substitui a investigação dos diferentes segmentos.

---

## 📈 Principais Resultados das Análises

### 1. Evolução temporal das compras online

A média dos percentuais de participação nas compras online entre os 31 países apresentou os seguintes resultados:

| Ano | Média entre países |
|---|---:|
| 2020 | 47,73% |
| 2021 | 53,18% |
| 2022 | 52,37% |
| 2023 | 55,23% |
| 2024 | 57,73% |
| 2025 | 59,62% |

Entre 2020 e 2025, foi observado um aumento de **11,89 pontos percentuais**.

Apesar de uma pequena redução entre 2021 e 2022, a tendência geral do período foi de crescimento.

Esses valores representam médias simples dos percentuais dos países, e não uma taxa populacional ponderada para toda a Europa.

### 2. Comparação entre países

A análise identificou diferenças importantes na evolução das compras online entre 2020 e 2025.

**Maiores crescimentos observados:**

| País | Variação |
|---|---:|
| Chipre | +27,10 pp |
| Grécia | +24,57 pp |
| Irlanda | +23,42 pp |
| Sérvia | +21,51 pp |
| Romênia | +19,42 pp |

**Menores variações observadas:**

| País | Variação |
|---|---:|
| Alemanha | −4,62 pp |
| Luxemburgo | +0,17 pp |
| Eslovênia | +1,60 pp |
| Bélgica | +2,01 pp |
| Dinamarca | +2,57 pp |

Os resultados demonstram que o crescimento das compras online não ocorreu de maneira uniforme.

É importante destacar que países com menor crescimento podem apresentar níveis elevados de participação desde o início do período.

Por exemplo, a Dinamarca já apresentava 79,36% em 2020, alcançando 81,93% em 2025.

Dessa forma, o nível de participação e a velocidade de crescimento devem ser considerados separadamente.

### 3. Diferenças entre faixas etárias

A análise de 2025 considerou seis faixas etárias, com dados disponíveis para os 31 países.

| Faixa etária | Média de participação |
|---|---:|
| 16–24 anos | 70,08% |
| 25–34 anos | 75,87% |
| 35–44 anos | 72,17% |
| 45–54 anos | 62,37% |
| 55–64 anos | 46,30% |
| 65–74 anos | 30,03% |

A maior média foi observada entre indivíduos de **25 a 34 anos**, enquanto a menor ocorreu no grupo de **65 a 74 anos**.

A diferença entre esses grupos foi de **45,84 pontos percentuais**.

Esse resultado evidencia diferenças relevantes na participação nas compras online conforme a idade.

Entretanto, os dados não permitem determinar isoladamente as causas dessas diferenças.

### 4. Frequência de compras online

A análise da frequência considerou consumidores que realizaram compras pela internet nos últimos três meses, em 2025.

| Frequência de compra | Média entre países |
|---|---:|
| 1 ou 2 compras | 32,88% |
| 3 a 5 compras | 34,54% |
| 6 compras ou mais | 32,43% |

A distribuição apresentou relativa proximidade entre as três categorias.

O grupo de **3 a 5 compras** apresentou a maior média, com 34,54%, mas sem uma diferença expressiva em relação aos demais.

Esses resultados indicam diferentes intensidades de compra entre os consumidores digitais.

---

## 💼 Recomendações para o Marketing Digital

As análises realizadas permitem propor algumas orientações para estratégias de Marketing Digital.

### Segmentação por mercado

Os países apresentam diferentes níveis de participação e ritmos de crescimento das compras online.

Assim, estratégias de Marketing podem considerar tanto mercados com participação elevada quanto aqueles em que o comércio eletrônico ainda apresenta menor alcance.

A escolha de campanhas, canais e investimentos deve ser complementada por informações específicas sobre cada mercado.

### Segmentação por faixa etária

As diferenças observadas entre os grupos etários sugerem a importância de adaptar a comunicação aos diferentes perfis de consumidores.

Ações de Marketing podem considerar preferências de canais, clareza das informações, facilidade de navegação e necessidades específicas dos públicos.

Entretanto, essas características precisam ser investigadas diretamente, pois os dados analisados não identificam as causas da menor participação de determinados grupos.

### Relacionamento e fidelização

A distribuição da frequência de compras indica a presença de consumidores com diferentes níveis de atividade no comércio eletrônico.

Essa informação pode orientar propostas de relacionamento e fidelização, desde que as empresas utilizem dados próprios para identificar o comportamento de seus clientes.

O conjunto de dados do Eurostat não permite identificar consumidores individualmente nem medir o desempenho de campanhas específicas.

---

## 🌍 Impacto Social e Inovação na Estratégia de Marketing Digital

### 1. Necessidade social e relação com o negócio

O crescimento do comércio eletrônico amplia as oportunidades de consumo e de relacionamento entre empresas e consumidores. Entretanto, a participação no ambiente digital não ocorre de maneira uniforme entre diferentes grupos populacionais.

Na análise dos dados do Eurostat referentes a 2025, a média de participação nas compras online foi de **75,87% entre pessoas de 25 a 34 anos**, enquanto o grupo de **65 a 74 anos apresentou 30,03%**.

A diferença de **45,84 pontos percentuais** evidencia uma desigualdade de participação entre esses grupos nos 31 países analisados.

Embora os dados não permitam identificar diretamente as causas dessa diferença, os resultados justificam investigar possíveis barreiras relacionadas à compreensão das informações, à acessibilidade e à experiência de compra.

**Objetivo de negócio:** melhorar a experiência dos consumidores nos canais digitais e reduzir possíveis dificuldades durante o processo de compra.

**Objetivo social:** contribuir para uma participação digital mais inclusiva, favorecendo a autonomia dos consumidores no acesso às informações e na realização de compras online.

### 2. Públicos afetados, benefícios e riscos

A proposta considera dois públicos principais:

| Público | Benefício esperado | Risco identificado | Medida de mitigação |
|---|---|---|---|
| Pessoas de 65 a 74 anos | Maior autonomia e facilidade na utilização dos canais digitais | Estereótipos relacionados à idade e à capacidade tecnológica | Investigar necessidades reais e oferecer recursos acessíveis sem discriminação |
| Pessoas de 25 a 34 anos | Maior clareza das informações e facilidade de navegação | Generalização do comportamento e exclusão de necessidades individuais | Realizar testes com diferentes perfis de consumidores |

A iniciativa também poderá beneficiar pessoas de outras faixas etárias que encontrem dificuldades na utilização de plataformas digitais.

Durante eventuais pesquisas, deverão ser respeitados os princípios de privacidade, participação voluntária, consentimento informado e minimização da coleta de dados pessoais.

### 3. Dados e evidências

- **Fonte:** Eurostat, conjunto de dados `isoc_ec_ib20`.
- **Período geral da pesquisa:** 2020 a 2025.
- **Período da comparação etária:** 2025.
- **Cobertura geográfica:** 31 países europeus.
- **Público analisado na comparação etária:** indivíduos de 16 a 74 anos, distribuídos em seis faixas etárias.
- **Indicador:** percentual de indivíduos cuja última compra online ocorreu nos três meses anteriores.

Os resultados representam médias simples dos percentuais dos países analisados, sem ponderação pelo tamanho de suas populações.

Entre as limitações e possíveis fontes de viés, destacam-se:

- Diferenças na disponibilidade e na qualidade dos dados entre países.
- Exclusão de localidades com cobertura temporal incompleta.
- Ausência de informações individuais sobre os consumidores.
- Impossibilidade de identificar diretamente as causas das diferenças observadas.
- Ausência de análise específica de sensibilidade às marcações de qualidade do Eurostat.
- Ausência de pessoas com 75 anos ou mais no recorte etário selecionado.

**Resultado observado:** diferença de 45,84 pontos percentuais na participação média nas compras online entre os grupos de 25 a 34 anos e de 65 a 74 anos.

**Resultado esperado:** melhoria da compreensão das informações, da experiência de navegação e da autonomia dos consumidores após uma eventual intervenção.

Os benefícios esperados ainda não foram comprovados e deverão ser avaliados por meio de testes específicos.

### 4. Impacto social nas etapas do CRISP-DM

| Etapa | Questão social considerada | Evidência ou decisão do projeto | Risco ou limitação |
|---|---|---|---|
| Compreensão do negócio | Como conciliar oportunidades comerciais e inclusão digital? | Investigar diferenças no consumo digital e propor estratégias de Marketing mais inclusivas | Priorizar exclusivamente os públicos com maior participação digital |
| Compreensão dos dados | Os dados representam adequadamente os diferentes públicos? | Utilização de dados públicos e agregados do Eurostat, com análise de cobertura geográfica e demográfica | Ausências, diferenças de qualidade e limitações de representatividade |
| Preparação dos dados | Como preservar a qualidade das informações e evitar exclusões indevidas? | Investigação dos valores ausentes, preservação das marcações de qualidade e seleção de países com cobertura temporal completa | Exclusão de localidades e perda de representatividade de determinados públicos |
| Modelagem e análise | Como o comportamento de compra varia entre diferentes grupos? | Comparação entre países, faixas etárias e frequências de compra, complementada por regressão linear simples | Generalizações, estereótipos e interpretações causais indevidas |
| Avaliação | Os resultados podem orientar benefícios sociais e comerciais? | Identificação da diferença de participação entre faixas etárias e proposição de indicadores para avaliar uma futura intervenção | Confundir resultados estatísticos com benefícios sociais efetivamente alcançados |
| Implantação | Como implementar, acompanhar e corrigir a estratégia? | Documentação dos resultados e proposta de comunicação digital acessível, com metas, responsáveis e acompanhamento | Ausência de monitoramento, escuta dos consumidores ou avaliação dos resultados |

### 5. Proposta de inovação social

**Nome da iniciativa: Comunicação Digital Acessível para Compras Online**

Propõe-se desenvolver um projeto-piloto de melhoria da comunicação digital em uma empresa de comércio eletrônico, utilizando os resultados da pesquisa como fundamentação inicial.

A iniciativa contempla:

- Revisão de textos para utilizar linguagem clara e objetiva.
- Orientações passo a passo sobre como realizar compras.
- Informações visíveis sobre pagamento, entrega, trocas e devoluções.
- Melhoria da legibilidade e da organização visual das páginas.
- Testes de compreensão e navegação com consumidores de diferentes faixas etárias.
- Disponibilização de canais de atendimento acessíveis.
- Criação de um canal de escuta para identificar dificuldades e sugestões dos consumidores.

**Público prioritário:** pessoas de 65 a 74 anos, sem restringir os benefícios aos demais grupos etários.

**Público de comparação:** pessoas de 25 a 34 anos.

**Canais:** site de comércio eletrônico, páginas de produtos, e-mail e conteúdos informativos em redes sociais.

**Recursos necessários:** equipe de Marketing, profissionais de experiência do usuário (UX), ferramentas de pesquisa, revisão de conteúdo e participantes voluntários.

**Responsáveis propostos:** equipe de Marketing, equipe de experiência do usuário e responsável pela proteção de dados.

#### Cronograma proposto

| Período | Atividade | Responsável |
|---|---|---|
| Semana 1 | Diagnóstico inicial e levantamento dos indicadores de referência | Marketing e UX |
| Semanas 2 e 3 | Revisão dos conteúdos e desenvolvimento das melhorias | Marketing e UX |
| Semana 4 | Testes de compreensão e navegação com os consumidores | UX e pesquisa |
| Semana 5 | Avaliação dos resultados e identificação de dificuldades | Marketing e UX |
| Semana 6 | Ajustes finais e decisão sobre a ampliação da iniciativa | Coordenação de Marketing |
| Após o projeto-piloto | Monitoramento mensal e revisão periódica | Marketing e UX |

A iniciativa possui prazo inicial proposto de seis semanas e constitui um planejamento acadêmico, não uma campanha já executada.

### 6. Indicadores e validação

Para avaliar os possíveis benefícios sociais e comerciais da iniciativa, são propostos quatro indicadores de acompanhamento.

| Indicador | O que será medido | Como será calculado | Linha de base e meta | Fonte e periodicidade | Responsável |
|---|---|---|---|---|---|
| Conformidade dos conteúdos com critérios de acessibilidade | Adequação dos conteúdos selecionados aos critérios definidos | Conteúdos aprovados no checklist ÷ total de conteúdos avaliados × 100 | Linha de base a medir; meta de 100% dos conteúdos selecionados | Checklist de avaliação; antes e depois da revisão e mensalmente | Marketing e UX |
| Acesso às informações de compra | Capacidade de localizar informações sobre pagamento, entrega e devolução sem ajuda | Participantes que localizarem corretamente as informações ÷ total de participantes × 100 | Linha de base a medir; aumento proposto de 10 pontos percentuais, limitado a 100% | Testes de navegação; antes e depois da intervenção e mensalmente | UX |
| Compreensão das informações de compra | Capacidade de compreender as condições de compra | Participantes que responderem corretamente às perguntas definidas ÷ total de participantes × 100 | Linha de base a medir; aumento proposto de 10 pontos percentuais, limitado a 100% | Questionários padronizados; antes e depois da intervenção e mensalmente | Marketing e pesquisa |
| Conclusão de compra simulada sem ajuda | Autonomia dos consumidores na realização de uma tarefa de compra | Participantes que concluírem a tarefa sem ajuda ÷ total de participantes × 100 | Linha de base a medir; aumento proposto de 10 pontos percentuais, limitado a 100% | Testes de usabilidade; antes e depois da intervenção e mensalmente | UX |

As metas apresentadas são propostas iniciais de planejamento e poderão ser revisadas após a medição da linha de base.

#### Planejamento da avaliação

Inicialmente, deverão ser realizados testes com a versão original das páginas e dos conteúdos digitais.

Após a implementação das melhorias, deverão ser realizados novos testes, utilizando tarefas equivalentes e grupos comparáveis.

Os resultados deverão ser analisados separadamente por faixa etária, considerando o número de participantes, as condições dos testes e as limitações da avaliação.

Sempre que possível, a ordem de apresentação das versões deverá ser alternada entre os participantes para reduzir possíveis efeitos de aprendizagem.

As compras utilizadas nos testes serão simuladas, sem necessidade de fornecer informações financeiras reais.

A avaliação buscará verificar se a intervenção contribuiu para melhorar a experiência e a autonomia dos consumidores, além de identificar possíveis benefícios para os objetivos de Marketing Digital.

### 7. Limites e acompanhamento

Os dados do Eurostat permitem identificar diferenças de participação nas compras online, mas não comprovam que essas diferenças sejam causadas por barreiras de acessibilidade ou dificuldades de utilização dos canais digitais.

Por esse motivo, a proposta deverá ser validada antes de sua ampliação.

Serão adotados os seguintes critérios de decisão:

- **Aprovar:** quando as metas forem alcançadas, sem agravamento das diferenças entre os grupos avaliados ou identificação de riscos relevantes.
- **Ajustar:** quando os indicadores permanecerem abaixo das metas, surgirem dificuldades recorrentes ou aumentarem as diferenças de desempenho entre os públicos.
- **Suspender temporariamente:** quando forem identificados problemas graves de acessibilidade, discriminação ou violação da privacidade dos participantes.

Também deverá ser disponibilizado um canal de escuta, por meio de formulário acessível ou e-mail de atendimento, permitindo que os consumidores relatem dificuldades e apresentem sugestões.

As manifestações deverão ser avaliadas semanalmente durante o projeto-piloto, com acompanhamento mensal dos indicadores após sua eventual implantação.

Dessa forma, a proposta busca conciliar os objetivos de Marketing Digital com a inclusão, a autonomia e a melhoria da experiência dos consumidores.

**Situação atual:** a iniciativa ainda não foi implementada. Os indicadores, as metas e o cronograma representam um planejamento para futura validação, não resultados efetivamente alcançados.

---
### Forma de apresentação

O projeto utiliza:

- Notebook no Google Colab com os códigos de preparação, análise e modelagem.
- Tabelas com os principais resultados.
- Gráficos de evolução temporal, comparação entre países, faixas etárias e frequência de compras.
- Visualização da regressão linear.
- Documentação do projeto no GitHub.

### Aplicação dos resultados

As análises podem contribuir para:

- Identificar diferenças de participação no comércio eletrônico entre países.
- Apoiar decisões iniciais de segmentação de mercado.
- Investigar necessidades de comunicação de diferentes faixas etárias.
- Orientar propostas de relacionamento com consumidores.
- Fundamentar iniciativas de comunicação digital mais inclusiva.

**Não foi realizado o desenvolvimento de um sistema de previsão em produção, painel automatizado ou campanha real de Marketing.**

A implantação, neste projeto acadêmico, corresponde à documentação e à apresentação dos resultados e recomendações.

---

## 📝 Considerações Finais

O projeto analisou o comportamento de compra online em países europeus entre 2020 e 2025, utilizando dados públicos do Eurostat e a metodologia CRISP-DM.

Os resultados demonstraram uma tendência geral de crescimento na média de participação nas compras online dos 31 países selecionados, passando de 47,73% em 2020 para 59,62% em 2025.

Entretanto, a comparação entre países revelou diferenças importantes nos ritmos de crescimento. Chipre, Grécia e Irlanda apresentaram avanços expressivos, enquanto a Alemanha registrou redução entre os dois anos analisados.

A análise demográfica também identificou diferenças relevantes entre faixas etárias, especialmente entre os grupos de 25 a 34 anos e de 65 a 74 anos.

A investigação da frequência de compras mostrou uma distribuição relativamente equilibrada entre consumidores com diferentes intensidades de compra.

Na etapa de modelagem, a regressão linear apresentou tendência estimada de crescimento de 2,17 pontos percentuais por ano, com R² de 0,9251 e MAE de 0,76 ponto percentual. Esses resultados indicam bom ajuste histórico, mas não garantem desempenho preditivo futuro.

Sob a perspectiva do Marketing Digital, as descobertas reforçam a importância de considerar diferenças geográficas e demográficas no planejamento de estratégias, evitando abordagens excessivamente generalizadas.

Na dimensão social, a menor participação média nas compras online entre pessoas de 65 a 74 anos motivou uma proposta de comunicação digital mais acessível.

A proposta busca facilitar a compreensão das informações e a realização de tarefas em canais digitais. Entretanto, seus benefícios ainda precisam ser verificados por meio de testes comparativos e indicadores específicos.

Conclui-se que a análise de dados pode contribuir tanto para decisões de negócio quanto para a identificação de oportunidades de inovação social, desde que os resultados sejam interpretados de forma crítica, considerando suas limitações.

---

## ⚠️ Limitações do Projeto

- Os dados representam percentuais agregados, não registros individuais de consumidores.
- As médias entre países não foram ponderadas pelo tamanho da população.
- A comparação temporal foi restrita a 31 países com dados completos entre 2020 e 2025.
- Os resultados não explicam isoladamente as causas das diferenças observadas.
- Os indicadores de qualidade disponibilizados pelo Eurostat foram preservados, mas não foi realizada uma análise específica de sensibilidade às sinalizações.
- A regressão linear foi ajustada com apenas seis médias anuais.
- O modelo não foi validado com dados independentes.
- Não foram coletados dados próprios de campanhas ou experiências de consumidores.
- A ação de inovação social foi proposta, mas ainda não implementada.

---

## 📚 Referências

**EUROSTAT.** Base de dados estatísticos da União Europeia. Conjunto de dados `isoc_ec_ib20`. Disponível em: https://ec.europa.eu/eurostat/data/database.

**CHAPMAN, P. et al.** CRISP-DM 1.0: Step-by-step data mining guide. 2000.

**SCIKIT-LEARN.** Documentação oficial da biblioteca. Disponível em: https://scikit-learn.org/stable/.

**PANDAS.** Documentação oficial da biblioteca. Disponível em: https://pandas.pydata.org/docs/.

**MATPLOTLIB.** Documentação oficial da biblioteca. Disponível em: https://matplotlib.org/stable/.

---

## 👥 Autoria

**Ian Roscoe Vogel**

Projeto acadêmico desenvolvido na área de Ciência de Dados e Marketing Digital.

---

**Fonte dos dados:** Eurostat | **Período:** 2020–2025 | **Metodologia:** CRISP-DM
