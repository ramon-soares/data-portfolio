# Portfólio de Análise e Ciência de Dados

Projetos desenvolvidos por **Ramon Soares** para aplicar e aprofundar habilidades de análise e ciência de dados com Python. Os trabalhos abordam exploração de dados, investigação de problemas de negócio, classificação supervisionada e sistemas de recomendação.

Cada pasta contém um projeto independente, com seus dados, implementação e documentação. Os READMEs apresentam o contexto, os métodos, os resultados disponíveis e as instruções de execução.

## Projetos

| Projeto | Objetivo | Técnicas e ferramentas | Entrega |
| --- | --- | --- | --- |
| [Superstore — análise de vendas e rentabilidade](superstore_data_analysis/) | Investigar a distribuição de lucros e prejuízos por região, categoria e produto. | Pandas, NumPy, Matplotlib, Seaborn e análise exploratória. | Notebook com visualizações, achados e hipóteses de ação. |
| [Tour & Travels — previsão de churn](tour_travels_customer_churn/) | Explorar indicadores de cancelamento e comparar modelos de classificação. | Scikit-learn, codificação de variáveis, F1 macro, árvore de decisão e GridSearchCV. | Notebook com comparação de nove classificadores e avaliação do experimento. |
| [Recomendação de animes por similaridade](similarity_anime_recommendation_system/) | Recomendar títulos a partir dos gêneros e das avaliações informadas pelo usuário. | Pandas, similaridade de Jaccard, média ponderada, Requests, Beautiful Soup e Streamlit. | Aplicação interativa com ranking de recomendações. |

## Habilidades demonstradas

- **Preparação de dados:** leitura de CSVs, inspeção de qualidade, padronização de colunas, conversão de datas e codificação de atributos categóricos.
- **Análise exploratória:** agregações, comparação de segmentos, identificação de prejuízos e investigação de padrões com visualizações.
- **Modelagem:** comparação de classificadores, seleção de hiperparâmetros e interpretação de métricas em uma base desbalanceada.
- **Recomendação:** representação binária de atributos e combinação de similaridades com preferências individuais.
- **Comunicação de resultados:** contextualização do problema, documentação dos métodos e discussão dos limites de cada trabalho.

## Destaques dos trabalhos

**Superstore:** análise de 9.994 registros, com aproximadamente 2,30 milhões em vendas e 286,40 mil de lucro na base. A investigação identifica diferenças de rentabilidade entre categorias e detalha subcategorias com resultado negativo.

**Tour & Travels:** estudo de 954 clientes, dos quais 224 apresentam cancelamento. A árvore de decisão alcançou F1 macro de aproximadamente 0,845 na comparação inicial. O README do projeto explica as limitações da seleção e da avaliação posterior.

**Recomendação de animes:** aplicação baseada em uma matriz de 4.148 títulos e 73 atributos binários de gêneros, temas e classificações. As notas do usuário ponderam a similaridade para gerar recomendações ordenadas.

Os projetos têm finalidade educacional e de portfólio. Os resultados descrevem as bases e os experimentos presentes neste repositório; não representam impacto comercial medido ou desempenho validado em produção.

## Como explorar

1. Acesse o README do projeto pela tabela acima para conhecer o problema e os resultados.
2. Abra os notebooks diretamente no GitHub para consultar o código e as saídas salvas.
3. Para executar localmente, siga as instruções específicas de cada pasta. Os caminhos de leitura dos dados são relativos ao diretório do projeto.

```text
Portfolio-Data-Science/
├── README.md
├── superstore_data_analysis/
│   ├── README.md
│   ├── superstore.ipynb
│   └── dataset/
├── tour_travels_customer_churn/
│   ├── README.md
│   ├── tour_travel_customer_churn.ipynb
│   └── data/
└── similarity_anime_recommendation_system/
    ├── README.md
    ├── run.py
    ├── processing.py
    ├── interface.py
    ├── get_animes_data.py
    ├── requirements.txt
    └── csv/
```

As fontes dos dados estão documentadas em cada projeto. Para executar os trabalhos, utilize ambientes virtuais separados e consulte as observações sobre as versões originais das dependências.

## Autor

**Ramon Soares** · [Perfil no GitHub](https://github.com/ramon-soares)
