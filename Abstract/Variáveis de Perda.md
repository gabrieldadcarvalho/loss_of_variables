Em ciências atuariais, muitas vezes estamos interessados em modelar uma variável aleatória $X$ que representa **perdas financeiras**, como os prejuízos de uma seguradora decorrentes de sinistros. Essa variável pode expressar perdas de diferentes naturezas, como custos com indenizações, despesas médicas ou danos materiais.

# Variável Excesso De Perda

Dado um valor $d$ tendo que $P(X > d)>0$, a variável $Y^p=x-d$, dado que $x>d$, vai ser definida como a **variável excedente de perda**.

## Com Censura a Esquerda

Uma forma comum de analisar perdas dentro do setor de seguros é utilizando a **variável excesso de perda com censura a esquerda**, definida como:

$$
Y^p =
\begin{cases} 
0, & \text{se } X < d \\ 
X - d, & \text{se } X > d 
\end{cases}
$$

Essa variável indica o **excesso de perda** em relação a um limite estabelecido $d$. Em termos atuariais, $d$ pode representar, por exemplo, uma **franquia** ou um **limite de cobertura**. Assim, só há uma perda real para a seguradora quando $X$ ultrapassa $d$, pois, nesse caso, a seguradora precisa arcar com a diferença $X - d$.

## Com Limite ou Censura a Direita

A variável de perda limitada, é dada por:

$$
Y_P
\begin{cases}
x, & \text{se} & x<u \\
u, & \text{se} & x\geq u 
\end{cases}
$$

Nesse tipo de perda, podemos ver que o valor da perda vai estar limitada em $u$.

## Esperança Da Variável Excesso De Perda

Se estivermos analisando uma seguradora com múltiplas apólices que seguem esse modelo de pagamento de benefícios, podemos calcular o **valor médio esperado da perda excedente**, dado por:

$$
E[Y^p] = E[X - d \mid X > d]
$$

Essa quantidade recebe diferentes denominações, como:
- **Função excesso de perda média**
- **Função de vida residual média**
- **Função expectativa de sobrevida**

Podemos reescrever essa expectativa usando a definição de probabilidade condicional:

$$
E[X - d \mid X > d] = \frac{E[(X-d) \cap P(X> d)]}{P(X> d)}
$$

Sabemos que $P(X \geq d)$ é dado pela função de sobrevivência $S(d)$ [[Variáveis Aleatórias#Função De Sobrevivência]], então podemos reescrever:

$$
E[Y^p] = \frac{E[X-d]}{S(d)}
$$

Além disso, a esperança da variável $X$ é dada pela soma de todos os seus valores possíveis [[Variáveis Aleatórias#Valor Esperado]]. Como estamos considerando apenas valores maiores que $d$, a soma ou a integral será feita a partir de $d$.

## Caso Discreto

No caso de uma variável discreta, a expectativa da variável excesso de perda é calculada como:

$$
E[Y^p] = \frac{\sum_{x_{i}>d} (x_{i} - d) P(X = x_i)}{S(d)}
$$

## Caso Contínuo

Para uma variável contínua, a esperança é dada por:

$$
E[Y^p] = \frac{\int_{d}^{+\infty} (x - d) f(x)dx}{S(d)}
$$

Dessa forma, conseguimos avaliar o impacto das perdas acima do limite estabelecido e calcular a expectativa de valores excedentes, o que auxilia na precificação de seguros e na modelagem do risco.

## Precificação de Seguro

Agora que já sabemos calcular a média de uma variável de perda, podemos modelar o seguinte problema:

Sabendo que os sinistros que ocorrem na janela de um ano segue uma distribuição de $poisson(\lambda)$. Tendo $x_i$ a perda associada ao cliente $i$, sendo iid. Portanto, pode-se calcular a perda agregada como:
$$
S = \sum_{i}^{n}x_{i}
$$
Sendo:
$S\to$ Perda Agregada
$n\to$ Nº Total de Sinistro da Carteira
$x_{i}\to$ Valor do beneficio do segurado $i$

Agora precisamos definir qual é o preço que devemos ter em caixa para obter uma solvência de $(1-\alpha)\%$ dos sinistros totais.

$$
P(S>p) = \alpha
$$
Sendo:
$p\to$ Preço do Seguro

$$
P(\frac{S-E[S]}{\sqrt{var(S)}}> \frac{p-E[S]}{\sqrt{var(S)}}) 
$$

Utilizando a aproximação gaussiana, temos que:


$$
\frac{p-E[S]}{\sqrt{var(S)}} = Z_{1-\alpha}
$$
Sendo:
$Z_{1-\alpha}\to$ O quantil da N(0,1) com $(1-\alpha)$%

$$
p = E[S] + Z_{1-\alpha}*\sqrt{var(S)}
$$
