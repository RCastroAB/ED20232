# Árvore AVL

A estrutura de dados Árvore Adelson-Velsky Landiis (AVL) é uma das primeiras estruturas que implementam uma **árvore balanceada de pesquisa**. 
Árvores balanceadas de pesquisa (ou auto-balanceantes) são relevantes por evitar o problema caminhos muito longos criados por inserções problemáticas.
No pior caso, uma árvore binária pode se tornar tão "degenerada" (ou seja, não parecendo uma árvore) que seja efetivamente uma lista, como vista na figura a seguir.


Nesses casos, teremos que embora o caso esperado de complexidade para busca binária em árvores seja $(log{n})$, a complexidade do pior caso irá se tornar $O(n)$, equivalente
a uma busca sequêncial. Como em muitas aplicações podemos ter listas de chaves com inserções e remoções arbitrárias (como por exemplo a lista de número de matrículas válidos),
precisamos de uma estrutura que mantenha todas as 3 operações a seguir eficientes:

* Busca por um elemento pela sua chave
* Inserção de uma chave em ordem
* Remoção de uma chave

É para isso que serve uma árvore balanceada de pesquisa. Existem várias árvores diferentes que em alguns casos são equivalentes, como a Rubro-Negra (Red-Black).

## Definição da AVL

A árvore AVL se baseia apenas em uma propriedade simples, onde para todo nó $v$, sendo $h_1$ e $h_2$ as alturas das subárvores a sua esquerda e direita respectivamente,

$$
|h_2 - h_1| \leq 1
$$

Para isso é utilizado um atalho, onde, ao invés de recomputar a altura para cada nó após toda inserção ou remoção, é armazenado um valor intermediário chamado 
Fator de Balanceamento ($FB$). Como $|h_2 - h_1| = |FB| \leq 1$, temos que os únicos valores válidos para $FB$ em todos os nós serão $\{-1, 0, 1\}$. Casos algum nó 
se encontre com valores fora desse intervalo, a árvore está desbalanceada e precisa ser "corrigida." Essas correções serão dadas utilizando um método chamado "rotação."

## Inserção

A Inserção em uma árvore AVL se dá inicialmente de forma idêntica a em uma árvore binária genérica. Iniciando da raíz, checa se o valor da chave a inserir é 
menor ou maior que a chave do nó examinado, e repete a função respectivatemente para o nó esquerdo ou direito. Esse processo se repete até que se alcance um espaço "vázio" 
onde a nova chave vai ser inserida.

```python
// Pseudocódigo
func Insere(Nó nó, int chave:
  if chave < nó.chave:
    if (no.esquerdo):
      Insere(nó.esquerdo, chave)
    else:
      Cria(nó.esquerdo, chave)

  else:
    if (nó.direito):
      Insere(nó.direito, chave)
    else:
      Cria(nó.esquerdo, chave)
```

### Desbalanceamento


Na segunda étapa é verificado se árvore se tornou desbalanceada, e caso sim, é corrigida. Primeiro os fatores de balanceamento terão que ser atualizados. Por padrão, 
como o novo nó é uma folha, seu FB será 0. Agora todo nó acima dele precisa ser atualizado de acordo com os fatores de balanceamento de seus filhos.

O nó imediatamente anterior ao nó inserido terá $\pm1$ adicionado ao seu FB, com o sinal definido pelo lado ao qual o novo vértice foi adicionado.
Caso o novo $FB$ agora seja zero, sabemos que não houve uma diferença na altura máxima, já que isso significa que a subárvore a partir desse nó se tornou 
balanceada, e podemos encerrar o algoritmo.

Caso esse novo $FB=\pm1$, sabemos que a altura dessa sub-árvore aumentou, e portanto, contiuamos propagando da mesma forma essa mudança pra cima da mesma forma ao 
parágrafo anterior.

Continuando esse procedimento eventualmente chegaremos à raíz com todos fatores de balanceamento válidos, no caso em que a árvore se manteve balanceada, ou propagaremos 
a mudança para algum nó que torne seu $FB=\pm2$. Nesse caso encontramos uma sub-árvore desbalanceada e precisamos rebalancear.

```python
// Pseudocódigo
func propaga(Nó nó, int lado): //lado = +/-1
  nó.FB += lado
  if nó.FB == 0:
    return
  else if nó.FB == +/-1:
    // houve mudança de altura, propaga
    if nó.chave < nó.pai.chave: //à esquerda
      propaga(nó.pai, -1)
    else: //à direita
      propaga(nó.pai, +1)

  else if nó.FB == +/-2:
    //REBALANCEAR

```


### Rebalanceamento

