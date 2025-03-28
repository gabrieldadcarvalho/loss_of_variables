# Conceito

De acordo com *Paul L. Mayer*:
> "Uma função $X$, que associa a cada elemento $s \in S$ um número real, $X(s)$, é denominada *variável aleatória*."

Portanto, podemos dizer que $X$ é uma variável que pode set analisada ao longo do tempo e, para cada elemento $s$ do domínio, que pertence ao espaço amostral $S$, há uma imagem correspondente $X(s)$.

Com isso, podemos definir algumas propriedades da variável aleatória.

## Função De Densidade De Probabilidade

A função de densidade de probabilidade $f(x)$ é dada por:

$$
f(x) = \lim_{ \nabla x  \to 0 } \frac{P(x \leq X < x +\nabla x )}{\nabla x}, \quad X > 0
$$

Analisando a expressão de $f(x)$, podemos dizer que ela representa o limit da probabilidade da variável $X$ assumir um valor entre $x$ e $x+\nabla x$, à medida que $\nabla x$ se aproxima de zero. Entretanto, a função de densidade de probabilidade captura uma "massa" de probabilidade dentro de um intervalo infinitesimal.


**"E se somarmos todas essas massas de probabilidade de $x$ até o infinito?"**

## Função De Distribuição Acumulada

A função de distribuição acumulada $F(x)$ pode set expressa como:

$$
F(x) = P(X \leq x)=\int_{0}^{x} f(x)dx
$$

Como o nome sugere, a função de distribuição acumulada informa a probabilidade de a variável $X$ assumir valores no intervalo $[0, x)$. Podemos interpretar essa probabilidade como uma soma de probabilidades menores:

**"X pode ser isso, ou isso, ou isso…"**

Se assumirmos que $X \in \mathbb{Z}^+$, temos: 

### Caso Discreto
$$
F(x) = P(X = 0) + P(X = 1) + P(X = 2) + P(X = 3) + \dots + P(X=x) = \sum_{i=0}^{x}P(X=i)
$$

Para variáveis contínuas, a função de distribuição acumulada é obtida pela integração da função de densidade $f(x)$.


### Caso Contínuo
$$
F(x) = \int_{0}^{x}f(x)dx
$$

## Função De Sobrevivência

A função de sobrevivência nos informa a probabilidade de a variável $X$ set maior ou igual a um determinado valor:

$$
S(x) = P(X \geq x) = \int_{x}^{\infty} f(x)dx = 1 - P(X\leq x) = 1-F(x) = 1 - \int_{0}^{x} f(x)dx
$$

Ou seja, $S(x)$ é o complemento da função de distribuição acumulada $F(x)$.

Sendo $X \sim N(0,1)$:

![[grafico_fdp_fda.png]]

## Taxa De Risco Ou Força De Mortalidade

Para definir a taxa de risco $h(x)$, primeiro vamos pensar da seguinte maneira:

Estamos interessados em observar a probabilidade da variável $X$ assumir valores dentro do intervalo $[x, x+\nabla x)$, sabendo que $X \geq x$. Dessa forma, temos a seguinte expressão:

$$
P(x\leq X<x+\nabla x \mid X\geq x)
$$

Agora, queremos calcular a taxa com que a variável $X$ assume valores dentro de $[x, x+\nabla x)$, dado que $X$ não assumiu valores menores que $x$. Para obter essa taxa, dividimos a probabilidade pelo tamanho do intervalo $\nabla x$:

$$
\frac{P(x\leq X<x+\nabla x \mid X\geq x)}{\nabla x}
$$

Tomando o limit quando $\nabla x$ tende a zero, obtemos:

$$
h(x) = \lim_{ \nabla x \to 0 } \frac{P(x\leq X<x+\nabla x \mid X\geq x)}{\nabla x}
$$

Utilizando a definição de probabilidade condicional:

$$
h(x) = \lim_{ \nabla x \to 0 } \frac{P(x\leq X<x+\nabla x) \cap P(X\geq x)}{P(X\geq x)\nabla x}
$$

