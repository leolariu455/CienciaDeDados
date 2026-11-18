# O Fim da Era de Ouro: A Decadência de Jogadores no Primeiro Ano de Call of Duty na Steam

> **Análise da queda de jogadores no multiplayer de Black Ops II (2012), Ghosts (2013) e Advanced Warfare (2014) durante o primeiro ano após o lançamento, com uma proposta de relançamento acessível do Black Ops II para PC.**

---

## Visão Geral do Projeto (Metodologia CRISP-DM)

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

## Ciclo de Vida do Projeto (Fases do CRISP-DM)

### 1. Entendimento do Negócio
* **Problema de Negócio:** Black Ops II (2012) é considerado o último jogo da "era de ouro" de Call of Duty. Os lançamentos seguintes, Ghosts (2013) e Advanced Warfare (2014), começaram com menos jogadores no PC e perderam o público mais rápido. Para a franquia, perder jogadores no primeiro ano significa menos vendas de conteúdo, partidas mais vazias e menos interesse no lançamento seguinte.
* **Objetivo:** Medir e comparar a queda de jogadores no multiplayer de cada jogo durante os 12 meses após o lançamento, identificando em que momento cada um perde metade do público.
* **Perguntas de Análise:**
  1. Quantos jogadores cada jogo tinha no primeiro mês e quantos restavam no 12º mês?
  2. Em que mês cada jogo perdeu metade do público?
  3. A velocidade da queda aumentou de um jogo para o outro?
* **Solução Proposta:** Uma base de dados mensal do primeiro ano de cada jogo, um modelo de tendência de queda e um painel de BI comparando as curvas de retenção. Com base nos resultados, propomos o relançamento do Black Ops II Remaster para PC.

### 2. Entendimento dos Dados
* **Fonte:** SteamDB, que registra o número de jogadores simultâneos a partir dos dados públicos da Steam. Os arquivos foram exportados em 18/11/2026.
* **Jogos Analisados:**

| Jogo | Lançamento | Estúdio | Período analisado |
|------|-----------|---------|-------------------|
| Black Ops II | 12/11/2012 | Treyarch | nov/2012 a nov/2013 |
| Ghosts | 05/11/2013 | Infinity Ward | nov/2013 a nov/2014 |
| Advanced Warfare | 03/11/2014 | Sledgehammer Games | nov/2014 a nov/2015 |

* **Estrutura dos Dados:** Um registro diário de jogadores simultâneos por jogo (colunas `DateTime` e `Players`).
* **Por que esses jogos:** O histórico público de jogadores da Steam só começa em julho de 2012. Por isso, Black Ops (2010) e Modern Warfare 3 (2011) não têm dados do primeiro ano completo, e a análise começa no Black Ops II.
* **Análise Exploratória (EDA):** Gráficos da quantidade diária de jogadores, identificação de dias sem registro e de picos isolados (possíveis fins de semana gratuitos e promoções).

### 3. Preparação dos Dados
* **Limpeza e Tratamento:** Remoção dos dias anteriores ao lançamento, conversão das datas e identificação de dias sem registro. O Advanced Warfare tem lacunas entre fevereiro e abril de 2015 (mês 5 com apenas 1 dia registrado e mês 6 com 14 dias). Essas lacunas foram mantidas e sinalizadas na coluna `dias_com_dado`.
* **Engenharia de Recursos (Feature Engineering):** Criação de novas variáveis:
  * `mes`: mês desde o lançamento (1 a 12), contado a partir da data de lançamento de cada jogo
  * `media`, `mediana`, `maximo`, `minimo`: estatísticas mensais de jogadores
  * `retencao_vs_mes1_%`: jogadores do mês ÷ jogadores do mês 1 × 100
  * `var_mes_anterior_%`: variação em relação ao mês anterior
  * `dias_com_dado`: quantidade de dias com registro no mês
