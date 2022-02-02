---
title: Listas
created: 2022-02-01T21:21:57.897Z
update: 2022-02-01T21:33:08.574Z
tags:
  - Javascript
  - Browser
---

# Listas

Formatação de lista no modo **conjuntivo** (`"e"`), **desjuntivo** (`"ou"`) e **unidade**

```javascript
const list = ['Macarrão', 'Alho', 'Oléo'];

// Conjuntivo
new Intl.ListFormat('pt-BR', { style: 'long', type: 'conjunction' }).format(list);
// Macarrão, Alho e Oléo

// Desjuntivo
console.log(new Intl.ListFormat('pt-BR', { style: 'long', type: 'disjunction' }).format(list));
// Macarrão, Alho ou Oléo

// Unidade
console.log(new Intl.ListFormat('pt-BR', { style: 'narrow', type: 'unit' }).format(list));
// Macarrão Alho Oléo
```