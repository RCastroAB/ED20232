# Gabarito da Prova 1 de Estrutura de Dados 2023/2

## Questão 1

### Avalie as afirmações a seguir como verdadeiro ou falso, e justifique

#### a) A ordem de complexidade da função $n^3 + 3n^2$ é $O(n^3)$

Verdadeiro. Seguindo a definição da complexidade O-grande:

Basta verificar que $n^3 + 3n^2 \leq cn^3$ para $n > n'$ suficientemente grande. Dividindo os dois lados da função por $n^3$ teremos $1 + \frac{3}{n} \leq c$ e 
escolhendo arbitrariamente $n' = 1$ teremos um valor possível $c=4$ que satisfaz a equação.

#### b) A ordem de complexidade da relação de recorrência $T(n) = 3T(\frac{n}{2}) + O(n)$ é $O(n^2)$

Falso. Aplicando o teorema mestre teremos que comparar as funções $n^{\log_{2}{3}}$ e $O(n)$ e teremos que a primeira domina a segunda. Portanto teremos que a complexidade
é $O(n^{\log_{2}{3}})$.




####