* **Modelagem Dimensional (BI):** Estruturação em formato **Star Schema**, com uma tabela fato de jogadores por dia e tabelas dimensão de jogos, estúdios e calendário.

### 4. Modelagem
* **Técnicas Utilizadas:** Análise descritiva comparativa e Regressão (tendência exponencial de queda) aplicada ao logaritmo da média mensal de jogadores.
* **Ferramenta:** IBM SPSS Modeler.
* **Abordagem:** Para cada jogo, o modelo estima a **taxa média de queda por mês** no primeiro ano, o que permite comparar a velocidade de perda de público entre os três jogos.

### 5. Avaliação
* **Métricas do Modelo:** O modelo de tendência explicou bem a queda dos três jogos, com **R² entre 0,92 e 0,94**.
* **Métricas de BI / KPIs de Negócio:**
  * **Retenção no 12º mês:** jogadores do mês 12 ÷ jogadores do mês 1.
  * **Mês em que o jogo perde metade do público.**
  * **Taxa média de queda por mês.**

---

## Análise dos Resultados

| Jogo | Média do 1º mês | Média do 12º mês | Retenção no 12º mês | Mês em que perdeu metade | Queda média por mês | Média do ano |
|------|----------------:|-----------------:|--------------------:|:------------------------:|--------------------:|-------------:|
| Black Ops II | 45.509 | 16.711 | **36,7%** | 8º mês | 8,5% | 28.405 |
| Ghosts | 23.704 | 3.562 | **15,0%** | 3º mês | 14,7% | 8.482 |
| Advanced Warfare | 21.378 | 2.508 | **11,7%** | 3º mês | 16,6% | 6.896 |

**Retenção mês a mês (% dos jogadores do 1º mês):**

| Mês | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
|-----|---|---|---|---|---|---|---|---|---|----|----|----|
| Black Ops II | 100 | 86,4 | 84,9 | 81,6 | 61,0 | 65,5 | 52,5 | 47,1 | 41,8 | 44,0 | 47,5 | 36,7 |
| Ghosts | 100 | 60,0 | 47,6 | 45,4 | 33,6 | 30,0 | 24,4 | 19,5 | 18,5 | 19,2 | 16,2 | 15,0 |
| Advanced Warfare | 100 | 59,8 | 45,6 | 36,6 | 29,1* | 24,3* | 20,4 | 17,5 | 15,4 | 13,4 | 13,2 | 11,7 |

\* Meses com poucos dias registrados.

**Principais conclusões:**
1. **O público encolheu de um lançamento para o outro.** O Ghosts começou com cerca de metade dos jogadores do Black Ops II no primeiro mês.
2. **A queda ficou quase duas vezes mais rápida.** O Black Ops II perdeu em média 8,5% dos jogadores por mês. O Ghosts e o Advanced Warfare perderam entre 14,7% e 16,6%.
3. **O Black Ops II segurou o público por muito mais tempo.** Levou 8 meses para perder metade dos jogadores, contra apenas 3 meses dos sucessores. Ghosts e Advanced Warfare perderam cerca de 40% já no segundo mês.
4. **Picos isolados no meio da queda.** Há dias com aumento forte de jogadores (por exemplo, mais de 70 mil no Black Ops II nos meses 3 e 4), que podem estar ligados a fins de semana gratuitos, promoções ou novos conteúdos.
5. **Interesse atual pelo Black Ops II.** Em julho de 2026, as versões de Black Ops e Black Ops II para PS4 e PS5 foram os jogos mais baixados do PS5 nos EUA/Canadá e na Europa, segundo o ranking oficial da PlayStation, o que mostra que ainda existe demanda por esse jogo.

**Limitações:**
* Os dados são apenas da Steam (PC). Na época, a maior parte do público jogava no Xbox 360 e no PlayStation 3.
* Os valores são registros diários do SteamDB, e não o total de pessoas que jogaram. Por isso, servem para comparar os jogos entre si.
* Os resultados mostram **associação** entre os jogos e a queda de público, e não provam a causa da queda.

