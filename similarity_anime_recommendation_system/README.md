# Recomendação de animes por similaridade

Aplicação interativa que recomenda animes com base nas características dos títulos selecionados pelo usuário. O sistema combina **similaridade de Jaccard** entre atributos binários com uma **média ponderada pelas notas individuais**, gerando um ranking de recomendações em Streamlit.

[Voltar ao portfólio](../README.md)

![Imagem utilizada na tela inicial da aplicação](img/home_screen.jpg)

## Objetivo

Facilitar a descoberta de títulos a partir de preferências explícitas: o usuário seleciona animes que conhece, atribui notas e recebe sugestões com características semelhantes. A abordagem é de recomendação baseada em conteúdo, usando gêneros, temas e classificações presentes na base.

O projeto reúne coleta de dados, preparação de atributos, cálculo de similaridade e apresentação dos resultados em uma aplicação web.

## Dados

Os dados foram coletados do [MyAnimeList](https://myanimelist.net) com o script [get_animes_data.py](get_animes_data.py). Os CSVs necessários para utilizar a aplicação já estão incluídos no repositório.

| Arquivo | Conteúdo |
| --- | --- |
| [csv/id_animes.csv](csv/id_animes.csv) | Identificadores coletados para consulta das páginas individuais. |
| [csv/info_animes.csv](csv/info_animes.csv) | 4.150 registros com identificador, título, atributos e nota geral. |
| [csv/database_animes.csv](csv/database_animes.csv) | Matriz processada com 4.148 títulos, três colunas de identificação e nota, e 73 atributos binários. |
| [csv/output.csv](csv/output.csv) | Arquivo de resultados, sobrescrito a cada cálculo de similaridade. |

O pré-processamento remove registros com valores ausentes e transforma os atributos em indicadores de presença ou ausência. A nota geral da base é exibida ao usuário e utilizada como segundo critério de ordenação; as notas informadas pelo usuário ponderam o cálculo da recomendação.

## Como a recomendação funciona

1. O usuário pesquisa títulos, adiciona seus IDs à seleção e atribui notas de 0 a 10.
2. Cada título é representado por um vetor binário de atributos: `1` indica presença e `0`, ausência.
3. Para cada candidato, o sistema calcula a similaridade de Jaccard em relação a cada título selecionado.
4. As similaridades são combinadas por uma média ponderada pelas notas do usuário.
5. Os títulos já selecionados são excluídos dos candidatos. O ranking é ordenado pela similaridade ponderada e, em seguida, pela nota geral, ambas em ordem decrescente.

### Similaridade de Jaccard

Para os conjuntos de atributos de dois títulos, a similaridade é a razão entre a quantidade de atributos em comum e a quantidade de atributos presentes em pelo menos um deles:

$$
J(A, B) = \frac{|A \cap B|}{|A \cup B|}
$$

Por exemplo, um título com `{Aventura, Romance}` e outro com `{Aventura, Comédia}` têm similaridade de `1/3`. A ausência conjunta de um atributo não aumenta a similaridade.

### Combinação das preferências

Para um candidato $x$, os títulos selecionados $u_1, \ldots, u_k$ e suas notas $n_1, \ldots, n_k$:

$$
S(x) = \frac{\sum_{i=1}^{k} J(x, u_i)\,n_i}{\sum_{i=1}^{k} n_i}
$$

Uma nota maior dá mais peso às características daquele título. O código arredonda o resultado para duas casas decimais antes de ordenar o ranking.

## Funcionalidades

- Pesquisa de títulos no catálogo.
- Inclusão e remoção de títulos por ID, com notas individuais.
- Cálculo de similaridade a partir da seleção do usuário.
- Exibição do título, da nota geral e da similaridade ponderada.
- Ajuste da quantidade exibida, de 1 a 100 recomendações.
- Exportação automática do ranking para CSV.

**Ferramentas:** Python, Pandas, NumPy, Streamlit, Requests, Beautiful Soup e Pillow.

## Como executar

O ambiente original utiliza Python 3.10, e o [requirements.txt](requirements.txt) fixa as versões das bibliotecas. Para reproduzir essa configuração, utilize um interpretador Python 3.10 e execute os comandos abaixo a partir da raiz do repositório:

```powershell
cd similarity_anime_recommendation_system
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m streamlit run run.py
```

O comando `python` deve apontar para a versão escolhida. Mantenha o diretório de trabalho nesta pasta: os caminhos em `constants.py` são relativos a ela. A atualização das dependências para versões diferentes das fixadas exige uma verificação de compatibilidade.

Na aplicação:

1. Clique em **Iniciar** e pesquise um título.
2. Informe seu ID, atribua uma nota e clique em **Adicionar**.
3. Repita para outros títulos e clique em **Calcular similaridade**.
4. Ajuste a quantidade de resultados exibidos.

Utilize pelo menos um título presente na matriz processada e uma soma de notas maior que zero, pois essa soma é o denominador da média ponderada.

## Coleta e preparação da base

A classe `ScrapingAnimes`, em [get_animes_data.py](get_animes_data.py), organiza o processo em três métodos:

| Método | Responsabilidade |
| --- | --- |
| `get_animes_id()` | Coletar identificadores nas páginas do ranking de animes de TV. |
| `get_animes_info()` | Consultar as páginas individuais e extrair título, atributos e nota geral. |
| `database_preprocessing()` | Remover registros incompletos e gerar a matriz binária. |

Esses métodos gravam os CSVs correspondentes e dependem da estrutura das páginas no momento da coleta. A aplicação pode ser utilizada com os arquivos existentes, sem executar novamente a coleta.

## Estrutura da implementação

| Arquivo | Responsabilidade |
| --- | --- |
| [run.py](run.py) | Carregar os dados e iniciar a aplicação. |
| [interface.py](interface.py) | Gerenciar a interface e a seleção do usuário. |
| [processing.py](processing.py) | Preparar a exibição, calcular Jaccard e gerar o ranking. |
| [get_animes_data.py](get_animes_data.py) | Implementar a coleta e o pré-processamento da base. |
| [constants.py](constants.py) | Centralizar os caminhos dos arquivos. |
| [requirements.txt](requirements.txt) | Registrar as versões das dependências. |

## Limitações e próximos passos

O sistema considera apenas os atributos binários disponíveis; ele não incorpora sinopses, comportamento de outros usuários ou contexto de consumo. O ranking não foi avaliado com métricas de relevância ou testes com usuários.

A lista exibida para seleção contém dois registros a mais que a matriz processada. Seleções ausentes dessa matriz, seleções vazias ou notas com soma zero podem resultar em uma tabela vazia, pois a interface trata falhas de cálculo sem detalhar a causa.

Como continuidade, seria possível alinhar o catálogo de seleção à matriz processada, melhorar as validações e mensagens, avaliar a qualidade das recomendações e otimizar o cálculo de similaridade para bases maiores.
