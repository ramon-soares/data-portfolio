# Superstore — análise de vendas e rentabilidade

Análise exploratória de dados de varejo para identificar onde o lucro se concentra e quais regiões, categorias e produtos apresentam prejuízo. O projeto conecta agregações e visualizações a hipóteses de melhoria do desempenho comercial.

[Acessar o notebook](superstore.ipynb) · [Voltar ao portfólio](../README.md)

## Problema de negócio

Uma operação de varejo precisa compreender quais partes do catálogo contribuem para o resultado e quais exigem investigação. O trabalho explora as seguintes perguntas:

- Quais regiões e categorias geram mais lucro total e médio por registro de venda?
- Quais produtos e subcategorias acumulam os maiores prejuízos?
- Como os resultados variam entre regiões e estados?
- Que padrões de rentabilidade aparecem nos diferentes níveis de desconto?

## Dados

| Característica | Descrição |
| --- | --- |
| Base | Sample Superstore |
| Fonte | [Superstore Dataset, no Kaggle](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final) |
| Arquivo local | [Sample - Superstore.csv](dataset/Sample%20-%20Superstore.csv) |
| Dimensão | 9.994 registros e 21 colunas na base original |
| Período dos pedidos | 3 de janeiro de 2014 a 30 de dezembro de 2017 |
| Abrangência | Vendas nos Estados Unidos |
| Unidade de análise | Registro de item vendido; um pedido pode ocupar várias linhas |

Os atributos incluem datas, localização, segmento de cliente, categoria, subcategoria, produto, vendas, quantidade, desconto e lucro. A inspeção registrada no notebook não identificou valores nulos.

## Abordagem

1. **Inspeção e preparação:** leitura do CSV com codificação Windows-1252, estatísticas descritivas, padronização dos nomes das colunas e conversão de datas.
2. **Visão geral:** levantamento de produtos, volume vendido, vendas totais e lucro total.
3. **Comparação de resultados:** agregação do lucro por modalidade de envio, segmento, região, categoria, quantidade e desconto.
4. **Investigação detalhada:** rankings de cidades e produtos, além de recortes de categorias e subcategorias por região e estado.
5. **Interpretação:** discussão de oportunidades e pontos de atenção com base nos padrões observados.

**Ferramentas:** Python, Jupyter Notebook, Pandas, NumPy, Matplotlib e Seaborn.

## Principais resultados

Os indicadores abaixo correspondem ao período completo do CSV versionado. Os valores de vendas e lucro mantêm a unidade monetária do dataset.

| Indicador | Valor |
| --- | ---: |
| Vendas totais | 2.297.200,86 |
| Lucro total | 286.397,02 |
| Unidades vendidas | 37.873 |
| Produtos distintos por ID | 1.862 |

- **Technology lidera o lucro por categoria:** aproximadamente 145,45 mil, seguida por Office Supplies, com 122,49 mil. Furniture soma 18,45 mil.
- **West e East concentram os maiores lucros regionais:** aproximadamente 108,42 mil e 91,52 mil, respectivamente.
- **Tables, Bookcases e Supplies apresentam lucro agregado negativo:** Tables acumula o maior prejuízo entre as subcategorias, com cerca de 17,73 mil.
- **Há diferenças relevantes dentro de Furniture:** o notebook aprofunda o prejuízo da região Central e os resultados de Texas e Illinois.
- **O desempenho varia entre produtos:** Canon imageCLASS 2200 Advanced Copier apresenta o maior lucro agregado por ID; Cubify CubeX 3D Printer Double Head Print apresenta o maior prejuízo.

Esses achados ajudam a priorizar a revisão de descontos, preços e condições comerciais nos recortes deficitários. São hipóteses para investigação: o projeto não mede o efeito de mudanças implementadas na operação.

## Como executar

Para leitura, abra o [notebook no GitHub](superstore.ipynb). Para executar, entre nesta pasta a partir da raiz do repositório e prepare um ambiente virtual:

```powershell
cd superstore_data_analysis
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install notebook numpy pandas matplotlib seaborn
.\.venv\Scripts\python.exe -m notebook superstore.ipynb
```

Execute as células na ordem apresentada, com o diretório de trabalho nesta pasta, para preservar o caminho relativo `dataset/Sample - Superstore.csv`.

O notebook registra Python 3.9.7 no ambiente original e não possui um arquivo com versões fixadas das bibliotecas. Algumas agregações usam o comportamento histórico de `groupby().sum()`; a execução com versões diferentes do Pandas pode exigir ajustes. As saídas salvas permanecem disponíveis para consulta.

## Estrutura do projeto

| Arquivo ou pasta | Conteúdo |
| --- | --- |
| [superstore.ipynb](superstore.ipynb) | Preparação, análise, gráficos e interpretação dos resultados. |
| [dataset/](dataset/) | CSV utilizado na análise e arquivo compactado da base. |
| [img/projeto_insights.png](img/projeto_insights.png) | Esquema de referência do fluxo analítico utilizado no projeto original. |

## Limitações e próximos passos

A análise é descritiva e considera o histórico disponível. As relações observadas entre desconto, localização e lucro não isolam efeitos causais. Os registros também não permitem, por si só, concluir que retirar um produto do catálogo aumentaria o lucro da operação.

Como continuidade, seria possível aprofundar a evolução temporal, comparar margens entre segmentos e testar hipóteses comerciais com dados adicionais de custos e demanda.
