---
title: String.prototype.includes()
slug: Web/JavaScript/Reference/Global_Objects/String/includes
tags:
  - JavaScript
  - Method
  - Prototype
  - Reference
  - String
  - Polyfill
browser-compat: javascript.builtins.String.includes
---
{{JSRef}}

Метод **`includes()`** виконує чутливий до регістру пошук для визначення, чи можна один рядок знайти всередині іншого, повертаючи `true` або `false` відповідно.

{{EmbedInteractiveExample("pages/js/string-includes.html", "shorter")}}

## Синтаксис

```js
includes(searchString)
includes(searchString, position)
```

### Параметри

- `searchString`
  - : Рядок, який необхідно знайти всередині початкового рядка `str`.
- `position` {{optional_inline}}
  - : Номер позиції всередині рядка, з якої розпочнеться пошук шуканого рядка `searchString`. (Усталено дорівнює `0`.)

### Повернене значення

Повертає **`true`**, якщо шуканий рядок було знайдено будь-де всередині початкового рядка, і **`false`**, якщо рядок знайдено не було.

## Опис

Цей метод дає змогу визначити, чи містить один рядок – інший.

### Чутливість до регістру

Метод `includes()` чутливий до регістру. Для прикладу, наступний вираз поверне `false`:

```js
'Синій кит'.includes('синій')  // повертає false
```

## Поліфіл

Цей метод було додано специфікацією ECMAScript 2015, і він поки що може не бути присутнім у всіх реалізаціях JavaScript.

Однак, його можна легко відтворити через такий поліфіл:

```js
if (!String.prototype.includes) {
  String.prototype.includes = function(search, start) {
    'use strict';

    if (search instanceof RegExp) {
      throw TypeError('first argument must not be a RegExp');
    }
    if (start === undefined) { start = 0; }
    return this.indexOf(search, start) !== -1;
  };
}
```

## Приклади

### Застосування методу `includes()`

```js
const str = 'Чи бути, чи не бути — ось питання.'

console.log(str.includes('Чи бути'))        // true
console.log(str.includes('питання'))     // true
console.log(str.includes('не існує'))  // false
console.log(str.includes('Чи бути', 1))     // false
console.log(str.includes('ЧИ БУТИ'))        // false
console.log(str.includes(''))             // true
```

## Специфікації

{{Specifications}}

## Сумісність із браузерами

{{Compat}}

## Дивіться також

- Поліфіл методу `String.prototype.includes` доступний у [`core-js`](https://github.com/zloirock/core-js#ecmascript-string-and-regexp)
- {{jsxref("Array.prototype.includes()")}}
- {{jsxref("TypedArray.prototype.includes()")}}
- {{jsxref("String.prototype.indexOf()")}}
- {{jsxref("String.prototype.lastIndexOf()")}}
- {{jsxref("String.prototype.startsWith()")}}
- {{jsxref("String.prototype.endsWith()")}}
