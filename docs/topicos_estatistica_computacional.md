# Tópicos em Estatística Computacional

## Geração de Números Pseudo-Aleatórios

O conteúdo para esse tópico entra-se em PDF e poderá ser acessado [**aqui**](files/computacional.pdf). Em um futuro próximo, essa seção será reescrita e fará parte do corpo deste HTML.


### Método da Aceitação e Rejeição

Em situações em que não podemos fazer uso do método da inversão (impossível obter a função quantílica) e nem conhecemos uma transformação que envolve uma variável aleatória ao qual sebemos gerar observações, poderemos fazer uso do **método a aceitação e rejeição**.

Suponha que $X$ e $Y$ são variáveis aleatórias com função densidade de probabilidade (fdp) ou função de probabilidade (fp) $f$ e $g$, respectivamente. Além disso, suponha que existe uma constante $c$ de tal forma que

$$\frac{f(t)}{g(t)} \leq c,$$
para todo valor de $t$, com $f(t) > 0$. Para utilizar o método a aceitação e rejeição para gerar observações da v.a. $X$, utilizando o algoritmo mais abaixo, antes, encontre uma v.a. $Y$ com pdf ou fp $g$, tal que satisfaça a condição acima.

**Importante**:

\BeginKnitrBlock{rmdimportant}<div class="rmdimportant"><div class=text-justify>
É importante que a v.a. $Y$ escolhida seja de tal forma que você consiga gerar facilmente suas observações. Isso se deve ao fato do método da aceitação e rejeição ser computacionalmente mais intensivo que métodos mais diretos como o método da transformação ou o método da inversão que exige apenas a regração de números pseudo-aleatórios com distribuição uniforme.
</div></div>\EndKnitrBlock{rmdimportant}

**Algoritmo do Método da Aceitação e Rejeição**:

1 - Gere uma observação $y$ proveniente de uma v.a. $Y$ com fdp/fp $g$;
  
2 - Gere uma observação $u$ de uma v.a. $\mathcal{U} \sim U(0, 1)$;
  
3 - Se $u < \frac{f(y)}{cg(y)}$ aceite $x = y$; caso contrário rejeite $y$ como observação da v.a. $X$ e volte para o passo anterior.
 
**Prova**: Consideremos o caso discreto, ou seja, que $X$ e $Y$ são v.a.s com fp's $f$ e $g$, respectivamente. Pelo passo 3 do algoritmo acima, temos que $\{aceitar\} =  \{x = y\} = u < \frac{f(y)}{cg(y)}$. Isto é, 

