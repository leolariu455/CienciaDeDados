# 📊 Call of Duty no Topo: Quanto Tempo a Franquia Segura seu Público?

> **Análise do tempo que cada Call of Duty se mantém no top 3 dos rankings após o lançamento, identificando o momento da queda e os fatores que influenciam essa permanência.**

---

## 📌 Visão Geral do Projeto (Metodologia CRISP-DM)

Este projeto foi desenvolvido seguindo a metodologia **CRISP-DM**, garantindo um ciclo de desenvolvimento estruturado e focado em gerar valor real para o negócio. Combinamos **Ciência de Dados** para modelagem preditiva e **Business Intelligence (BI)** para visualização estratégica dos resultados.

```text
       ┌────────────────────────────────────────────────────────┐
       │                                                        │
       ▼                                                        │
┌──────────────┐      ┌──────────────┐      ┌──────────────┐    │
│ 1. Entendimento     │ 2. Entendimento     │ 3. Preparação│    │
│    do Negócio│ ───> │    dos Dados │ ───> │    dos Dados │    │
└──────────────┘      └──────────────┘      └──────────────┘    │
                                                   │            │
                                                   ▼            │
┌──────────────┐      ┌──────────────┐      ┌──────────────┐    │
│ 6. Implantação      │ 5. Avaliação │ <─── │ 4. Modelagem │    │
│   (BI e Prod)│ <─── │  (Métricas)  │      │  (Algoritmos)│    │
└──────────────┘      └──────────────┘      └──────────────┘    │
       │                                                        │
       └────────────────────────────────────────────────────────┘
```

---

## 🛠️ Ciclo de Vida do Projeto (Fases do CRISP-DM)

### 1. Entendimento do Negócio
* **Problema de Negócio:** Call of Duty lança um jogo novo todo ano e historicamente domina os rankings de vendas. Em 2025, porém, o Black Ops 7 terminou o ano em 5º lugar nos EUA, e pela primeira vez um Battlefield vendeu mais que um Call of Duty. Isso levanta a dúvida: a franquia está perdendo a capacidade de se manter no topo?
* **Objetivo:** Medir quanto tempo cada Call of Duty se mantém no top 3 dos rankings após o lançamento, identificar o momento em que o público começa a cair e descobrir quais fatores influenciam essa permanência.
* **Perguntas de Análise:**
  1. Quantos meses cada CoD permanece no top 3 após o lançamento?
  2. Esse tempo está diminuindo ao longo dos anos?
  3. Fatores como estúdio, concorrentes, temporadas e Game Pass influenciam a permanência no topo?
* **Solução Proposta:** Uma base de dados histórica dos rankings mensais, um modelo que explique a permanência no top 3 e um painel de BI com a trajetória de cada jogo.

### 2. Entendimento dos Dados
* **Fontes:**
  * **Circana (EUA):** ranking mensal dos jogos mais vendidos, divulgado publicamente pelo analista Mat Piscatella.
  * **GSD (Europa):** ranking semanal de vendas, publicado pelo site The Game Business.
  * **PlayStation Store:** ranking mensal de downloads, publicado pela Sony (EUA/Canadá e Europa).
  * **SteamDB / SteamCharts:** número de jogadores simultâneos na Steam (dados globais).
* **Jogos Analisados:**

| Jogo | Ano | Estúdio |
|------|-----|---------|
| Modern Warfare | 2019 | Infinity Ward |
| Black Ops Cold War | 2020 | Treyarch (com Raven) |
| Vanguard | 2021 | Sledgehammer |
| Modern Warfare II | 2022 | Infinity Ward |
| Modern Warfare III | 2023 | Sledgehammer |
| Black Ops 6 | 2024 | Treyarch |
| Black Ops 7 | 2025 | Treyarch |

* **Análise Exploratória (EDA):** Gráficos da posição de cada jogo mês a mês, comparação entre regiões e identificação de padrões de queda. *(Os arquivos desta fase estão localizados em `notebooks/1_eda/`)*.

### 3. Preparação dos Dados
* **Limpeza e Tratamento:** Padronização dos nomes dos jogos entre as fontes, conversão dos rankings semanais da GSD para mensais e tratamento dos meses em que o jogo não aparece no ranking.
* **Engenharia de Recursos (Feature Engineering):** Criação de novas variáveis como:
  * `meses_desde_lancamento` (alinha todos os jogos a partir do mês 0)
  * `meses_no_top3` e `meses_no_top10`
  * `mes_da_queda` (primeiro mês fora do top 3)
  * `posicao_media_primeiro_ano`
  * `estudio`, `concorrente_forte_no_periodo`, `inicio_de_temporada`, `game_pass`
* **Modelagem Dimensional (BI):** Estruturação das tabelas em formato **Star Schema**, com uma tabela fato de rankings mensais e tabelas dimensão de jogos, estúdios, fontes e calendário.

### 4. Modelagem
* **Algoritmos Testados:** Regressão Linear (para prever quantos meses o jogo fica no top 3) e Árvore de Decisão (para classificar jogos em "permanência alta" ou "permanência baixa").
* **Ferramenta:** IBM SPSS Modeler.
* **Abordagem:** Por ter poucos jogos na base, a análise combina o modelo com comparações descritivas entre jogos, estúdios e regiões.

### 5. Avaliação
* **Métricas do Modelo:** [Preencher após a modelagem, ex: R² de X e erro médio de Y meses]
* **Métricas de BI / KPIs de Negócio:**
  * **Tempo médio no top 3:** número médio de meses que um CoD permanece entre os 3 primeiros.
  * **Mês da queda:** em que mês após o lançamento o jogo sai do top 3.
  * **Tendência da franquia:** variação do tempo no topo de um lançamento para o outro.
* **Limitações:** Não existe um ranking mundial público e completo, por isso foram combinadas fontes regionais (EUA e Europa). Os rankings da Circana e da GSD medem vendas, não jogadores ativos, e na Steam os CoDs recentes dividem o mesmo aplicativo, o que impede separar os jogadores de cada jogo.

### 6. Implantação
* **Atualização dos Dados:** A base pode ser atualizada todo mês com os novos rankings divulgados, incluindo os próximos lançamentos da franquia.
* **Camada de Visualização (BI):** Os resultados são disponibilizados em um painel interativo no **[Power BI / Tableau / Looker Studio]** com duas visões principais:
  1. *Visão da Franquia:* evolução do tempo no topo de cada CoD ao longo dos anos.
  2. *Visão por Jogo:* trajetória mês a mês de cada lançamento, com o momento da queda e os eventos do período.
* **Recomendações:** Conclusões práticas para a franquia, como o melhor momento para lançar novas temporadas e conteúdos.

---

## 📁 Estrutura de Pastas (Mapeada pelo CRISP-DM)

```text
├── docs/                  # 1. Negócio: dicionário de dados e escopo do projeto
├── dados/                 # 2. Dados: rankings coletados (Circana, GSD, PS Store, Steam)
│   ├── brutos/
│   └── tratados/
├── notebooks/             # 2. Dados: análise exploratória (EDA)
│   ├── 1_eda/
│   └── 2_testes_modelagem/
├── modelagem/             # 3 e 4. Streams do SPSS Modeler e scripts de preparação
├── bi/                    # 6. Implantação: arquivos do dashboard
└── README.md              # Este arquivo
```
*Para abrir e editar a camada de BI, abra o arquivo localizado em `bi/[nome_do_painel]` utilizando o [Power BI Desktop].*

---

## 👥 Autores e Contato

* **[Leonardo Lariú e Pedro Zinn]** 
