---
title: Використання медіазапитів
slug: Web/CSS/Media_Queries/Using_media_queries
tags:
  - Advanced
  - CSS
  - Guide
  - Media
  - Media Queries
  - Responsive Design
  - Web
---

{{CSSRef}}

**Медіазапити** корисні тоді, коли хочеться змінити сайт чи застосунок залежно від загального типу пристрою (наприклад, друк чи екран) або певних характеристик і параметрів (наприклад, роздільної здатності екрану чи ширини {{glossary("viewport", "вікна перегляду")}} браузера).

Медіазапити використовуються для наступних речей:

- Для умовного застосування стилів за допомогою [директив](/uk/docs/Web/CSS/At-rule) [CSS](/uk/docs/Web/CSS) {{cssxref("@media")}} та {{cssxref("@import")}}.
- Для націлення на певні медіа {{HTMLElement("style")}}, {{HTMLElement("link")}}, {{HTMLElement("source")}} та інших [HTML](/uk/docs/Web/HTML) елементів за допомогою атрибуту `media=`.
- Для [перевірки та відстеження станів медіа](/uk/docs/Web/CSS/Media_Queries/Testing_media_queries) за допомогою методів [JavaScript](/uk/docs/Web/JavaScript) {{domxref("Window.matchMedia()")}} та {{domxref("MediaQueryList.addListener()")}}.

> **Примітка:** Приклади на цій сторінці використовують медіазапит CSS `@media` для ілюстративних потреб, однак базовий синтаксис залишається однаковим для всіх типів медіазапитів.

## Синтаксис

Медіазапит складається із необов‘язкового _типу медіа_ і будь-якої кількості виразів _ознак медіа_, що необов‘язково можуть бути поєднані у різний спосіб за допомогою _логічних операторів_.
Медіазапити є нечутливими до регістру.