$$P(aceitar | Y = y) = \frac{P(aceitar \cap \{Y = y\})}{g(y)} = \frac{P(U \leq f(y)/cg(y)) \times g(y)}{g(y)} = \frac{f(y)}{cg(y)}.$$
Daí, pelo [**Teorema da Probabilidade Total**](https://pt.wikipedia.org/wiki/Lei_da_probabilidade_total), temos que:

$$P(aceitar) = \sum_y P(aceitar|Y=y)\times P(Y=y) = \sum_y \frac{f(y)}{cg(y)}\times g(y) = \frac{1}{c}.$$
Portanto, pelo método da aceitação e rejeição aceitamos ocorrência de $Y$ como sendo uma ocorrência de $X$ com probabilidade $1/c$. Além disso, pelo Teorema de Bayes, temos que

$$P(Y = y | aceitar) = \frac{P(aceitar|Y = y)\times g(y)}{P(aceitar)} = \frac{[f(y)/cg(y)] \times g(y)}{1/c} = f(y).$$
O resultado logo acima, mostra que aceitar $x = y$ pelo procedimento do algoritmo equivale a aceitar um valor proveniente de $X$ que tem fp $f$. Para o caso contínuo, a demonstração é similar.

**Importante**:

\BeginKnitrBlock{rmdimportant}<div class="rmdimportant"><div class=text-justify>
Perceba que para reduzir o custo computacional do método, deveremos escolher $c$ de tal forma que possamos maximizar $P(aceitar)$. Sendo assim, escolher um valor exageradamente grande da constante $c$ irá reduzir a probabilidade de aceitar uma observação de $Y$ como sendo observação da v.a. $X$.
</div></div>\EndKnitrBlock{rmdimportant}
      
**Nota**:

\BeginKnitrBlock{rmdnote}<div class="rmdnote"><div class=text-justify>
Computacionalmente, é conveniente considerar $Y$ como sendo uma v.a. com distribuição uniforme no suporte de $f$, uma vez que gerar observações de uma distribuição uniforme é algo simples em qualquer computador. Para o caso discreto, considerar $Y$ com distribuição uniforme discreta poderá ser uma boa alternativa.
</div></div>\EndKnitrBlock{rmdnote}
         
## Exercício {-}

1. Quais as propriedades de um bom gerador de números pseudo-aleatórios? Disserte sobre cada uma delas.

2. Implemente o gerador **Midsquare** idealizado pelo matemático John Von Neumann. Por que o gerador **Midsquare** não é um bom gerador? Explique.  

3. Defina matematicamente o gerador congruencial linear. Implemente uma função em R que implementa esse gerador.

4. O gerador **Randu** é definido por $x_{i + 1} = 65539 \times x_i\,\mathrm{mod}\,31$. O **Randu** é um gerador congruencial misto ou multiplicativo? 

5. Por que o gerador **Randu** é um dos peiores geradores de números pseudo-aleatório já criado? Explique.

6. Defina um gerador congruencial de período completo para geração de números pseudo-aleatórios com distribuição uniforme no intervalo $(0,1)$

7. Explique o método da transformação para geração de números pseudo aleatório. Apresente um exemplo.

8. Defina o método da inversão para geração de números pseudo-aleatórios. Sempre será possível utilizar esse método? Explique.

9. Implemente uma função para geração de números pseudo-aleatórios com distribuição normal padrão. A função deverá implementar o método de Box-Müller e o método polar. Ao final obtenha um histograma com os números gerados (mil valores) e realize um teste de normalidade. Realize um teste de normalidade.

10. Seja $X$ uma variável aleatória em um espaço de probabilidade $(\Omega, \mathcal{A},\mathcal{P})$ e suponha que $X \sim \mathcal{U}(0,1)$. Obtenha a distribuição de $Y = -\log(X)$.

11. Com base na distribuição da variável aleatória (v.a.) $Y$ do exercício acima, implemente uma função em R que gere observações de $Y$.

12. Conhecendo a distribuição da v.a. $X$, implemente para cada um dos itens que seguem, uma função para geração de observações da v.a. $Y$:

    * $X \sim \mathrm{Exp}(\lambda),$ com $x \geq 0$ e $\lambda > 0$ e  $Y = \sum_{i = 1}^n X_i \sim \Gamma(n, \lambda)$;
   
    * $X \sim \mathrm{Exp}(\lambda)$, com $x \geq 0$ e $\lambda>0$ e $Y = \mu - \beta\log(\lambda X) \sim \mathrm{Gumbel}(\mu,\beta)$, com $\mu \in \Bbb{R}$ e $\beta>0$;
   
    * $X \sim \mathcal{U}(0,1)$ (contínua) e $Y = m + s[-\log(X)]^{-1/\alpha} \sim$ Fréchet$(\alpha,s,m)$, com $x, \alpha,s > 0$ e $m \in  \Bbb{R}$. 
    
13. Cite algumas das propriedades do gerador **Mersenne Twister**. Qual o seu período de ocorrência?

14. Explique o algoritmo do método da aceitação e rejeição.

15. Utilizando o método da aceitação e rejeição, implemente uma função que gere valores aleatório provenientes da distribuição da v.a. $X$ tal que

$$P(X = 1) = 0.3, P(X = 2) = 0.2, P(X = 3) = 0.35, P(X = 4) = 0.15.$$

16. Implemente uma função que gera observações da v.a. $X$, tal que:

\begin{eqnarray}
P(X = 0) &=& 0.01, P(X = 1) = 0.04, P(X = 2) = 0.12,\nonumber\\
P(X = 3) &=& 0.27, P(X = 4) = 0.44, P(X = 5) = 0.62, \nonumber\\
P(X = 6) &=& 0.76, P(X = 7) = 0.87, P(X = 8) = 0.93, \nonumber\\
P(X = 9) &=& 0.97, P(X = 10) = 0.99, P(X = 11) = 0.99, \nonumber\\ 
P(X = 12) &=& 1.\nonumber
\end{eqnarray}


17. Implemente uma função para o método da aceitação e rejeição (`ar_fp(n, x, prob)`), para o caso em que deseja-se gerar observações de uma v.a. $X$ discreta. O argumento `n` refere-se à quantidade de observações a serem geradas, `x` é um vetor de valores assumidos por $X$ e `prob` é um vetor de probabilidades de cada observação de $X$. A função `ar_fp(n, x, prob)` deverá escolher um valor adequado para $c$.

18. Seja $X$ uma v.a. contínua com fdp $f(x) = 6x(x-1)$, com $0 < x < 1$. Implemente a função `rf(n, c = 0.5)` que gera números pseudo-aleatórios como observações de $X$, pelo método da aceitação e rejeição, em que `n` é a quantidade de números a serem gerados e `c` é o valor da constante (0.5 por padrão) no algoritmo do método da aceitação e rejeição. **Dica**: considere $Y \sim U(0,1)$.

19. Considerando a função `rf(n, c)` implementada no exercício anterior, quantos passos serão necessários para que possamos gerar 10 mil observações proveniente da distribuição de $X$, considerando `c = 6`? Respectivamente, quantos passos serão necessários para serem gerados a mesma quantidade de observações de $X$ considerando `c = 0.5`? **Dica**: antes de chamar a função implementada, fixe a semente fazendo `set.seed(0)`.