---

## Impacto Social e Inovação na Estratégia de Marketing Digital

### 1. Necessidade social e relação com o negócio
* **Necessidade social: acesso e exclusão digital.** Os jogos atuais de Call of Duty custam caro (R$ 349,90 na PlayStation Store para Black Ops 7) e exigem equipamentos cada vez mais modernos. O Modern Warfare 4 (2026), por exemplo, não foi lançado para PS4 e Xbox One. Isso deixa de fora pessoas com computadores simples ou com menor renda.
* **Evidência documentada:** No lançamento de Ghosts, em novembro de 2013, a versão para PC exigia 6 GB de memória RAM e impedia a entrada de quem tinha menos, embora o jogo usasse cerca de 2 GB. Jogadores que tinham comprado na pré-venda não conseguiram jogar. A exigência só foi reduzida para 4 GB em um patch de 19/11/2013. Esse caso coincide com o início da queda de público analisada neste projeto.
* **Relação com o Marketing Digital:** A forma como a empresa divulga requisitos, preços e lançamentos pode **ampliar** o acesso (informação clara, versões leves, preços acessíveis) ou **agravar** a exclusão (requisitos exagerados, foco apenas em equipamentos caros).

### 2. Públicos, benefícios e riscos

| Público | Como é afetado |
|---------|----------------|
| Jogadores com PC simples ou de menor renda | Não conseguem rodar ou comprar os CoDs atuais |
| Ex-jogadores da era de ouro | Pararam de jogar na transição para Ghosts e Advanced Warfare |
| Novos jogadores | Nunca jogaram o Black Ops II e hoje não têm uma porta de entrada acessível para a franquia |

* **Benefício social:** Mais pessoas conseguem jogar um Call of Duty online, com preço e requisitos acessíveis.
* **Risco:** Trapaceiros (hackers), que já foram um problema nos relançamentos de Black Ops e Black Ops II no PlayStation em 2026 e afastam justamente os jogadores novos.
* **Medida de mitigação:** Sistema anti-cheat atualizado desde o lançamento e canal de denúncia em português.

### 3. Dados e evidências
* **Fontes:** SteamDB (jogadores diários de Black Ops II, Ghosts e Advanced Warfare), ranking oficial de downloads da PlayStation Store (julho de 2026), PlayStation Store Brasil (preços) e reportagens de 2013 sobre o caso Ghosts.
* **Período:** novembro de 2012 a novembro de 2015 (primeiro ano de cada jogo) e julho de 2026 (relançamento no PlayStation).
* **Público a que os dados se referem:** Jogadores de PC na Steam (dados de 2012 a 2015) e jogadores de PlayStation (2026).
* **Resultados observados:**
  * Ghosts e Advanced Warfare perderam cerca de 85% a 88% do público no primeiro ano, contra 63% do Black Ops II.
  * O caso Ghosts mostra que requisitos exagerados barraram jogadores no lançamento.
  * Em julho de 2026, Black Ops II foi o jogo mais baixado do PS5 nos EUA/Canadá e na Europa.
* **Resultados esperados (ainda não medidos):** Que um relançamento acessível para PC inclua jogadores com computadores simples e mantenha o público por mais tempo. Isso só poderá ser verificado com os indicadores após o lançamento.
* **Limites:** Os dados de 2012 a 2015 são só da Steam. Não é possível afirmar que os requisitos causaram a queda de público, apenas que os dois aconteceram no mesmo período. As vendas de 2026 no PlayStation são estimativas de empresas de pesquisa.

### 4. Leitura pelo CRISP-DM

