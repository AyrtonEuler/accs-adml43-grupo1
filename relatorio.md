# Relatório
## Primeira Semana - 04/06
### Estatística descritiva com distribuição dos dados, padrões e outliers
Parte do describe e gerar boxplots, porém ainda não arrumamos 

![](./histogramas.svg)

![](./correlation.svg)


![image](https://github.com/matheuscardimdasilva/accs-adml43-grupo1/assets/742079/032ade07-4142-4a20-892e-6ca58dba8601)

### Divisão dos conjuntos de treino, teste e validação
![image](https://github.com/matheuscardimdasilva/accs-adml43-grupo1/assets/742079/145d32be-6a1b-4963-981f-6440c1f70418)

#### Divisão dos conjuntos de treino

Os algoritmos foram divididos entre os programadores juniores e seniôr. A atribuição ficou da seguinte forma:

- Marina: Árvore de Decisão;
- Felipe: Rede Neural;
- Pedro: Regressão Logistica;
- Matheus: KNN e Floresta Aleatória.


### Validação dos algoritmos com métricas de P, R e F1
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
