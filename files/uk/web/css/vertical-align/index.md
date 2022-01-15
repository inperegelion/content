---
title: vertical-align
slug: Web/CSS/vertical-align
tags:
  - CSS
  - CSS Property
  - Reference
  - recipe:css-property
browser-compat: css.properties.vertical-align
---

{{CSSRef}}

Властивість [CSS](/uk/docs/Web/CSS) **`vertical-align`** (вертикальне шикування) встановлює вертикальне шикування рядкового, рядково-блокового елемента або елемента комірки таблиці.

{{EmbedInteractiveExample("pages/css/vertical-align.html")}}

Властивість `vertical-align` може вживатись у двох контекстах:

- Для вертикального шикування рамок рядкового елемента всередині рамок рядка його контейнера. Наприклад, це може бути помічним у [вертикальному розміщенні зображення в рядку тексту](#vertykalne-shykuvannia-u-ramkakh-riadka).
- Для вертикального шикування [вмісту комірки таблиці](#vertykalne-shykuvannia-u-komirtsi-tablytsi).

Зверніть увагу, що `vertical-align` застосовується лише до рядкових, рядково-блокових елементів та комірок таблиці: її не можна використати для вертикального шикування [блокових елементів](/uk/docs/Web/HTML/Block-level_elements).

## Синтаксис

```css
/* Значення – ключові слова */
vertical-align: baseline;
vertical-align: sub;
vertical-align: super;
vertical-align: text-top;
vertical-align: text-bottom;
vertical-align: middle;
vertical-align: top;
vertical-align: bottom;

/* Значення <length> */
vertical-align: 10em;
vertical-align: 4px;

/* Значення <percentage> */
vertical-align: 20%;

/* Глобальні значення */
vertical-align: inherit;
vertical-align: initial;
vertical-align: revert;
vertical-align: unset;
```

Властивість `vertical-align` вказується як одне із перелічених нижче значень.

### Значення для рядкових елементів

#### Значення, відносні щодо предка

Наступні значення вертикально шикують елемент відносно свого батьківського елемента:

- `baseline` (основна лінія)
  - : Припасовує основну лінію елемента до основної лінії предка. Основна лінія деяких [заміщених елементів](/uk/docs/Web/CSS/Replaced_element), наприклад, {{HTMLElement("textarea")}}, не описана специфікацією HTML, тож їх поведінка з цим ключовим словом може відрізнятися у різних браузерах.
- `sub` (під)
  - : Припасовує основну лінію елемента до основної лінії підрядкового тексту свого предка.
- `super` (над)
  - : Припасовує основну лінію елемента до основної лінії надрядкового тексту свого предка.
- `text-top` (верх тексту)
  - : Припасовує верх елемента до верху шрифту батьківського елемента.
- `text-bottom` (низ тексту)
  - : Припасовує низ елемента до низу шрифту батьківського елемента.
- `middle` (середина)
  - : Припасовує середину елемента до основної лінії батьківського елемента плюс половина x-висоти шрифту предка.
- {{cssxref("&lt;length&gt;")}}
  - : Припасовує основну лінію елемента на вказаній висоті над основною лінією предка. Допускаються від‘ємні значення.
- {{cssxref("&lt;percentage&gt;")}}
  - : Припасовує основну лінію елемента на вказаній висоті над основною лінією предка, у відсотках щодо властивості {{Cssxref("line-height")}} предка. Допускаються від‘ємні значення.

#### Значення, відносні щодо рядка

Наступні значення вертикально шикують елемент відносно усього рядка:

- `top` (верх)
  - : Припасовує верх елемента та його нащадків до верху всього рядка.
- `bottom` (низ)
  - : Припасовує низ елемента та його нащадків до низу всього рядка.

Для елементів без основної лінії натомість використовується край нижнього зовнішнього відступу.

### Значення для комірок таблиць

- `baseline` (а також `sub`, `super`, `text-top`, `text-bottom`, `<length>` і `<percentage>`)
  - : Припасовує основну лінію комірки до основної лінії усіх інших комірок в ряду, що шикуються за основною лінією.
- `top` (верх)
  - : Припасовує край верхнього внутрішнього відступу комірки до верху ряду.
- `middle` (середина)
  - : Центрує рамки внутрішніх відступів комірки у ряду.
- `bottom` (низ)
  - : Припасовує край нижнього внутрішнього відступу до низу ряду.

Допустимі від‘ємні значення.

## Формальне визначення

{{CSSInfo}}

## Формальний синтаксис

{{csssyntax}}

## Приклади

### Базовий приклад

#### HTML

```html
<div>
  Ось <img src="frame_image.svg" alt="link" width="32" height="32" /> зображення
  із звичайним шикуванням.
</div>
<div>
  А ось
  <img class="top" src="frame_image.svg" alt="link" width="32" height="32" /> –
  зображення із шикуванням `text-top`.
</div>
<div>
  Також
  <img class="bottom" src="frame_image.svg" alt="link" width="32" height="32" />
  – зображення із шикуванням `text-bottom`.
</div>
<div>
  І
  <img class="middle" src="frame_image.svg" alt="link" width="32" height="32" />
  зображення із шикуванням `middle`.
</div>
```

#### CSS

```css
img.top {
  vertical-align: text-top;
}
img.bottom {
  vertical-align: text-bottom;
}
img.middle {
  vertical-align: middle;
}
```

#### Результат

{{EmbedLiveSample("Basic_example")}}

### Вертикальне шикування у рамках рядка

#### HTML

```html
<p>
  top: <img style="vertical-align: top" src="star.png" /> middle:
  <img style="vertical-align: middle" src="star.png" /> bottom:
  <img style="vertical-align: bottom" src="star.png" /> super:
  <img style="vertical-align: super" src="star.png" /> sub:
  <img style="vertical-align: sub" src="star.png" />
</p>

<p>
  text-top: <img style="vertical-align: text-top" src="star.png" /> text-bottom:
  <img style="vertical-align: text-bottom" src="star.png" /> 0.2em:
  <img style="vertical-align: 0.2em" src="star.png" /> -1em:
  <img style="vertical-align: -1em" src="star.png" /> 20%:
  <img style="vertical-align: 20%" src="star.png" /> -100%:
  <img style="vertical-align: -100%" src="star.png" />
</p>
```

```css hidden
#* {
  box-sizing: border-box;
}

img {
  margin-right: 0.5em;
}

p {
  height: 3em;
  padding: 0 0.5em;
  font-family: monospace;
  text-decoration: underline overline;
  margin-left: auto;
  margin-right: auto;
  width: 80%;
}
```

#### Результат

{{EmbedLiveSample("Vertical_alignment_in_a_line_box", '100%', 160, "", "")}}

### Вертикальне шикування у комірці таблиці

#### HTML

```html
<table>
  <tr>
    <td style="vertical-align: baseline">baseline</td>
    <td style="vertical-align: top">top</td>
    <td style="vertical-align: middle">middle</td>
    <td style="vertical-align: bottom">bottom</td>
    <td>
      <p>
        Є теорія, згідно з якою, якщо хтось нарешті здогадається, в чому сенс
        існування Всесвіту, той одразу щезне або буде замінений на щось ще
        придуркуватіше й заплутаніше.
      </p>
      <p>Відповідно до іншої теорії це вже трапилося.</p>
    </td>
  </tr>
</table>
```

#### CSS

```css
table {
  margin-left: auto;
  margin-right: auto;
  width: 80%;
}

table,
th,
td {
  border: 1px solid black;
}

td {
  padding: 0.5em;
  font-family: monospace;
}
```

#### Результат

{{EmbedLiveSample("Vertical_alignment_in_a_table_cell", '100%', 230, "", "")}}

## Специфікації

{{Specifications}}

## Сумісність із браузерами

{{Compat}}

## Дивіться також

- [Типові випадки використання Флексбоксу, розділ "Центрування елемента"](/uk/docs/Web/CSS/CSS_Flexible_Box_Layout/Typical_Use_Cases_of_Flexbox#tsentruvannia-elementa)
- {{Cssxref("line-height")}}, {{Cssxref("text-align")}}, {{Cssxref("margin")}}
- [Розуміння `vertical-align`, або "Як (не) центрувати вміст вертикально" (англ.)](http://phrogz.net/css/vertical-align/index.html)
- [Vertical-Align: усе, що варто знати (англ.)](https://christopheraue.net/design/vertical-align)