| Etapa | Questão social considerada | Evidência ou decisão do projeto | Risco ou limitação |
|-------|----------------------------|---------------------------------|--------------------|
| Compreensão do negócio | Quem deixa de jogar e por quê? | Objetivo social: ampliar o acesso de jogadores com PCs simples e menor renda | Ex-jogadores que migraram para console não aparecem na análise |
| Compreensão dos dados | Os dados representam todos os jogadores? | Uso de dados públicos da Steam de três jogos | Dados só de PC; sem informação de renda ou de equipamento dos jogadores |
| Preparação dos dados | Como tratar dias sem registro? | Lacunas mantidas e sinalizadas, sem inventar valores | Meses 5 e 6 do Advanced Warfare têm poucos dias registrados |
| Modelagem e análise | A queda foi igual para todos os jogos? | Comparação da taxa de queda mensal entre os três jogos | Associação não prova causa |
| Avaliação | A proposta beneficia o público sem prejudicar o negócio? | Critérios: acesso de PCs simples e retenção no 12º mês | Trapaceiros podem afastar novos jogadores |
| Implantação | Como acompanhar e corrigir a ação? | Indicadores medidos mensalmente no primeiro ano | Dependência de dados internos da empresa sobre hardware dos jogadores |

### 5. Ação de inovação social
Para enfrentar **a falta de acesso de jogadores com computadores simples e menor renda aos jogos atuais da franquia**, propomos **o relançamento do Black Ops II Remaster para PC, com requisitos baixos, preço acessível em reais, legendas e dublagem em português e opções de acessibilidade (como modo para daltônicos e legendas ampliadas)**, no canal **Steam e redes oficiais de Call of Duty Brasil**, voltado a **ex-jogadores da era de ouro e a novos jogadores**. Ele pode contribuir para **recuperar o público perdido desde 2013** e gerar **acesso mais amplo a um jogo online da franquia**. Para reduzir **o risco de trapaceiros**, adotaremos **um sistema anti-cheat atualizado desde o lançamento**.

* **Recursos:** Equipe de desenvolvimento para o remaster, equipe de marketing para a campanha na Steam e nas redes sociais e equipe de segurança para o anti-cheat.
* **Prazo:** Lançamento planejado com campanha de divulgação de 2 meses.

### 6. Indicadores e validação

| Indicador | O que será medido | Como será calculado | Linha de base e meta | Fonte e periodicidade | Responsável |
|-----------|-------------------|---------------------|----------------------|-----------------------|-------------|
| **Acesso (mudança para o público):** jogadores com PCs abaixo do requisito dos CoDs atuais que conseguem rodar o remaster (%) | Se pessoas que antes não conseguiam jogar passaram a conseguir | Jogadores com PC abaixo do requisito mínimo dos CoDs atuais que rodam o remaster ÷ total desses jogadores que tentaram × 100 | Base: 0% (hoje não rodam os CoDs atuais). Meta: 90% | Dados de hardware da Steam; na primeira semana e depois mensalmente | Equipe de produto |
| **Resultado:** retenção no 12º mês (%) | Se o público se mantém ao longo do primeiro ano | Média de jogadores no mês 12 ÷ média no mês 1 × 100 | Base: 36,7% (Black Ops II original). Meta: acima de 40% | SteamDB; mensalmente durante o primeiro ano | Equipe de marketing |

> **Atenção:** Vendas, visualizações e cliques mostram apenas o alcance da campanha. O indicador de acesso mede o que muda para o público: se pessoas com computadores simples conseguem, de fato, jogar.

### 7. Limites e acompanhamento
* Ainda é preciso verificar, após o lançamento, se o remaster realmente alcança jogadores com computadores simples e se mantém o público por mais tempo.
* A estratégia deverá ser ajustada se a porcentagem de acesso ficar abaixo da meta (revisando os requisitos), se a retenção cair mais rápido que a do Black Ops II original ou se houver aumento de denúncias de trapaça.

---

## Considerações Finais

