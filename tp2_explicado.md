# Explicação TP2

## Introdução: Coloração Gulosa

A sua entrada nesse trabalho é um grafo que já vem colorido por vértices, o que significa que cada vértice tem uma "cor" nesse caso representada por um número. 

Você pode inclusive tomar como pressuposto que essa coloração é uma coloração própria, ou seja, que nunca existem dois vértices vizinhos com a mesma cor.

O seu objetivo nesse trabalho é verificar se a coloração é gulosa. Uma coloração gulosa é qualquer coloração que possa ser gerada por um algoritmo guloso. O como ele funciona é que ele escolhe uma ordem arbitrária para iterar sobre todos os nós do grafo e colore sempre cada vértice com a menor "cor" disponível para aquele vértice.

Por exemplo, se você está colorindo um vértice que já tem vizinhos com a cor 1, 2 e 3, ele necessariamente será colorido com a cor 4.

Esse algoritmo não é ótimo (ele não colore sempre usando o menor número de cores distintas possível), mas é bastante eficiente.

## Verificação

Mas a sua função não é colorir em si, mas determinar se a coloração foi ou não feita por um algoritimo assim. Para determinar isso, você tem que verificar uma propriedade simples, onde **para todo vértice, você tem que checar se ele tem uma cor que não seja a menor disponível para ele.**

Por exemplo, se você encontrar um vértice com a cor 4, ele precisa necessariamente ter vizinhos com as cores 1, 2 e 3. Caso essa propriedade seja verificada para todos os vértices, a coloração é gulosa. Caso algum vértice não satisfaça essa propriedade, ela não é gulosa.


## Gerando a permutação geradora: Ordenação


Já a questão da ordenação entra na segunda etapa. Como o algoritmo guloso é determinístico, ele sempre vai gerar a mesma coloração dado que a ordem da execução seja a mesma. Por outro lado várias ordenações diferentes podem gerar a mesma coloração.

Como a saída do seu programa deve gerar a ordem de execução "canonica" que gera aquela coloração, é aí que entra a ordenação.

Considerando que o algoritmo sempre seleciona a menor cor possível para cada vértice, então se você recolorir o grafo seguindo a ordem da menor cor até a maior cor da coloração antiga, você terá exatamente a mesma coloração sempre.

> Como "prova" intuitiva, tente imaginar se seria possível atribuir uma cor menor que a antiga para um vértice considerando que todos os vértices com cores menores já foram coloridos, ou uma cor maior considerando que seria impossível ele ter um vizinho com a mesma cor que ele tinha originalmente

Dessa forma, ordenando os vértices pelas suas cores, você vai ter sempre **alguma** ordenação que gera aquela coloração. 

## Permutação geradora única

Mas para garantir que seja a "canônica" (principalmente por motivos de avaliação automática por vpl), você também tem que garantir que os vértices ordenados por cor também estarão ordenados por rótulos quando suas cores forem iguais.

Por exemplo, se os vértices 1 e 4 ambos tem a cor 1, tanto [1,4] e [4,1] seriam ordenações *válidas* para o começo do seu resultado, mas apenas a primeira será aceita pela VPL.



Para garantir essa segunda "sub-ordenação," existem duas soluções.

### Ordenações Estáveis

A primeira seria modificar todos os algoritmos de ordenação não-estáveis para suas formas estáveis. Estabilidade se refere ao ato de manter a "sub-ordem" inicial de elementos que tem a mesma chave. 

Como o seu programa sempre recebe as cores por ordem dos rótulos, você pode intuitivamente observar que se a ordenação for estável, nunca vai acontecer de ter um vértice com mesma cor e rótulo maior que outro aparecendo antes.

Existem variantes estáveis para cada um dos algoritmos nesse TP na internet, não caberia aqui.

### Quebra de empates

O outro método é usar um desempate na comparação com rótulos. No caso quando você estiver comparando em qualquer algoritmo de ordenação qual vértice tem cor menor que o outro, você também vai ter que considerar o caso de "empate" onde os dois tenham a mesma cor.

Caso eles tenham a mesma cor, então o menor nessa comparação vai ser decidido por quem tem a menor cor. Por exemplo, se você tiver dois vértices com a cor 1 na comparação, você vai ter que olhar também os rótulos e ver que um é 2 e o outro é 4, então considerar o vértice 2 como o menor para efeitos da sua ordenação.


### Adendo: YouSort


Já o seu método de ordenação que você tem que desenvolver, a performance dele não é relevante contanto que ele esteja correto. Caso não tenha ideias, experimente misturar dois métodos de ordenação diferentes de acordo com tamanho do problema, ou assista um daqueles vídeos de "métodos de ordenação vizualizados" e veja se algum te interessa e implemente ele.
