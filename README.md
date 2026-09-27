# MVP: Pipeline de Dados na Nuvem — Metagame de Torneios do MTGO

Projeto de MVP da Sprint de Engenharia de Dados (PUC-Rio), com o objetivo de construir, do zero, um pipeline de dados completo na nuvem — da coleta bruta à análise de negócio — usando como estudo de caso o metagame competitivo de **Magic: The Gathering**.

## Sobre o projeto

O trabalho analisa resultados de torneios do **mtgo.com** entre 2022 e meados de 2024, buscando entender:

- Como o metagame (quais cartas dominam) evoluiu ao longo do tempo, por formato;
- Quais cartas funcionam como *staples* (sempre no mainboard) versus respostas situacionais de sideboard;
- Se existe relação entre o custo de mana médio de um deck e seu sucesso competitivo;
- Se jogadores com mais participações em torneios mantêm uma taxa de vitória consistente.

O pipeline segue a **Arquitetura Medalhão** (Bronze → Silver → Gold), implementado inteiramente no **Databricks Free Edition**, com o modelo final organizado em um **esquema estrela** (dimensões de torneio, jogador, deck e carta; fatos de carta-em-deck e resultado-de-deck).

## Fontes de dados

- **[MTGODecklistCache](https://github.com/Badaro/MTGODecklistCache)** — decklists e resultados de torneios do mtgo.com.
- **[Scryfall](https://scryfall.com)** (bulk data *Oracle Cards*) — enriquecimento com custo de mana, tipo e cor de cada carta.

Detalhes de escopo, licença e tratamento de cada fonte estão documentados no relatório completo (link abaixo).

## Estrutura dos notebooks

| Notebook | Conteúdo |
|---|---|
| `mvp00-objetivo` | Problema, perguntas de negócio e terminologia |
| `mvp01-prep` | Preparação inicial |
| `mvp02-import` | Extração dos dados brutos |
| `mvp03-bronze` | Ingestão para a camada Bronze |
| `mvp04-silver` | Limpeza, decomposição e enriquecimento (Silver) |
| `mvp05-gold` | Modelagem dimensional — esquema estrela (Gold) |
| `mvp06-perguntas` | Consultas SQL respondendo cada pergunta de negócio |
| `mvp07-consideracoes-finais` | Dificuldades, trabalhos futuros e autoavaliação |

## Documentação completa

O relatório completo — contexto, coleta, modelagem, catálogo de dados, qualidade de dados e análise, com evidências de execução — está disponível em [`MVP_MTGO_Documentacao.docx`](./MVP_MTGO_Documentacao.docx).

## Tecnologias

- **Databricks Free Edition** (PySpark + SQL)
- **Delta Lake**
- **Unity Catalog** (governança e catálogo de dados)
- **Scryfall API** (enriquecimento de dados)