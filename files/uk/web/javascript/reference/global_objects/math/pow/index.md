---
title: Math.pow()
slug: Web/JavaScript/Reference/Global_Objects/Math/pow
tags:
  - JavaScript
  - Math
  - Method
  - Reference
browser-compat: javascript.builtins.Math.pow
---
{{JSRef}}

Функція **`Math.pow()`** повертає результат піднесення основи `base` до степеня `exponent`, як у `base^exponent`.

{{EmbedInteractiveExample("pages/js/math-pow.html")}}

## Синтаксис

```js
Math.pow(base, exponent)
```

### Параметри

- `base`
  - : Значення основи.
- `exponent`
  - : Показник степеня, до якого слід піднести основу `base`.

### Повернене значення

Число, що відповідає результату піднесення переданої основи до переданого показника степеня.

## Опис

Функція **`Math.pow()`** повертає результат піднесення основи `base` до степеня `exponent`, як у `base^exponent`, причому і `base`, і `exponent` вказані в десятковій системі числення.

Оскільки `pow()` — це статичний метод об'єкта `Math`, його потрібно завжди використовувати через `Math.pow()`. Не слід звертатись до нього як до методу власноруч створеного екземпляра `Math` (`Math` не є конструктором).

Якщо значення основи — від'ємне, а переданий показник степеня — не ціле число, результат дорівнюватиме NaN.

## Приклади

### Застосування Math.pow()

```js
// простий приклад
Math.pow(7, 2);    // 49
Math.pow(7, 3);    // 343
Math.pow(2, 10);   // 1024
// дробові показники степеня
Math.pow(4, 0.5);  // 2 (квадратний корінь з 4)
Math.pow(8, 1/3);  // 2 (кубічний корівнь з 8)
Math.pow(2, 0.5);  // 1.4142135623730951 (квадратний корінь з 2)
Math.pow(2, 1/3);  // 1.2599210498948732 (кубічний корінь з 2)
// від‘ємні показники степеня
Math.pow(7, -2);   // 0.02040816326530612 (1/49)
Math.pow(8, -1/3); // 0.5
// від‘ємні основи
Math.pow(-7, 2);   // 49 (квадрати — завжди додатні)
Math.pow(-7, 3);   // -343 (куби можуть бути від'ємними)
Math.pow(-7, 0.5); // NaN (від'ємні числа не мають дійсного квадратного кореня)
// у зв'язку з тим, що "парні" та "непарні" корені знаходяться близько один від одного,
// та через обмеження точності чисел з рухомою комою,
// від'ємні основи з дробовими показниками степенів завжди повертатимуть NaN
Math.pow(-7, 1/3); // NaN
```

## Специфікації

{{Specifications}}

## Сумісність із браузерами

{{Compat}}

## Дивіться також

- {{jsxref("Math.cbrt()")}}
- {{jsxref("Math.exp()")}}
- {{jsxref("Math.log()")}}
- {{jsxref("Math.sqrt()")}}
- [Оператор піднесення до степеня](/en-US/docs/Web/JavaScript/Reference/Operators/Exponentiation)