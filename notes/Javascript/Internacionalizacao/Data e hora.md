---
title: Data e hora
created: 2022-02-01T19:23:35.468Z
update: 2022-02-01T20:43:16.242Z
tags:
  - Javascript
  - Browser
---

# Data e hora

> Formatação de data e hora.

Algumas formatações que achei útil e muito mais intuitivas.

```js
const date = new Date('Tue Feb 01 2022 20:23:52 GMT-0300');

new Intl.DateTimeFormat("pt-BR" , {
 	dateStyle: "short",
	timeStyle: "short"
}).format(date);

// '01/02/2022 20:23'

new Intl.DateTimeFormat('pt-BR', { 
	dateStyle: 'full', 
	timeStyle: 'long' 
}).format(date);

// 'terça-feira, 1 de fevereiro de 2022 20:23:52 BRT'

new Intl.DateTimeFormat('pt-BR', {
    hour: 'numeric', 
    minute: 'numeric', 
    hourCycle: 'h12',   // necessário para o dayPeriod funcionar
    dayPeriod: 'short', // para pt-BR o argumento não importa
    timeZone: 'UTC' 
}).format(date);

// '11:23 da noite'
```