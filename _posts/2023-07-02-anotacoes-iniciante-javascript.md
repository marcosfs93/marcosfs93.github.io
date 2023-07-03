---
title: Anotações para Iniciantes do Javascript
date: 2023-07-02
author: M4rQu1Nh0S
tags: [anotações, iniciante, javascript]
subtitle: Minhas anotações sobre as aulas do curso iniciante de Javascript
category: [Dicas e tutoriais]
comments: true
cover-img: https://cdn-images-1.medium.com/max/800/0*LxgduJ4mHazq-CZG.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*LxgduJ4mHazq-CZG.jpg
share-img: https://cdn-images-1.medium.com/max/800/0*LxgduJ4mHazq-CZG.jpg
layout: post
---
Recentemente, durante um vídeo que eu assisti no canal do [diolinux](https://www.youtube.com/channel/UCEf5U1dB5a2e2S-XUlnhxSA), eu acabei conhecendo o “[Curso de programação gratuito — JavaScript do Zero](https://www.betrybe.com/curso-de-programacao-javascript-do-zero)” da Trybe.

Esse curso trás muito conhecimento bacana sobre essa linguagem de programação, e obviamente muita coisa seria aprendida ali.

Já que muita coisa seria aprendida, eu tinha o receio de acabar esquecendo uma coisa ou outra, já que eu decidi fazer o curso apenas por curiosidade e também para ver como é o jeito de ensinar as coisas na Trybe.

A seguir trago umas anotações que eu guardei para eu mesmo, lembrando que são anotações apenas o que é diferente do conteúdo em sí.

**Conteúdo:**
- [Variaveis](#variaveis)
- [Uso do ponto e virgula](#uso-do-ponto-e-virgula)
- [Tipos primitivos](#tipos-primitivos)
- [Operadores de calculo/aritméticos](#operadores-de-calculoaritméticos)
- [Operadores lógicos](#operadores-lógicos)
- [Estrutura condicional if/else](#estrutura-condicional-ifelse)
- [Arrays](#arrays)
- [For](#for)

## Variaveis:

### **var** e **let**:

Essas variaveis podem ser alteradas.

**Como se usa mesmo?**

```javascript
let cor = 'azul';
// ou
var cor = 'azul';
```

Dá pra **mudar o seu valor**, exemplo:

```javascript
cor = 'verde'; // não precisa colocar let
```

### **const**:

**const** também é usado para criar variaveis, porem uma vez declaradas você não consegue alterar seu valor.

**Como se usa mesmo?**

```javascript
const nome = 'Marcos'; // valor permanente
```

### Uso do ponto e virgula

Quando você terminar uma linha de javascript, você é obrigado a colocar um ponto e virgula ( ; ) no final da linha, se não pode ocorrer erros no código.

## Tipos primitivos

Existem 3 tipos primitivos:

**string:** Podem conter palavras, numeros e simbolos, e toda string vai ser consideredo string **se estiver entre áspas** (‘ ’ ou “ ”).

**number:** Só pode conter numeros, não pode estar entre áspas porque quem deve usar aspas são strings.

**boolean:** Só pode ter dois valores: “**true”** ou “**false”**. todo boolean é considerado false até que seja declarado o valor true.

**null:** Só pode ter o valor “null”. Usado para criar variaveis com valor nulo ou que ainda não se tem um valor definido.

**undefined:** Variavel sem valor. Usado para criar variaveis vazias, que ainda vão receber um valor.

**Como se usa mesmo?**

```javascript
let strings = 'textos'; // usa aspas
let numeros = 2023; // só numeros, sem aspas
let boolean = true; // pode ter apenas 'true' ou 'false'
```

**A diferença de null e undefined:**

A variavel null é criado com o valor null, enquanto a variavel undefined é criada vazio, nem se quer tem valor, enquanto na variavel null ela já é criada com o valor null.

**Como se usa mesmo?**

```javascript
let variavel = null; // null - variavel criada já o valor null.
let indefinida // undefined - variavel criada sem valor.
```

## Operadores de calculo/aritméticos:

```javascript
let soma = 1 + 2; // sinal de +
let subtracao = 2 - 1; // sinal de -
let divisao = 2 / 1; // Usa "/"
let multiplicacao = 1 * 1; // Usa "*"

let expoente = 2 ** 2; // exponenciação, semelhante a 2², ou seja: 2x2
let expoente = 2 ** 3; // equivalente a 2³, ou seja: 2x2x2

let modulo = 2 % 2; // operações de módulo
let modulo = 7 % 3; // usados para encontrar o resto de uma divisão
let modulo = 5 % 3; // de um numero por outro.
```

## Operadores de comparação

-   `===` para comparar estritamente a igualdade entre dois valores;
-   `!==` para comparar estritamente a diferença entre dois valores;
-   `>` para comparar se um valor é maior do que o outro;
-   `<` para comparar se um valor é menor do que o outro;
-   `>=` para comparar se um valor é maior ou igual do que o outro;
-   `<=` para comparar se um valor é menor ou igual do que o outro.

## Operadores lógicos

Existem 3 operadores lógicos:

`&&` (AND) = Operador usado para comparar duas condições, somente vai ter valor TRUE se as duas condições forem cumpridas, outra combinações resultam em FALSE.

`||` (OR) = Operador usado para comparar duas condições, somente vai ter TRUE se pelo menos uma das condições forem cumpridas, outras combinações se resultam em FALSE.

`!` (NOT) = Operador usado para reverter o valor de um boolean

**Como se usa?**

```javascript
// Sem operador ! NOT
let interruptor = true; // criado uma boolean com valor TRUE, ligado
console.log(interruptor); // resultado será true

// Com operador ! NOT
console.log(!interruptor); // resultado será FALSE
```

Como viram, o operador ! é capaz de reverter um valor de boolean se na frente da váriavel se colocar uma exclamação na frente do nome da variavel.

## Estrutura condicional **if/else**

Usado em situações em que se algo não acontecer, então fará outra coisa.

**Como se usa?**

```javascript
let carroLigado = true;

if (carroLigado){
Então vai andar
}
else {
Vai ficar parado
}
```

### else if

Existe o **else if** que fica entre **if** e **else**. ele vai ser usado quando haver um terceiro comportamento ou mais.

**Como se usa?**

```javascript
let temCarro = false;
let temMoto = true;

if (temCarro) {
Vai de carro
}

else if (temMoto) {
Vai de moto
}

else {
Nem vai kkk
}
```

Nessa estrutura o codigo vai checar se você tem carro, se tiver, vai de carro mesmo.

Se não carro, o código vai checar se você tem pelo menos uma moto, se tiver, vai de moto. se você não tivesse a moto o codigo iria dizer “Nem vai kkk”

No codigo a variavel temCarro era booleano falso, portanto o codigo pulou essa parte, no if else a variavel temMoto foi checada, como o valor era true então essa parte do código é executada, caso a variavel temMoto fosse false então o codigo no bloco else seria executado.

## Arrays:

Array é uma variavel que tem mais de um valor, ou seja são uma lista de valores. Os vários valores ficam dentro de colchetes “ [ ] ”

**Como se faz:**

```javascript
const escola = 'Instituto Municipal'; // variavel composta, com um unico valor.
const professores = ['Rogério', 'Romulo', 'Santos', 'Guilherme']; // Arrays, lista com 4 valores diferentes.
```

Arrays usam indices, cada valor dentro de uma array tem um numero de referencia, o primeiro valor dentro da array sempre será 0, enquanto o segundo valor usa o numero 1.

Exemplo:

```javascript
professores = ['Rogério', 'Romulo', 'Santos', 'Guilherme'];
    // index =    '0'   ,   '1'   ,    '2'  ,    '3'
```

Para alterar valores é necessário saber qual é o numero de indice daquele valor e depois aplicar o novo valor:

Ou seja, _variavel[numero_indice] = ‘novo valor’;_

No caso, _professores[1] = ‘Carlos’;_

```javascript
professores[1] = 'Carlos'; // vai substituir o 'Romulo' do Index 1 pelo 'Carlos'

// resultado:
professores: ['Rogério', 'Carlos', 'Santos', 'Guilherme'];
    index: =     '0'   ,   '1'   ,    '2'  ,     '3'
```

Além de alterar valores, também é possivel adicionar mais itens novos dentro de uma array.

```javascript
professores[4] = 'Alberto'; // vai criar o valor 'Alberto' e adicionar no indice 4.
```

Invéz de contar valor por valor e indice por indice, é possivel saber quantos itens há no total em uma array usando o **.length**

```javascript
let professores = ['Rogério', 'Romulo', 'Santos', 'Guilherme'];

console.log(professores.length)
// resultado:
4
// array professores tem 4 itens
```

O length vai contar quantos valores existem dentro de uma array, no caso a array professores tem 4 itens.

Esse mesmo 4, do resultado, é o mesmo numero do Index disponivel para adicionar um novo valor em uma array, percebeu? Porque no array atual o professor ‘Guilherme’ está no Index 3, o ultimo numero usado, ou seja, o Index 4 pode ser usado para adicionar o novo valor com base no .length.

Então é possivel usar o .length para adicionar um novo valor dentro de uma array.

Como se faz?

```javascript
let professores = ['Rogério', 'Romulo', 'Santos', 'Guilherme'];

professores[professores.length] = 'José'

//resultado
['Rogério', 'Romulo', 'Santos', 'Guilherme', 'José'];
```

Há outra forma de adicionar novos valores na array sem saber o numero de indice disponivel e sem usar o parametro .length. Usando o parametro .push():

Como se faz:

```javascript
let professores = ['Rogério', 'Romulo', 'Santos', 'Guilherme'];

professores.push('Antônio')

//resultado
['Rogério', 'Romulo', 'Santos', 'Guilherme', 'Antônio']
```

## For:

Usado para repetir um código e seu conteúdo até uma condição ou um determinado numero de vezes.

o “For” segue usa essa regra:

```javascript
for (expressão inicial; condição a ser cumprida; atualização da expressão inicial) {
    // código que será repetido
}
```

- _expressão inicial: início do loop._
- _condição a ser cumprida: critério que vai parar o loop._
- _atualização da expressão inicial: alteração da variável utilizada na primeira expressão, o que acontece a cada loop, até a condição ser atendida._

**Como se faz?**

```javascript
for (let index = 1; index <= 3; index = index + 1){
console.log(index);
}

// resultado
1
2
3
```

Bom, essas foram minhas anotações, que vão aumentar ou não, se tiver sugestões deixe nos comentários.
