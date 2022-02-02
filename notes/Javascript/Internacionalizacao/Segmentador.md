---
title: Segmentador
created: 2022-02-01T20:54:45.231Z
update: 2022-02-01T21:10:14.229Z
tags:
  - Javascript
  - Browser
---

# Segmentador

O segmentador identifica as letras/palavras/grafemas do idioma para realizar uma seperação adequada, beneficiando principalmente as linguas que não usam espaços entrem as palavras (Por exemplo: japonês, chinês, tailandês, etc).

```javascript
const phrase = "Primeira linha.\nSegunda linha.\nTerceira linha."
const segmenterWord = new Intl.Segmenter('pt-BR', { granularity: 'word' });

Array.from(segmenterWord.segment(phrase)).map(({ segment }) => segment)
// ['Primeira', ' ', 'linha', '.', '\n', 'Segunda', ' ', 'linha', '.', '\n', 'Terceira', ' ', 'linha', '.']

const phrase = "A\nB\nC."
const segmenter = new Intl.Segmenter('pt-BR');

Array.from(segmenter.segment(phrase)).map(({ segment }) => segment)
// ['A', '\n', 'B', '\n', 'C', '.']
```

Também corrige os problemas do Javascript por utiliza UTF-16: [[Revertendo strings com emoji]]