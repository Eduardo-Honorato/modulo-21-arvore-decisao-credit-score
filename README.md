# Módulo 21: Projeto de Credit Score com Árvore de Decisão

Exercício do curso Profissão: Cientista de Dados (EBAC). Aplica uma árvore de decisão às bases de crédito tratadas no Módulo 17 para prever o score de cada cliente em três classes: Low (baixo), Average (médio) e High (alto), e compara o resultado com o Naive Bayes do [Módulo 20](https://github.com/Eduardo-Honorato/modulo-20-naive-bayes-credit-score).

[![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Eduardo-Honorato/modulo-21-arvore-decisao-credit-score/blob/main/Profissao_Cientista_de_Dados_M21_Pratique_resolvido.ipynb)

## Arquivos

| Arquivo | Conteúdo |
|---|---|
| `Profissao_Cientista_de_Dados_M21_Pratique_resolvido.ipynb` | Notebook com código, saídas, gráficos e interpretações |
| `X_treino.csv`, `y_treino.csv` | Base de treino, balanceada com oversampling (270 linhas) |
| `X_teste.csv`, `y_teste.csv` | Base de teste, com a distribuição original das classes (33 linhas) |

O score foi codificado no Módulo 17 como Low = 0, Average = 1 e High = 2.

## O que o notebook faz

1. Carrega e valida as quatro bases (linhas, variáveis, nulos, balanceamento e cópias entre treino e teste).
2. Explica o passo a passo de aplicação de uma árvore de decisão e como melhorá-la.
3. Treina a árvore com critério Gini e `random_state=0` e mede a acurácia no treino.
4. Avalia no teste com relatório de classificação e matriz de confusão e compara com o treino.
5. Plota a árvore e analisa profundidade e variáveis usadas.
6. Identifica as 2 principais variáveis e treina uma segunda árvore só com elas.
7. Compara a árvore com o Naive Bayes.
8. Exemplos gráficos interativos em React e Tailwind CSS (matriz de confusão, árvore, importância das variáveis e comparação de modelos).

## Resultados

| | Naive Bayes | Árvore (todas as variáveis) | Árvore (2 variáveis) |
|---|---|---|---|
| Acurácia no treino | 99,26% | 100% | 99,63% |
| Acurácia no teste | 96,97% | 93,94% | 93,94% |
| Recall macro no teste | 95,24% | 93,79% | 93,79% |

- A árvore completa tem profundidade 5, 7 folhas e 13 nós. A primeira divisão, `renda <= 38.750`, isola todos os clientes Low.
- As duas variáveis mais importantes são `renda` (53,2%) e `moradia_cod` (43,6%), que somam cerca de 96,7% da importância. A árvore treinada só com elas teve o mesmo desempenho no teste.
- O Naive Bayes teve resultados um pouco melhores no teste e menor distância entre treino e teste. A árvore tem a vantagem da interpretabilidade, com regras claras que podem ser explicadas ao cliente.

## Limitações

- **Teste pequeno:** são 33 clientes, com apenas 3 Low e 7 Average. Um único erro muda a acurácia em cerca de 3 pontos, e a diferença entre os modelos equivale a um cliente.
- **Teste não balanceado:** cerca de 70% dos clientes do teste são High.
- **Cópias entre treino e teste:** 12 dos 33 clientes do teste têm uma cópia idêntica no treino, porque as linhas duplicadas foram mantidas no Módulo 17. O resultado do teste é um pouco otimista.
- **Overfitting:** a árvore completa acerta 100% do treino e algumas folhas têm só 1 a 3 clientes. Limitar a profundidade, usar validação cruzada e remover duplicatas antes da divisão são melhorias possíveis.

## Como executar

O caminho mais simples é abrir no Google Colab pelo botão acima e enviar os quatro CSVs para o painel de arquivos. Para rodar localmente:

```bash
pip install pandas numpy seaborn matplotlib scikit-learn jupyter
jupyter notebook Profissao_Cientista_de_Dados_M21_Pratique_resolvido.ipynb
```

Mantenha os quatro CSVs na mesma pasta do notebook e execute as células na ordem, começando pela de imports. Os painéis interativos precisam de conexão com a internet, porque carregam React e Tailwind CSS por CDN. O GitHub mostra o notebook, mas não executa esses painéis.

## Tecnologias

Python, pandas, NumPy, seaborn, Matplotlib, scikit-learn, React e Tailwind CSS.
