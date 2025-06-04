# Análise Preditiva de Sífilis Congênita em Pernambuco

Este repositório contém um projeto de Aprendizado de Máquina focado na análise e desenvolvimento de modelos preditivos para dados clínicos e sociodemográficos relacionados à Sífilis Congênita em Pernambuco, Brasil. O estudo utiliza dados do Programa Mãe Coruja Pernambucana (PMCP) no período de 2013 a 2021.

## Membros do projeto
- Ana Beatriz Alves ([@anabxalves](https://github.com/anabxalves))
- Caio Barreto de Albuquerque ([@Caiobadv](https://github.com/Caiobadv))
- Isabela Spinelli ([@bela975](https://github.com/bela975))
- Maria Luisa Arruda ([@MaluArr](https://github.com/MaluArr))
- Victor Hora Tenório ([@victorhorat](https://github.com/victorhorat))
## Estrutura do Repositório

- `av2ml.ipynb`: O notebook principal do Jupyter que contém todo o código para pré-processamento de dados, análise exploratória (EDA), treinamento de modelos de regressão e classificação, e avaliação dos resultados.
- `Atv2 - Aprendizado de Máquina - 2025.1.pdf`: O artigo científico que detalha a pesquisa, metodologia e resultados.
- `data_set.csv`: O conjunto de dados original utilizado no projeto, contendo 41.762 registros e 26 atributos clínicos e sociodemográficos.
- `LICENSE`: O arquivo de licença MIT.

## Sobre o Projeto

A sÍfilis congênita continua sendo um problema de saúde pública significativo. A detecção precoce é crucial, e este projeto explora o uso de técnicas de aprendizado de máquina para auxiliar nesse processo.

### Objetivos Principais:

1.  **Prever a idade (`AGE`)** das participantes utilizando técnicas de regressão. A idade é um indicador demográfico relevante para políticas públicas de prevenção.
2.  **Classificar os resultados do teste VDRL (`VDRL_RESULT`)** para sífilis congênita, focando na identificação de casos positivos. Casos positivos representam a classe minoritária no dataset, com aproximadamente 1,98% do total de registros.

## Fonte de Dados
A base deste estudo, incluindo o conjunto de dados, foi o artigo "Sífilis Congênita em Pernambuco: Uma Análise Preditiva de Dados Clínicos e Sociodemográficos (2013-2021)", disponível em: https://data.mendeley.com/datasets/3zkcvybvkz/1.  O data_set.csv é o conjunto de dados extraído diretamente dessa fonte.

## Conjunto de Dados

O dataset, intitulado "Clinical and sociodemographic data on congenital syphilis cases, Brazil, 2013-2021", abrange 41.762 registros e 26 atributos. Ele inclui informações clínicas e sociodemográficas sobre cuidados pré-natais, desfechos de gestantes e os resultados do teste VDRL de seus filhos, coletados em municípios pernambucanos atendidos pelo PMCP.

### Atributos Chave:

-   `VDRL_RESULT`: Variável alvo para classificação (Positivo: 0, Negativo: 1).
-   `AGE`: Variável alvo para regressão (idade das participantes).
-   `LEVEL_SCHOOLING`: Escolaridade, identificada como uma das *features* importantes para a predição do VDRL.
-   `MARITAL_STATUS`: Estado civil, também considerado um fator importante.
-   `FOOD_INSECURITY`: Grau de insegurança alimentar, outro atributo de destaque na análise de importância.
-   Outros atributos incluem informações sobre saúde, infraestrutura familiar e renda.

## Metodologia

O projeto seguiu as seguintes etapas:

1.  **Pré-processamento de Dados:**
    -   Carregamento e análise inicial para verificação de valores ausentes e *outliers*.
    -   Remoção de valores anômalos na variável `AGE` (ex: idades negativas).
    -   Tratamento de valores ausentes em atributos categóricos com a categoria "Não informado".
2.  **Análise Exploratória dos Dados (EDA):**
    -   Visualização da distribuição da idade (`AGE`), mostrando concentração de pacientes entre 20 e 30 anos.
    -   Análise da distribuição dos resultados do VDRL, revelando um severo desbalanceamento de classes (aprox. 1.98% de casos positivos).
    -   Criação de uma matriz de correlação, que indicou ausência de correlações fortes entre variáveis numéricas e as variáveis-alvo, sublinhando a importância de variáveis categóricas e modelos não-lineares.
3.  **Modelagem Preditiva:**
    -   **Regressão (Previsão de `AGE`):** Utilizado `RandomForestRegressor` em um pipeline com `StandardScaler` para atributos numéricos e `OneHotEncoder` para categóricos. A avaliação foi feita com MAE, MSE e RMSE.
    -   **Classificação (Classificação de `VDRL_RESULT`):** Empregado `DecisionTreeClassifier` e, para lidar com o desbalanceamento de classes, a técnica `SMOTEENN` foi aplicada aos dados de treinamento. As métricas de avaliação incluíram AUC-ROC, Precision, Recall e F1-Score, com foco na classe positiva.
4.  **Análise de Importância de Atributos:** Identificação dos fatores mais influentes para a predição do `VDRL_RESULT` pelo `DecisionTreeClassifier`.
5.  **Visualização da Árvore de Decisão:** Representação gráfica dos primeiros níveis da árvore de decisão para entender as regras de classificação.

## Resultados

### Regressão (Previsão de Idade)

-   **RMSE:** Aproximadamente 4.16. Isso sugere que o modelo consegue estimar a idade com um erro médio de cerca de 4 anos.

### Classificação (Resultado do VDRL)

-   **AUC-ROC:** ~0.5641 (com SMOTEENN). O valor próximo a 0.5 indica um desempenho similar a um classificador aleatório.
-   **Recall (Sensibilidade):** ~0.1659.O modelo identificou apenas cerca de 16.6% dos casos reais de sífilis.
-   **Precision:** ~0.0279. Quando o modelo previu sífilis, esteve correto em apenas aproximadamente 2.8% das vezes.
-   **Matriz de Confusão:** Demonstrou um número significativo de falsos negativos (1.230 casos), tornando o modelo inadequado para triagem clínica sensível. A aplicação de SMOTEENN não melhorou a AUC-ROC em relação ao modelo sem reamostragem.

### Importância dos Atributos para VDRL_RESUL

Os atributos mais importantes identificados foram:

-  `MARITAL_STATUS_1.0` (estado civil)
-  `FOOD_INSECURITY_2.0` (grau de insegurança alimentar)
-  `LEVEL_SCHOOLING` (escolaridade)

Esses resultados indicam que fatores socioeconômicos têm um papel relevante na identificação de risco para sífilis congênita.

## Conclusão

Embora o modelo de regressão para a previsão da idade tenha apresentado um desempenho satisfatório, o modelo de classificação para sífilis congênita foi limitado. A baixa capacidade de detecção da classe minoritária (sífilis congênita), mesmo com técnicas de reamostragem como SMOTEENN, ressalta o desafio em prever corretamente a sífilis congênita com os atributos e modelos atuais. Futuras investigações devem explorar variáveis mais informativas e modelos mais sofisticados.

## Como Executar o Projeto

1.  **Clone o repositório:**
    ```bash
    git clone https://github.com/seu-usuario/seu-repositorio.git
    cd seu-repositorio
    ```

2.  **Instale as dependências:**
    Recomenda-se usar um ambiente virtual.
    ```bash
    pip install pandas numpy scikit-learn matplotlib seaborn imblearn
    ```

3.  **Abra o notebook Jupyter:**
    ```bash
    jupyter notebook av2ml.ipynb
    ```
    Execute as células do notebook sequencialmente para reproduzir a análise e os resultados.

---