- [Типи медіа](/uk/docs/Web/CSS/@media#media_types) визначають широкі категорії пристроїв, до яких застосовується медіазапит: `all` (усі), `print` (друк), `screen` (екран), `speech` (мовлення).

  Тип є необов‘язковим (усталено вважається рівним `all`), крім випадків використання логічних операторів `not` або `only`.

- [Ознаки медіа](/uk/docs/Web/CSS/@media#media_features) описують певну характеристику {{glossary("user agent", "користувацького агента")}}, пристрою виведення чи середовища:  {{cssxref("@media/any-hover", "any-hover")}}, {{cssxref("@media/any-pointer", "any-pointer")}}, {{cssxref("@media/aspect-ratio", "aspect-ratio")}}, {{cssxref("@media/color", "color")}}, {{cssxref("@media/color-gamut", "color-gamut")}}, {{cssxref("@media/color-index", "color-index")}}, {{cssxref("@media/device-aspect-ratio", "device-aspect-ratio")}} {{deprecated_inline}}, {{cssxref("@media/device-height", "device-height")}} {{deprecated_inline}}, {{cssxref("@media/device-width", "device-width")}} {{deprecated_inline}}, {{cssxref("@media/display-mode", "display-mode")}}, {{cssxref("@media/dynamic-range", "dynamic-range")}}, {{cssxref("@media/forced-colors", "forced-colors")}}, {{cssxref("@media/grid", "grid")}}, {{cssxref("@media/height", "height")}}, {{cssxref("@media/hover", "hover")}}, {{cssxref("@media/inverted-colors", "inverted-colors")}}, {{cssxref("@media/monochrome", "monochrome")}}, {{cssxref("@media/orientation", "orientation")}}, {{cssxref("@media/overflow-block", "overflow-block")}}, {{cssxref("@media/overflow-inline", "overflow-inline")}}, {{cssxref("@media/pointer", "pointer")}}, {{cssxref("@media/prefers-color-scheme", "prefers-color-scheme")}}, {{cssxref("@media/prefers-contrast", "prefers-contrast")}}, {{cssxref("@media/prefers-reduced-motion", "prefers-reduced-motion")}}, {{cssxref("@media/resolution", "resolution")}}, {{cssxref("@media/scripting", "scripting")}}, {{cssxref("@media/update-frequency", "update")}}, {{cssxref("@media/video-dynamic-range", "video-dynamic-range")}}, {{cssxref("@media/width", "width")}}.

  Наприклад, риса {{cssxref("@media/hover", "hover")}} дає змогу запитові перевірити, чи підтримує пристрій наведення курсора.
  Вирази ознак медіа перевіряють присутність таких ознак або певних значень, і є цілком необов‘язковими.
  Кожен вираз ознаки медіа мусить бути оточений дужками.

- [Логічні оператори](/uk/docs/Web/CSS/@media#logical_operators) можуть використовуватись для створення складних медіазапитів: `not` (не), `and` (і) та `only` (лише).
  Також можна поєднувати кілька медіазапитів в одне правило, розділяючи їх комами.

Медіазапит обчислюється в `true`, коли тип медіа (якщо вказаний) відповідає пристроєві, на котрому відбувається перегляд документа _і_ всі вирази ознак медіа обчислюються в `true`.
Запити, що включають невідомі типи медіа, завжди обчислюються в `false`.

> **Примітка:** Файл стилів із медіазапитом, прикріпленим до його тега {{HTMLElement("link")}}, [будуть стягнені](https://scottjehl.github.io/CSS-Download-Tests/) навіть якщо запит обчислюється у `false`; стягнення відбудеться, але пріоритет такого стягнення буде куди нижчим.
> Попри це, такі стилі не будуть застосовані, якщо (або поки) медіазапит не матиме значення `true`.
> Про причини такої поведінки можна прочитати в блозі Tomayac: [Чому браузер стягує файли стилів із невідповідними медіазапитами (англ.)](https://medium.com/@tomayac/why-browsers-download-stylesheets-with-non-matching-media-queries-eb61b91b85a2).

## Націлення на типи медіа

Медіа типи описують загальні категорії пристроїв.
Попри те, що вебсайти зазвичай розробляють для відображення на екранах, може виникнути потреба створити стилі, націлені на особливі пристрої, наприклад, принтери або звукові читачі з екрана.

```css
@media print {
  ...;
}
```

Також можна цілитись на кілька категорій пристроїв.
Наприклад, наступна директива `@media` використовує два медіазапити, щоб націлитись як на пристрої з екраном, так і на принтери:

```css
@media screen, print {
  ...;
}
```

Перелік медіатипів можна переглянути в розділі [типи медіа](/uk/docs/Web/CSS/@media#media_types).
Оскільки типи медіа описують дуже широкі категорії пристроїв, доступні лише кілька можливих значень; щоб цілитись на більш специфічні атрибути, слід натомість використовувати _ознаки медіа_.

## Націлення на ознаки медіа

Ознаки медіа описують специфічні характеристики {{glossary("user agent", "користувацьких агентів")}}, пристрою виводу чи середовища.
Наприклад, можна застосувати певні стилі до широкоекранних моніторів, комп‘ютерів із мишами, або до пристроїв, що використовуються в умовах низького освітлення.
Наступний приклад застосовує стилі тоді, коли _основний_ механізм введення користувача (наприклад, миша) може наводити курсор на елементи:

```css
@media (hover: hover) {
  ...;
}
```

Чимало ознак медіа є _діапазонними_, тобто можуть мати префікс "min-" чи "max-", щоб вказати обмеження найменшого та найбільшого можливих значень.
Наприклад, наступний CSS застосує стилі лише якщо ширина {{glossary("viewport", "вікна перегляду")}} браузера рівна або менша як 12450 пікселів:

```css
@media (max-width: 12450px) {
  ...;
}
```

Якщо створити запит на ознаку медіа, не вказуючи значення, то вкладені стилі будуть використовуватись, поки значення ознаки не рівне нулю (або, на Рівні 4, `none`).
Наприклад, наступний CSS буде застосований на будь-якому пристрої із кольоровим екраном:

```css
@media (color) {
  ...;
}
```

Якщо ознака не відповідає пристроєві, на котрому працює браузер, то вирази, що включають таку ознаку медіа, завжди рівні `false`.
Наприклад, стилі, вкладені у наступний запит, ніколи не будуть використані, тому що жоден суто мовленнєвий пристрій не має співвідношення сторін екрана:

```css
@media speech and (aspect-ratio: 11/5) {
  ...;
}
```

Для отримання більшої кількості прикладів медіазапитів з [ознаками медіа](/uk/docs/Web/CSS/@media#media_features), дивіться довідкові сторінки відповідних ознак.

## Створення складних медіазапитів

Іноді хочеться створити медіазапит, що залежить від кількох умов. Тоді на сцену виходять _логічні оператори_: `not` (не), `and` (і) та `only` (лише).
Крім того, можна поєднувати кілька медіазапитів у _розділений комами список_; це дає змогу застосовувати однакові стилі в різних ситуаціях.

У попередньому прикладі присутнє використання оператора `and` для групування _типу_ медіа з _ознакою_ медіа.
Оператор `and` також може поєднувати кілька ознак медіа в один медіазапит. Тим часом оператор `not` заперечує медіазапит, по суті обертаючи його звичайне значення на протилежне.
Оператор `only` не дає старим браузерам застосувати стилі.

> **Примітка:** У більшості випадків використовується тип медіа `all` – коли не вказаний інший.
> Втім, якщо використовується оператор `not` або `only`, то вказання типу медіа є обов‘язковим.

### Поєднання кількох типів або ознак

Ключове слово `and` поєднує ознаку медіа із типом медіа _або_ з іншими ознаками медіа.
Наступний приклад поєднує дві ознаки медіа, щоб обмежити застосування стилів пристроями з альбомною орієнтацією та шириною не меншою 30 емів:

```css
@media (min-width: 30em) and (orientation: landscape) {
  ...;
}
```

Аби обмежити дію стилів пристроями з екраном, можна приєднати ознаки медіа ланцюжком до типу медіа `screen`:

```css
@media screen and (min-width: 30em) and (orientation: landscape) {
  ...;
}
```

### Перевірка кількох запитів

Для застосування стилів тоді, коли пристрій користувача відповідає будь-якому з кількох типів медіа, ознак чи станів, можна використати розділений комами список.
Наприклад, наступна директива застосує свої стилі, якщо пристрій користувача або має висоту не меншу 680 пікселів, _або_ є пристроєм з екраном у книжній орієнтації:

```css
@media (min-height: 680px), screen and (orientation: portrait) {
  ...;
}
```

Щодо прикладу вище, якщо користувач має принтер із висотою сторінки 800 пікселів, то виказ медіа матиме значення `true`, оскільки спрацює перший запит.
Так само, якщо користувач користується смартфоном у книжному режимі з висотою вікна перегляду 480 пікселів, спрацює другий запит, і виказ медіа знову матиме значення `true`.

### Розворот значення запиту

Ключове слово `not` обертає значення цілого медіазапиту на протилежне. Воно заперечить лише той певний медіазапит, до котрого застосовано.
(Отже, воно не буде застосовано до кожного медіазапиту в розділеному комами списку медіазапитів.)
Ключове слово `not` не може бути використане для заперечення одного запиту ознаки, а лише цілого медіазапиту.
`not` обробляється останнім у наступному запиті:

```css
@media not all and (monochrome) {
  ...;
}
```

... так, що запит вище обробляється в наступному порядку:

```css
@media not (all and (monochrome)) {
  ...;
}
```

... а не так:

```css example-bad
@media (not all) and (monochrome) {
  ...;
}
```

Ось іще один приклад, наступний медіазапит:

```css
@media not screen and (color), print and (color) {
  ...;
}
```

... обробляється так:

```css
@media (not (screen and (color))), print and (color) {
  ...;
}
```

### Покращення сумісності зі старішими браузерами

Ключове слово `only` запобігає застосуванню певних стилів старішими браузерами, що не підтримують медіазапити з ознаками медіа.
_Це не має ефекту в сучасних браузерах._

```css
@media only screen and (color) {
  ...;
}
```

## Покращення синтаксису в Рівні 4

Специфікація "Медіазапити, рівень 4" включає певні покращення синтаксису, покликані зробити медіазапити з використанням ознак типу діапазону, наприклад, висоти чи ширини, менш багатослівними. Рівень 4 додає _контекст діапазону_ для написання таких запитів. Наприклад, за допомогою функціональності `max-` для ширини можна було б написати наступне:

> **Примітка:** Специфікація "Медіазапити, рівень 4" має прийнятну підтримку у сучасних браузерах, втім, деякі ознаки медіа підтримуються недостатньо добре.
> Дивіться [таблицю сумісності з браузерами `@media`](/uk/docs/Web/CSS/@media#sumisnist-iz-brauzeramy) для заглиблення.

```css
@media (max-width: 30em) {
  ...;
}
```

На "Медіазапитах, рівень 4" це може бути переписано як:

```css
@media (width <= 30em) {
  ...;
}
```

За допомогою `min-` і `max-` можна було б перевірити попадання ширини в діапазон так:

```css
@media (min-width: 30em) and (max-width: 50em) {
  ...;
}
```

На Рівні 4 це було б переписано так:

```css
@media (30em <= width <= 50em) {
  ...;
}
```

"Медіазапити, рівень 4" також додає способи поєднання медіазапитів за допомогою повної булевої алгебри з **and**, **not** і **or**.

### Заперечення ознаки з `not`

Застосування `not()` до ознаки медіа заперечує таку ознаку в запиті. Наприклад, `not(hover)` дасть збіг, якщо пристрій не має функціоналу наведення:

```css
@media (not(hover)) {
  ...;
}
```

### Перевірка кількох ознак із `or`

Можна використовувати `or` для перевірки збігу з більш ніж однією ознакою, отримуючи `true`, якщо є збіг з будь-якою із наведених ознак.
Наприклад, наступний запит перевіряє пристрій на монохромний екран або на функціонал наведення:

```css
@media (not (color)) or (hover) {
  ...;
}
```

## Дивіться також

- [@media](/uk/docs/Web/CSS/@media)
- [Програмна перевірка медіазапитів](/uk/docs/Web/CSS/Media_Queries/Testing_media_queries)
- [Анімації CSS між медіазапитами (англ.)](http://davidwalsh.name/animate-media-queries)
- [Розширені ознаки медіа від Mozilla](/uk/docs/Web/CSS/Mozilla_Extensions#Media_features)
- [Розширені ознаки медіа в WebKit](/uk/docs/Web/CSS/WebKit_Extensions#Media_features)
