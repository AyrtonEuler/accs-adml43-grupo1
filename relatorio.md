# Relatório
## Primeira Semana - 04/06
### Estatística descritiva com distribuição dos dados, padrões e outliers
Gráficos de histograma de cada campo da base de dados

![](./histogramas.svg)

Matriz de correlação dos campos da base de dados
![](./correlation.svg)

Decidimos usar `CLASSI_FIN` como output para o nosso modelo
![image](https://github.com/matheuscardimdasilva/accs-adml43-grupo1/assets/742079/032ade07-4142-4a20-892e-6ca58dba8601)
Criamos um campo `DOENTE`. Se o campo `CLASSI_FIN` for algum destes números, seguindo o Dicionário de Dados do SINAN:
```
10-Dengue
11-Dengue comsinais de alarme
12-Dengue grave
13-Chikungunya
```
O campo `DOENTE` será 1. Caso contrário, o campo `DOENTE` será 0.

Usamos a técnica One Hot Encoding para converter dados categóricos em binários, com um campo para cada categoria. 
Por exemplo, ao invez de um campo `CS_SEXO` que possa ser `[F, M ou I]`, criamos três campos `CS_SEXO_F`,`CS_SEXO_M` e `CS_SEXO_I` todos sendo `[1 ou 0]` de acordo com o campo `CS_SEXO`

Removemos todas as linhas que tinham ou `CS_SEXO` ou `CLASSI_FIN` ausente. 


### Divisão dos conjuntos de treino, teste e validação
Utilizamos a função `train_test_split` da biblioteca Scikit-Learn para embaralhar o dataset e depois dividir-lo em dois, sendo 66.7% para treino, e 33.3% para teste, mantendo as proporções de estratificação do campo `DOENTE` afim de manter a mesma porcentagem de doentes em ambos o treino e o teste, já que o dataset é desbalanceado.


### Validação dos algoritmos com métricas de P, R e F1

Os algoritmos foram divididos entre os programadores juniores e seniôr. A atribuição ficou da seguinte forma:

- Marina: Árvore de Decisão;
- Felipe: Rede Neural;
- Pedro: Regressão Logistica;
- Matheus: KNN e Floresta Aleatória.
  
![image](https://github.com/matheuscardimdasilva/accs-adml43-grupo1/assets/742079/1609c641-658f-4e79-ab13-0167fd04b425)

#### Validação Regressão Logistica

O modelo foi testado com os hiperparametros pré-definidos que já estão no padrão dele. Porém, já foi possivel observar que é necessário aumentar o número máximo de interações.

![image](https://github.com/matheuscardimdasilva/accs-adml43-grupo1/assets/171699350/93049911-36fd-473a-ad10-32afba267d22)

O resultado ficou da seguinte forma:

![image](https://github.com/matheuscardimdasilva/accs-adml43-grupo1/assets/171699350/5ce4877c-8d3b-4734-8715-ec40b978bae0)

#### Validação Árvore de Decisão
```python
from sklearn.tree import DecisionTreeClassifier
clf = DecisionTreeClassifier(
    criterion = 'entropy',  # Critério de Divisão: Entropia
    max_depth = None,       # Profundidade Máxima: Sem limite inicial, ajustável com validação cruzada.
    min_samples_split = 2,  # Número Mínimo de Amostras para Divisão de um Nó: 2
    min_samples_leaf = 1,   # Número Mínimo de Amostras em um Nó Folha: 1
)
clf = clf.fit(X_train, y_train)
```
Com os hiperparâmetros pré-definidos nesta etapa inicial da árvore de decisão e após o conjunto de dados pré-processado e dividido em conjuntos de treino e teste, criamos uma baseline inicial para comparação futura com os hiperparâmetros otimizados:

![image](https://github.com/matheuscardimdasilva/accs-adml43-grupo1/assets/107217921/dbbab7fe-89b9-4205-86e9-cf501f8e756e)

Após o treinamento, foram feitas as previsões no conjunto de teste e avaliada a performance através da acurácia e relatório de classificação:

![Captura de tela 2024-06-18 112218](https://github.com/matheuscardimdasilva/accs-adml43-grupo1/assets/107217921/1010da9b-d669-458b-b7fb-01d53f4bc1f5)

![Captura de tela 2024-06-18 112315](https://github.com/matheuscardimdasilva/accs-adml43-grupo1/assets/107217921/1a5648a0-842f-40cb-9d8a-1f5f58a8300d)


### Deploy em um container e conexão com dados
Ainda não fizemos por não ter feito todos os modelos. **Perguntar se é só jogar o ipynb numa imagem do Docker**

---

## Segunda Semana - 11/06
### Dashboard de visualização dos dados

### Avaliação dos hiperparâmetros

### Monitoramento da performance do modelo

---

## Terceira Semana - 18/06
### Estatística descritiva com distribuição dos dados, padrões e outliers para o pré-processamento definidos
Mesma coisa que o da primeira semana. 

### Divisão dos conjuntos de treino, teste e validação
Mesma coisa que o da primeira semana.

### Validação dos algoritmos com métricas de P, R e F1

### Deploy em um container e conexão com dados; 


---

## Quarta Semana - 25/06
### Dashboard de visualização dos dados

### Avaliação dos hiperparâmetros e proposta de novos hiperparâmetros mais adequados aos dados
Para tunar os hiperparâmetros dos modelos, usamos a classe `HalvingGridSearchCV` da biblioteca Scikit-Learn, que basicamente faz um Grid Search porém com poucos dados no inicio, descarta os modelos mais fracos, depois treina novamente os modelos restantes com o dobro de dados, até chegar no dataset total. Utilizamos Stratified Cross Validation, com K = 3, por ser bem mais rápido e não apresentar muitas diferenças se comparado com K = 5 ou K = 10. 
Decidimos optimizar a métrica f1-score, já que o dataset é desbalanceado. 

#### K-Nearest Neighbors (KNN)

Parâmetros tunados:
```python
hyperparameters = {
    "n_neighbors" : [5,7,10,13,15,20],
    "weights": ['uniform', 'distance']
}
```
---

#### Árvore de Decisão
![](./ADML43_DecisionTreeClassifier_.svg)

Parâmetros tunados:
```python
hyperparameters = {
    'criterion' : ['gini', 'entropy', 'log_loss'],  # Critério de Divisão: Entropia
    'min_samples_split': [2,4,8,16],                # Número Mínimo de Amostras para Divisão de um Nó: 2
    'min_samples_leaf': [1,2,4,8,16,32,64,128],     # Número Mínimo de Amostras em um Nó Folha: 1
}
```

Melhores hiperparâmetros: 
```python
{'criterion': 'gini', 'min_samples_leaf': 32, 'min_samples_split': 16}
```
Melhor F1-score : 0.8865631871945879

|              | precision | recall | f1-score | support      |
|--------------|-----------|--------|----------|--------------|
| 0            | 0.93      | 0.94   | 0.93     | 131690       |
| 1            | 0.89      | 0.87   | 0.88     | 72980        |
| accuracy     |           |        | 0.91     | 204670       |
| macro avg    | 0.91      | 0.91   | 0.91     | 204670       |
| weighted avg | 0.92      | 0.92   | 0.92     | 204670       |

---

#### Rede Neural (Multilayer Perceptron - MLP)

Parâmetros tunados:
```python
hyperparameters = {
    'hidden_layer_sizes' : [(100, 100), (100,100,100), (100,100,100,100), (200,200), (300,300), (100,200,300), (400,400,400)],
    'criterion' : ['gini', 'entropy', 'log_loss'],  # Critério de Divisão: Entropia
    'n_estimators': [10,100,200,250,400,800],     # Número Mínimo de Amostras em um Nó Folha: 1
}
```
---

#### Logistic Regression (Regressão Logística)

Parâmetros tunados:
```python

hyperparameters = {
    "max_iter": [1000],
    "solver": ['newton-cg', 'lbfgs', 'liblinear', 'sag', 'saga'],
    "penalty":["l1","l2"]
}

```

![image](https://github.com/matheuscardimdasilva/accs-adml43-grupo1/assets/742079/a9bdb0d6-ce26-4638-86ce-313d7e43061a)

Melhores hiperparâmetros: 
```python
{'max_iter': 1000, 'penalty': 'l2', 'solver': 'saga'}
```
Melhor F1-score :0.8751328155228276

|              | precision | recall | f1-score | support      |
|--------------|-----------|--------|----------|--------------|
| 0            | 0.92      | 0.93   | 0.93     | 131690       |
| 1            | 0.88      | 0.86   | 0.87     | 72980        |
| accuracy     |           |        | 0.91     | 204670       |
| macro avg    | 0.90      | 0.90   | 0.90     | 204670       |
| weighted avg | 0.91      | 0.91   | 0.91     | 204670       |

---

#### Random Forest (Floresta Aleatória)

Parâmetros tunados:
```python
hyperparameters = {
    'criterion' : ['gini', 'entropy', 'log_loss'],  # Critério de Divisão: Entropia
    'n_estimators': [10,100,200,250,400,800],     # Número Mínimo de Amostras em um Nó Folha: 1
}
```

### Monitoramento de desempenho do modelo


---

