---
title: Tempo relativo
created: 2022-02-01T20:46:45.893Z
update: 2022-02-01T21:35:53.373Z
tags:
  - Javascript
  - Browser
---

# Tempo relativo

Exemplos de formatação de tempo relativo em português brasileiro.

```javascript
const rtf = new Intl.RelativeTimeFormat("pt-BR", {
    localeMatcher: "best fit",
    numeric: "always",
    style: "long",
});

rtf.format(-2, "day");
// 'há 2 dias'

rtf.format(3, "day");
// 'em 3 dias'

rtf.format(5, "hour");
// 'em 5 horas'
```

Com a opção `numeric: "auto"` a contagem de dias vai dar preferência para  `"anteontem"`, `"ontem"`, `"amanhã"` e `"depois de amanhã"`.

```javascript
const rtf = new Intl.RelativeTimeFormat("pt-BR", { numeric: "auto" });

rtf.format(-3, "day");
// 'há 3 dias'

rtf.format(-2, "day");
// 'anteontem'

rtf.format(-1, "day");
// 'ontem'

rtf.format(1, "day");
// 'amanhã'

rtf.format(2, "day");
// 'depois de amanhã'

rtf.format(3, "day");
// 'em 3 dias'
```