A análise mostrou que a era de ouro de Call of Duty no PC terminou com o Black Ops II: seus sucessores, Ghosts e Advanced Warfare, começaram com cerca de metade dos jogadores e perderam o público quase duas vezes mais rápido, com retenção de 15% e 11,7% no 12º mês, contra 36,7% do Black Ops II. O sucesso do relançamento de Black Ops e Black Ops II no PlayStation em 2026 indica que ainda existe interesse por esse jogo.

A estratégia proposta contribui para **o acesso de jogadores com computadores simples e menor renda** ao **relançar o Black Ops II Remaster para PC com requisitos baixos, preço acessível e opções de acessibilidade**. Os dados analisados indicam que a queda de público coincidiu com jogos mais exigentes e com o caso de requisitos exagerados do Ghosts, mas ainda não permitem confirmar que essa foi a causa da queda nem que o remaster vai incluir esses jogadores, pois não há dados do relançamento para PC. A organização deverá acompanhar **a porcentagem de jogadores com PCs simples que conseguem rodar o jogo e a retenção no 12º mês** e revisar a ação mensalmente durante o primeiro ano, conciliando o objetivo de recuperar o público da franquia com a ampliação do acesso ao jogo.

---

## Fontes
* SteamDB – histórico de jogadores (exportado em 18/11/2026):
  * [Call of Duty: Black Ops II – Multiplayer](https://steamdb.info/app/202990/charts/)
  * [Call of Duty: Ghosts – Multiplayer](https://steamdb.info/app/209170/charts/)
  * [Call of Duty: Advanced Warfare](https://steamdb.info/app/209650/charts/)
* [SteamCharts – início da coleta de dados da Steam em julho de 2012](https://steamcharts.com/about)
* [PlayStation Store Brasil – preço de Call of Duty: Black Ops 7](https://store.playstation.com/pt-br/product/UP0002-PPSA01649_00-CODBO7VAULT00001)
* [Call of Duty (blog oficial) – anúncio do Modern Warfare 4](https://www.callofduty.com/blog/2026/05/call-of-duty-modern-warfare-4-announcement)
* [Game Overdrive – Black Ops II é o jogo mais baixado do PS5 em julho de 2026 (ranking oficial da PlayStation)](https://gameoverdrive.com.br/black-ops-2-jogo-mais-baixado-ps5-julho-2026/)
* [OpenCritic/GameRant – lançamento de Black Ops e Black Ops II para PS4 e PS5 em 09/07/2026](https://opencritic.com/news/34659/call-of-duty-black-ops-2-on-ps5-is-officially-more-popular-than-bo7-and-warzone-combined)
* [inkl – problemas com trapaças nos relançamentos de Black Ops e Black Ops II](https://www.inkl.com/news/call-of-duty-black-ops-and-black-ops-2-ports-were-both-in-the-top-10-us-playstation-games-last-week-despite-cheating-and-dlc-mess)
* Caso do requisito de 6 GB de RAM de Call of Duty: Ghosts (novembro de 2013):
  * [High-Def Digest – jogadores da pré-venda impedidos de jogar](https://www.highdefdigest.com/news/show/Infinity_Ward/Call_of_Duty/Call_of_Duty_Ghosts_6GB_RAM_Requirement_Patched_Out/13150)
  * [Softpedia – jogo exigia 6 GB, mas usava cerca de 2 GB](https://games.softpedia.com/blog/Download-Now-Call-of-Duty-Ghosts-PC-Updates-to-Remove-6GB-RAM-Limit-401562.shtml)
  * [Shacknews – patch reduz o requisito para 4 GB](https://shacknews.com/article/82082/call-of-duty-ghosts-patch-lowers-pc-ram-requirement)
  * [PC Gamer – patch reduz o requisito de 6 GB](https://www.pcgamer.com/call-of-duty-ghosts-patch-lowers-6gb-ram-requirement-adds-e-sports-features)

---

## Autores e Contato

* **Leonardo Lariú**
* **Pedro Zinn**
