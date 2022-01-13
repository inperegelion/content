---
title: String.prototype.charAt()
slug: Web/JavaScript/Reference/Global_Objects/String/charAt
tags:
  - JavaScript
  - Method
  - Prototype
  - Reference
  - String
browser-compat: javascript.builtins.String.charAt
---
{{JSRef}}

Метод **`charAt()`** об'єкту {{jsxref("String")}} повертає новий рядок, що складається з єдиної кодової одиниці UTF-16, знайдений в рядку за переданою позицією.

{{EmbedInteractiveExample("pages/js/string-charat.html", "shorter")}}

## Синтаксис

```js
charAt(index)
```

### Параметри

- `index`
  - : Ціле число в діапазоні від `0` і до `str.length - 1`. Якщо `index` неможливо перетворити на число, або його просто не задано — замість нього буде використано усталене значення `0`, і таким чином – повернено перший символ рядка `str`.

### Повернене значення

Рядок, що відповідає одному символу (рівно одній кодовій одиниці UTF-16) за вказаним індексом `index`. Якщо значення `index` виходить за межі допустимого діапазону, метод `charAt()` поверне порожній рядок.

## Опис

Символи в рядках індексуються зліва направо. Індексом першого елемента є `0`, а індекс останнього символу в рядку, який, приміром, називається `stringName`, дорівнює значенню виразу `stringName.length - 1`. Якщо індекс, який передається в метод, виходить за межі цього діапазону, JavaScript поверне порожній рядок.

Якщо в `index` до методу `charAt()` не було передано ніякого значення — буде використано усталене, яке дорівнює `0`.

## Приклади

### Демонстрація символів, які знаходяться в різних місцях рядка

Наступний приклад вибирає символи з різних місць рядка "`Прекрасний новий світ`" і друкує їх на екран:

```js
var anyString = 'Прекрасний новий світ';
console.log("За індексом 0   знаходиться символ '" + anyString.charAt()   + "'");
// Ніякого індексу в метод не передано, використовується усталене значення 0

console.log("За індексом 0   знаходиться символ '" + anyString.charAt(0)   + "'");
console.log("За індексом 1   знаходиться символ '" + anyString.charAt(1)   + "'");
console.log("За індексом 2   знаходиться символ '" + anyString.charAt(2)   + "'");
console.log("За індексом 3   знаходиться символ '" + anyString.charAt(3)   + "'");
console.log("За індексом 4   знаходиться символ '" + anyString.charAt(4)   + "'");
console.log("За індексом 999 знаходиться символ '" + anyString.charAt(999) + "'");
```

Ці рядки виведуть на екран наступне:

```js
За індексом 0   знаходиться символ 'П'
За індексом 0   знаходиться символ 'П'
За індексом 1   знаходиться символ 'р'
За індексом 2   знаходиться символ 'е'
За індексом 3   знаходиться символ 'к'
За індексом 4   знаходиться символ 'р'
За індексом 999 знаходиться символ ''
```

### Отримання цілих символів

Наступний код дає змогу пересвідчитись, що під час проходження по рядку цикл завжди віддасть цілий символ, навіть якщо рядок містить символи, що не належать базовому багатомовному плану.

```js
var str = 'A \uD87E\uDC04 Z'; // Також можна було б безпосередньо вжити не-BMP символ
for (var i = 0, chr; i < str.length; i++) {
  if ((chr = getWholeChar(str, i)) === false) {
    continue;
  }
  // Цей код прилаштовується вгорі кожного циклу. Всередину
  // передаються цілий рядок та індекс ітерації, а повертається
  // змінна з окремим символом

  console.log(chr);
}

function getWholeChar(str, i) {
  var code = str.charCodeAt(i);

  if (Number.isNaN(code)) {
    return ''; // Позиція не знайдена
  }
  if (code < 0xD800 || code > 0xDFFF) {
    return str.charAt(i);
  }

  // Старший сурогатний символ (останнє шістнадцяткове значення можна
  // замінити на 0xDB7F, щоб повернути старший сурогат як окремий символ)
  if (0xD800 <= code && code <= 0xDBFF) {
    if (str.length <= (i + 1)) {
      throw 'Старший сурогат без наступного молодшого сурогатного символа';
    }
    var next = str.charCodeAt(i + 1);
      if (0xDC00 > next || next > 0xDFFF) {
        throw 'Старший сурогат без наступного молодшого сурогатного символа';
      }
      return str.charAt(i) + str.charAt(i + 1);
  }
  // Молодший сурогат (0xDC00 <= code && code <= 0xDFFF)
  if (i === 0) {
    throw 'Молодший сурогат без попереднього старшого сурогатного символа';
  }
  var prev = str.charCodeAt(i - 1);

  // (тут можна замінити останнє шістнадцяткове значення на 0xDB7F, щоб повернути
  // старший сурогат окремим символом приватного плану unicode)
  if (0xD800 > prev || prev > 0xDBFF) {
    throw 'Молодший сурогат без попереднього старшого сурогатного символа';
  }
  // Пропускаємо ітерації на молодших сурогатах,
  // оскільки їх уже було опрацьовано в парах зі старшими сурогатними символами
  return false;
}
```

