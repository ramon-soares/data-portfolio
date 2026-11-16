# Tour & Travels — previsão de churn

Estudo de classificação supervisionada para identificar clientes com indicação de cancelamento em uma empresa de turismo. O trabalho explora a base, compara nove algoritmos e aprofunda o uso de uma árvore de decisão com busca de hiperparâmetros.

[Acessar o notebook](tour_travel_customer_churn.ipynb) · [Voltar ao portfólio](../README.md)

## Problema de negócio

Identificar clientes propensos a deixar um serviço pode apoiar a priorização de ações de retenção. Neste projeto, o objetivo técnico é classificar o indicador de churn a partir dos atributos disponíveis e examinar o equilíbrio entre precisão e recall.

A variável `Target` representa as classes **0 — não cancelou** e **1 — cancelou**. O estudo avalia classificadores; não estima o efeito de uma campanha de retenção.

## Dados

| Característica | Descrição |
| --- | --- |
| Base | Tour & Travels Customer Churn Prediction |
| Fonte | [Dataset no Kaggle](https://www.kaggle.com/datasets/tejashvi14/tour-travels-customer-churn-prediction) |
| Arquivo local | [Customertravel.csv](data/Customertravel.csv) |
| Dimensão | 954 registros, seis atributos preditores e uma variável alvo |
| Distribuição do alvo | 730 clientes na classe 0 (76,52%) e 224 na classe 1 (23,48%) |

Os atributos descrevem idade, frequência de voos, classe de renda anual, utilização de serviços, sincronização com redes sociais e reserva de hotel. O notebook verifica valores nulos, explora as distribuições e examina relações entre as variáveis.

## Abordagem

1. **Preparação:** inspeção da base, padronização de nomes e análise do desbalanceamento do alvo.
2. **Exploração:** gráficos de distribuição e uma matriz de correlação com codificação numérica auxiliar.
3. **Representação:** conversão dos atributos categóricos em variáveis indicadoras com `pd.get_dummies`.
4. **Comparação inicial:** separação de 70% para treino e 30% para teste, com `random_state=42`, e avaliação por F1 macro.
5. **Aprofundamento:** busca de hiperparâmetros da árvore de decisão com `GridSearchCV`, cinco divisões de validação cruzada e `scoring='f1_macro'`.
6. **Interpretação:** matrizes de confusão, relatórios de classificação e representação textual da árvore.

Foram comparados AdaBoost, Decision Tree, Extra Trees, Gaussian Naive Bayes, Gradient Boosting, K-Nearest Neighbors, Logistic Regression, Random Forest e Support Vector Classifier.

**Ferramentas:** Python, Jupyter Notebook, Pandas, NumPy, Matplotlib, Seaborn e Scikit-learn. O pipeline da busca contém uma etapa `scaler=None`, sem aplicação de padronização.

## Resultados registrados

As métricas abaixo correspondem às saídas salvas no notebook.

| Classificador | F1 macro na comparação inicial |
| --- | ---: |
| Decision Tree | 0,8450 |
| Gradient Boosting | 0,8291 |
| Random Forest | 0,8148 |
| K-Nearest Neighbors | 0,7958 |
| Extra Trees | 0,7827 |
| AdaBoost | 0,7634 |
| Logistic Regression | 0,7411 |
| Gaussian Naive Bayes | 0,7312 |
| Support Vector Classifier | 0,4328 |

A árvore de decisão apresentou o melhor resultado na comparação inicial. Para a classe de cancelamento, o relatório inicial registra **precisão de 0,80, recall de 0,72 e F1 de 0,76**, em 68 exemplos dessa classe no conjunto de teste.

Na busca de hiperparâmetros, o melhor resultado médio de validação cruzada registrado foi **F1 macro de 0,8591**, com `criterion='gini'`, `max_depth=7`, `min_samples_leaf=4` e `min_samples_split=2`.

### Como interpretar a avaliação

O F1 macro atribui o mesmo peso às duas classes, contribuindo para uma leitura que não seja dominada pela classe majoritária. O recall da classe 1 também é relevante para entender quantos cancelamentos o classificador identifica.

**A avaliação final exige uma ressalva metodológica:** a busca é ajustada com `grid.fit(X, y)`, usando a base completa. O melhor estimador é então avaliado em `X_test`, cujos registros já participaram desse ajuste. Assim, a acurácia final de 0,93 e o F1 macro de aproximadamente 0,90 exibidos no notebook não constituem uma avaliação em dados independentes e podem ser otimistas.

A comparação inicial também utiliza o mesmo conjunto de teste para selecionar o algoritmo. Para uma estimativa final de generalização, é necessário reservar um conjunto de teste que não participe da escolha do modelo nem do ajuste dos hiperparâmetros.

## Como executar

Para leitura, abra o [notebook no GitHub](tour_travel_customer_churn.ipynb). Para executar, entre nesta pasta a partir da raiz do repositório e prepare um ambiente virtual:

```powershell
cd tour_travels_customer_churn
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install notebook numpy pandas matplotlib seaborn scikit-learn
.\.venv\Scripts\python.exe -m notebook tour_travel_customer_churn.ipynb
```

Execute as células na ordem apresentada, com o diretório de trabalho nesta pasta, para que `data/Customertravel.csv` seja encontrado.

O notebook não possui um arquivo com versões fixadas das dependências; versões diferentes podem alterar o comportamento de algumas células. A grade original também inclui valores inválidos, como zero para `max_depth` e `min_samples_leaf`, além de valores menores que dois para `min_samples_split`. Isso provoca falhas em parte dos ajustes e aumenta o custo da busca. A reprodução do experimento deve considerar esses pontos e a limitação de avaliação descrita acima.

## Estrutura do projeto

| Arquivo ou pasta | Conteúdo |
| --- | --- |
| [tour_travel_customer_churn.ipynb](tour_travel_customer_churn.ipynb) | Análise exploratória, comparação de modelos, busca e avaliação. |
| [data/Customertravel.csv](data/Customertravel.csv) | Base utilizada no experimento. |
| [img/passos_projeto_ml.png](img/passos_projeto_ml.png) | Esquema de referência do fluxo de Machine Learning do projeto original. |

## Próximos passos

- Separar treino e teste com estratificação e realizar a seleção de modelos somente dentro do conjunto de treino.
- Restringir a grade a valores válidos e avaliar o modelo escolhido uma única vez no teste reservado.
- Comparar com um classificador de referência e examinar precisão, recall e F1 da classe de churn.
- Investigar ponderação de classes ou reamostragem dentro da validação cruzada.
- Relacionar erros de classificação aos custos das ações de retenção, caso esses dados estejam disponíveis.
