---
date: 2021-11-26T00:00:00.000Z
tags:
  - javascript
---

# Não use `str.split("")`

Quando queremos separar uma string letra por letra ou até mesmo reverter um texto utilizamos o método [`split()`](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/String/split), porém, existem diversos problemas em se utilizar este método, a própria documentação faz um breve comentário sobre [reverter uma String usando `split("")`](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/String/split#revertendo_uma_string_usando_split) não ser a melhor opção.

## Problemas do `String.prototype.split("")`

Ao fazer `.split("")` a divisão não é feita "letra por letra" por conta da maneira que o Javascript lida com o strings esta divisão pode não ocorrer como o esperado.

Por exemplo, enquanto esse emoji `😃` é representado por 2 caracteres javascript esse `😶‍🌫️` é por 6. Isso é:

```javascript
> "a".length
1
> "😃".length
2
> "😶‍🌫️".length
6
> "H̵̙͗ė̴̘l̴̥͒ḷ̶͂o̶̰͝".length
20
```

E o  resultado de tentar utilizar este método para lidar com simbolos mais complexos é esse:

```javascript
> "Rust & Go".split("")
Array(9) [ "R", "u", "s", "t", " ", "&", " ", "G", "o" ]

> "𝟘𝟙𝟚𝟛".split('')
Array(8) [ "\ud835", "\udfd8", "\ud835", "\udfd9", "\ud835", "\udfda", "\ud835", "\udfdb" ]

> '🦀 Rust & 🐹 Go'.split('')
Array(15) [ "\ud83e", "\udd80", " ", "R", "u", "s", "t", " ", "&", … ]

> "😶‍🌫️".split('')
Array(6) [ "\ud83d", "\ude36", "‍", "\ud83c", "\udf2b", "️" ]
```

## Tentativas falhas

Nenhum desses métodos resolvem o problema de fato e todos retornam os mesmos output. Emojis compostos `[ "😶‍🌫️", "🏳️‍🌈", ...]` ainda não serão divididos corretamente.

* Spread syntax (`...`)

Utilizar o [spread operator (`...`)](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Operators/Spread_syntax) na String dentro de um array.

```javascript
> [..."🦀 Rust & 🐹 Go"]
Array(13) [ "🦀", " ", "R", "u", "s", "t", " ", "&", " ", "🐹", … ]

> [..."😶‍🌫️"]
Array(4) [ "😶", "‍", "🌫", "️" ]
```

* `Array.from`

Nesse método o [`Array.from`](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/from) te permite transformar a string em um array.

* RegExp `u` flag

Nesse método é utilizado [RegExp](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/RegExp), não diria ser uma boa escolha pela legibilidade e compressão do código.

* Reduce method

Nesse método, por conta do [`for...of`](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Statements/for...of), é necessário criar uma variável para armazenar os valores.

## Solução

A única solução que encontrei com um amigo é utilizando o [Intl.Segmenter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/Segmenter). E vai da sua criatividade para utiliza-lo:

* Generator

```javascript=
function* stringChars(s) { 
  for (const ch of new Intl.Segmenter().segment(s)) 
    yield ch.segment;
}

console.log([...stringChars('😶‍🌫️')]) // [ '😶‍🌫️' ]
console.log([...stringChars('👨‍👨‍👧‍👦')]) // [ '👨‍👨‍👧‍👦' ]
```

* Spread Operator

```javascript=
const segmenter = new Intl.Segmenter()

console.log([...segmenter.segment('😶‍🌫️')].map(({ segment }) => segment)) // [ '😶‍🌫️' ]
console.log([...segmenter.segment('👨‍👨‍👧‍👦')].map(({ segment }) => segment))// [ '👨‍👨‍👧‍👦' ]
```