В середовищах з реалізованим стандартом ECMAScript 2016, які дають змогу виконувати присвоєння з деструктуризацією, можна вжити наступну, більш лаконічну і дещо гнучкішу альтернативу (в тому сенсі, що тут індекс циклу автоматично враховує пропуски, пов'язані з обробкою сурогатних пар).

```js
let str = 'A\uD87E\uDC04Z'  // Також можна було б безпосередньо вжити не-BMP символ
for (let i = 0, chr; i < str.length; i++) {
  [chr, i] = getWholeCharAndI(str, i)

  // Цей код прилаштовується вгорі кожного циклу. Всередину передаються
  // цілий рядок та індекс ітерації, а повертається масив з окремим символом та
  // новим значенням 'i' (яке змінюється лише під час обробки сурогатної пари)

  console.log(chr)
}

function getWholeCharAndI(str, i) {
  let code = str.charCodeAt(i)

  if (Number.isNaN(code)) {
    return ''  // Позиція не знайдена
  }
  if (code < 0xD800 || code > 0xDFFF) {
    return [str.charAt(i), i]  // Звичайний символ, зберігаємо значення 'i' без змін
  }

  // Старший сурогатний символ (останнє шістнадцяткове значення можна
  // замінити на 0xDB7F, щоб повернути старший сурогат як окремий символ)
  if (0xD800 <= code && code <= 0xDBFF) {
    if (str.length <= (i + 1)) {
      throw 'Старший сурогат без наступного молодшого сурогатного символа'
    }
    let next = str.charCodeAt(i + 1)
      if (0xDC00 > next || next > 0xDFFF) {
        throw 'Старший сурогат без наступного молодшого сурогатного символа'
      }
      return [str.charAt(i) + str.charAt(i + 1), i + 1]
  }

  // Молодший сурогат (0xDC00 <= code && code <= 0xDFFF)
  if (i === 0) {
    throw 'Молодший сурогат без попереднього старшого сурогатного символа'
  }

  let prev = str.charCodeAt(i - 1)

  // (тут можна замінити останнє шістнадцяткове значення на 0xDB7F, щоб повернути
  // старший сурогат окремим символом приватного плану unicode)
  if (0xD800 > prev || prev > 0xDBFF) {
    throw 'Молодший сурогат без попереднього старшого сурогатного символа'
  }

  // Натомість повертається наступний символ (та збільшується індекс ітерацій)
  return [str.charAt(i + 1), i + 1]
}
```

### Виправлення методу charAt() так, щоб він підтримував не лише символи Базового багатомовного плану (BMP)

Хоча попередній приклад може бути кориснішим для програм з обов'язковою підтримкою не-BMP символів (оскільки він не вимагає знання про те, де саме знаходиться якийсь не-BMP символ), в деяких випадках може виникнути потреба вибирати символи за індексом, і при цьому обробляти сурогатні пари як один символ. В такому разі можна використати наступний код:

```js
function fixedCharAt(str, idx) {
  let ret = ''
  str += ''
  let end = str.length

  let surrogatePairs = /[\uD800-\uDBFF][\uDC00-\uDFFF]/g
  while ((surrogatePairs.exec(str)) != null) {
    let lastIdx = surrogatePairs.lastIndex
    if (lastIdx - 2 < idx) {
      idx++
    } else {
      break
    }
  }

  if (idx >= end || idx < 0) {
    return ''
  }

  ret += str.charAt(idx)

  if (/[\uD800-\uDBFF]/.test(ret) && /[\uDC00-\uDFFF]/.test(str.charAt(idx + 1))) {
    // Вперед на одну позицію, оскільки один із "символів" — це частина сурогатної пари
    ret += str.charAt(idx + 1)
  }
  return ret
}
```

## Специфікації

{{Specifications}}

## Сумісність із браузерами

{{Compat}}

## Дивіться також

- {{jsxref("String.prototype.indexOf()")}}
- {{jsxref("String.prototype.lastIndexOf()")}}
- {{jsxref("String.prototype.charCodeAt()")}}
- {{jsxref("String.prototype.codePointAt()")}}
- {{jsxref("String.prototype.split()")}}
- {{jsxref("String.fromCodePoint()")}}
- [JavaScript має проблему з Unicode – Mathias Bynens (англ.)](https://mathiasbynens.be/notes/javascript-unicode)