Como $P(X\geq x)$ é justamente a função de sobrevivência $S(x)$, podemos reescrever:

$$
h(x) = \lim_{ \nabla x \to 0 }\frac{P(x\leq X<x+\nabla x)}{S(x)\nabla x}
$$

Também vimos anteriormente que a "massa" de probabilidade dentro de um intervalo infinitessimal é dada pela função de densidade, teremos:

$$
h(x) = \frac{f(x)}{S(x)}
$$

Portanto, em termos de análise de sobrevivência, podemos interpretar $h(x)$ como a **taxa instantânea de falha** da variável $X$, ou seja, a probabilidade de falha imediatamente após atingir o valor $x$. Essa taxa mede o **ritmo de ocorrência das falhas** ao longo do tempo.

## Valor Esperado

O valor esperado de uma variável $X$ representa o valor médio que se obteria ao longo de infinitas repetições do experimento.

Por exemplo, se lançarmos dois dados 10.000 vezes, qual seria o valor mais provável da soma?

As possíveis somas são:

| D(1) / D(2) | **1** | **2** | **3** | **4** | **5** | **6** |
|-------------|------|------|------|------|------|------|
| **1**       | 2    | 3    | 4    | 5    | 6    | 7    |
| **2**       | 3    | 4    | 5    | 6    | 7    | 8    |
| **3**       | 4    | 5    | 6    | 7    | 8    | 9    |
| **4**       | 5    | 6    | 7    | 8    | 9    | 10   |
| **5**       | 6    | 7    | 8    | 9    | 10   | 11   |
| **6**       | 7    | 8    | 9    | 10   | 11   | 12   |


Como há $6 \times 6 = 36$) combinações possíveis, observamos que o valor $7$ aparece com maior frequência. Assim, faz sentido apostar nele como o valor com maior probabilidade de ocorrência.


**"E se tivermos uma variável com muitos valores possíveis e não conseguirmos observar diretamente essa tendência?**


Podemos calcular a **média**. Voltando ao exemplo dos dados:

### Caso Discreto
$$
E[X] = \sum_{x = 2}^{12} x P(X=x)
$$

Código para calcular o valor esperado:

```python
# Definição das faces dos dados
dado1 = [x for x in range(1, 7)]
dado2 = [x for x in range(1, 7)]
somaDado = []

# Somando todas as 36 combinações possíveis
for d1 in dado1:
    for d2 in dado2:
        somaDado.append(d1 + d2)

Ex = 0
n = len(somaDado)

# Calculando a probabilidade de cada soma
for x in set(somaDado):
    freq_x = somaDado.count(x)
    prob_x = freq_x / n
    Ex += x * prob_x

print(f"Valor esperado E[X]: {Ex:.0f}") # A saída será E(X) = 7.
```

**"Se jogarmos infinitas vezes, a soma dos dois dados realmente converge para 7?**

Podemos verificar isso com um gráfico:

```python
# Importando bibliotecas
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

n = 10000  # Número de simulações
dado1 = np.random.randint(1, 7, size=n)  
dado2 = np.random.randint(1, 7, size=n)  
somaDado = dado1 + dado2  

# Contando as frequências das somas
freq_x = pd.Series(somaDado).value_counts().sort_index()  

# Gerando o gráfico
fig = plt.figure(figsize=(10, 6))
plt.bar(freq_x.index, freq_x.values, color="blue", edgecolor="black")
plt.xlabel("Soma dos Dados")
plt.ylabel("Frequência")
plt.title("Distribuição das Somas dos Lançamentos")
plt.grid(axis="y", linestyle="--", alpha=0.7)
plt.show()
```

![[distribution_sum_dice.png]]

### Caso Contínuo

Como vimos que a soma das probabilidades contínuas é dada pela $F(x)$ e utilizamos a integral da $f(x)$ para encontra-la, agora só precisamos multiplicar o valor de $x$ e sua respectiva probabilidade, portanto a média vai set dada por

$$
E[X] = \int_{-\infty}^{+\infty}xf(x)dx 
$$