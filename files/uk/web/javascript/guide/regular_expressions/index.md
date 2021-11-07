---
title: Регулярні вирази
slug: Web/JavaScript/Guide/Regular_Expressions
tags:
  - Guide
  - Intermediate
  - JavaScript
  - Reference
  - RegExp
  - Regular Expressions
  - regex
---
{{jsSidebar("JavaScript Guide")}} {{PreviousNext("Web/JavaScript/Guide/Text_formatting", "Web/JavaScript/Guide/Indexed_collections")}}

Регулярні вирази — це паттерни, які застосовуються для пошуку збігів з комбінаціями символів у рядках. У JavaScript регулярні вирази також є об'єктами. Ці паттерни використовуються методами об'єкта {{jsxref("RegExp")}}: {{jsxref("RegExp.exec", "exec()")}} і {{jsxref("RegExp.test", "test()")}}, і методами {{jsxref("String")}}: {{jsxref("String.match", "match()")}}, {{jsxref("String.matchAll", "matchAll()")}}, {{jsxref("String.replace", "replace()")}}, {{jsxref("String.replaceAll", "replaceAll()")}}, {{jsxref("String.search", "search()")}} і {{jsxref("String.split", "split()")}}.
Цей розділ описує регулярні вирази у JavaScript.

## Створення регулярного виразу

Сконструювати регулярний вираз можна одним із двох способів:

- Використавши літерал регулярного виразу, який складається з паттерну, оточеного косими рисками, як показано нижче:

  ```js
    let re = /ab+c/;
    ```

  Літерали регулярного виразу забезпечують компіляцію виразу під час завантаження скрипта.
  Якщо регулярний вираз залишається незмінним, такий варіант може покращити швидкодію.

- Або ж викликавши конструктор об'єкту {{jsxref("RegExp")}}, як показано:

  ```js
    let re = new RegExp('ab+c');
    ```

  Використання конструктора забезпечує компіляцію регулярного виразу під час виконання програми.
  Конструктор слід використовувати, якщо наперед невідомо, чи паттерн буде змінюватись, або ж якщо паттерн іще невідомий, і його буде отримано пізніше з інших джерел (наприклад, введено користувачем).

## Написання паттерну регулярного виразу

Паттерн регулярного виразу складається з простих символів, як от `/abc/`, або ж з поєднання простих і спеціальних символів, як `/ab*c/` чи `/Chapter (\d+)\.\d*/`.
Останній приклад містить дужки, які використовуються як вказівка до запам'ятовування.
Зіставлення, виконане з цією частиною паттерну, буде запам'ятоване для пізнішого використання, як це описано в частині [Застосування груп](/uk/docs/Web/JavaScript/Guide/Regular_Expressions/Groups_and_Ranges#using_groups).

> **Зауваження:** Якщо ви вже знайомі з формами регулярних виразів, зверніть увагу на [шпаргалку](/uk/docs/Web/JavaScript/Guide/Regular_Expressions/Cheatsheet), якщо потрібно швидко знайти якийсь конкретний паттерн чи конструкцію.

### Застосування простих паттернів

Прості паттерни складаються з символів, яким треба знайти прямі відповідники. Наприклад, паттерн `/abc/` збігається з комбінацією символів у рядках тільки коли трапляється саме ця послідовність `"abc"` (всі букви разом, і саме в такому порядку). Такий збіг трапився б у двох рядках: `"Hi, do you know your abc's?"` і `"The latest airplane designs evolved from slabcraft."`. В обох випадках трапляється збіг з підрядком `"abc"`. Не існує збігів у рядку `"Grab crab"`, і хоча він містить підрядок `"ab c"`, в ньому не зустрічається точна послідовність `"abc"`.

### Застосування спеціальних символів

Якщо пошук збігу потребує чогось більшого, аніж просто прямого відповідника, як от знаходження однієї чи більше літер «b», чи знаходження пробілу, слід включати в паттерн спеціальні символи. Наприклад, щоб знайти збіг для _одної літери `"a"`, після якої є нуль або більше літер `"b"`, а за ними літера `"c"`_, використовується патерн `/ab*c/`: зірочка `*` після `"b"` означає "наявність попереднього елемента в кількості 0 чи більше одиниць. В рядку `"cbbabbbbcdebc"` цей патерн покаже збіг з підрядком `"abbbbc"`.

Наступні сторінки містять списки різних спеціальних символів, розбитих на категорії, з описами та прикладами.

- [Перевірки](/uk/docs/Web/JavaScript/Guide/Regular_Expressions/Assertions)
  - : Перевірки включають межі, які позначають початки й закінчення слів та рядків, та інші паттерни, котрі якимось чином вказують, що збіг можливий (включно з випереджувальними, ретроспективними та умовними виразами).
- [Класи символів](/uk/docs/Web/JavaScript/Guide/Regular_Expressions/Character_Classes)
  - : Розрізняють різні типи символів. Наприклад, розрізнення літер та цифр.
- [Групи й діапазони](/uk/docs/Web/JavaScript/Guide/Regular_Expressions/Groups_and_Ranges)
  - : Вказують групи й діапазони символів виразу.
- [Квантори](/uk/docs/Web/JavaScript/Guide/Regular_Expressions/Quantifiers)
  - : Вказують кількість символів чи виразів для збігу.
- [Екранування юнікодних полів](/uk/docs/Web/JavaScript/Guide/Regular_Expressions/Unicode_Property_Escapes)
  - : Розрізнення засноване на властивостях символів юнікоду. Наприклад, літери верхнього та нижнього регістру, математичні та пунктуаційні знаки.

Нижче наведено єдину таблицю всіх спеціальних символів, які можна використовувати в регулярних виразах:

<table class="standard-table">
  <caption>
    Спеціальні символи в регулярних виразах.
  </caption>
  <thead>
    <tr>
      <th scope="col">Символи / конструкції</th>
      <th scope="col">Відповідна стаття</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>\</code>, <code>.</code>, <code>\cX</code>, <code>\d</code>,
        <code>\D</code>, <code>\f</code>, <code>\n</code>, <code>\r</code>,
        <code>\s</code>, <code>\S</code>, <code>\t</code>, <code>\v</code>,
        <code>\w</code>, <code>\W</code>, <code>\0</code>, <code>\xhh</code>,
        <code>\uhhhh</code>, <code>\uhhhhh</code>, <code>[\b]</code>
      </td>
      <td>
        <p>
          <a
            href="/uk/docs/Web/JavaScript/Guide/Regular_Expressions/Character_Classes"
            >Класи символів</a
          >
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>^</code>, <code>$</code>, <code>x(?=y)</code>,
        <code>x(?!y)</code>, <code>(?&#x3C;=y)x</code>,
        <code>(?&#x3C;!y)x</code>, <code>\b</code>, <code>\B</code>
      </td>
      <td>
        <p>
          <a
            href="/uk/docs/Web/JavaScript/Guide/Regular_Expressions/Assertions"
            >Перевірки</a
          >
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>(x)</code>, <code>(?:x)</code>, <code>(?&#x3C;Name>x)</code>,
        <code>x|y</code>, <code>[xyz]</code>, <code>[^xyz]</code>,
        <code>\<em>Number</em></code>
      </td>
      <td>
        <p>
          <a
            href="/uk/docs/Web/JavaScript/Guide/Regular_Expressions/Groups_and_Ranges"
            >Групи та діапазони</a
          >
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>*</code>, <code>+</code>, <code>?</code>,
        <code>x{<em>n</em>}</code>, <code>x{<em>n</em>,}</code>,
        <code>x{<em>n</em>,<em>m</em>}</code>
      </td>
      <td>
        <p>
          <a
            href="/uk/docs/Web/JavaScript/Guide/Regular_Expressions/Quantifiers"
            >Квантори</a
          >
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>\p{<em>UnicodeProperty</em>}</code>,
        <code>\P{<em>UnicodeProperty</em>}</code>
      </td>
      <td>
        <a
          href="/uk/docs/Web/JavaScript/Guide/Regular_Expressions/Unicode_Property_Escapes"
          >Екранування поля Unicode</a
        >
      </td>
    </tr>
  </tbody>
</table>

> **Зауваження:** [Доступна також більша шпаргалка](/uk/docs/Web/JavaScript/Guide/Regular_Expressions/Cheatsheet) (зібрана з тих окремих статей).

### Екранування

Якщо потрібно вжити будь-який спеціальний вираз буквально (наприклад, шукаючи власне символ `"*"`), його потрібно екранувати шляхом додавання зворотного скосу перед ним.
Зокрема, щоб знайти літеру `"a"`, за якою слідує `"*"`, слідом за яким літера `"b"`, треба вжити патерн `/a\*b/`: зворотний скіс «екранує» `"*"`, роблячи її просто знаком і відбираючи спеціальне значення.

Аналогічно, якщо під час написання літералу регулярного виразу потрібно знайти збіг із символом скосу ("/"), слід його екранувати (інакше він означатиме кінець паттерну).
Для прикладу, щоб знайти рядок "/example/", за яким слідує одна чи більше букв алфавіту, слід використати паттерн `/\/example\/[a-z]+/i` — зворотна коса перед кожною косою робить їх просто символами.

Щоб знайти збіг зворотної косої буквально, слід її екранувати.
Наприклад, щоб знайти рядок "C:\\", де «C» може бути будь-якою літерою, слід використати паттерн `/[A-Z]:\\/` — перша зворотна коса екранує наступну після неї, тож вираз шукатиме буквально одну зворотну косу риску.

Використовуючи конструктор `RegExp` з рядковим літералом, пам'ятайте, що зворотна коса — це екранувальний символ в рядкових літералах. І щоб застосувати її в регулярному виразі, слід спершу її екранувати на рівні рядкового літерала. `/a\*b/` та `new RegExp("a\\*b")` створюють один і той самий вираз, який шукатиме літеру "a" з символом за нею "\*" і літерою "b" після них.

Якщо екранувальні рядки ще не входять в готовий паттерн, їх можна додати за допомогою {{jsxref('String.replace')}}:

```js
function escapeRegExp(string) {
  return string.replace(/[.*+?^${}()|[\]\\]/g, '\\$&'); // $& означає цілий рядок, який збігся з паттерном
}
```

Літера "g" після регулярних виразів — це опція або прапорець, який виконує глобальний пошук, перебираючи рядок цілком, і повертаючи всі можливі збіги.
Це пояснено в деталях нижче, в розділі [Поглиблений пошук з прапорцями](#advanced_searching_with_flags).

_Чому це не вбудовано всередину JavaScript?_ Була пропозиція додати таку функцію до RegExp, проте [TC39 її відхилив.](https://github.com/benjamingr/RegExp.escape/issues/37)

### Застосування дужок

Дужки навколо будь-якої частини паттерну регулярного виразу призводять до того, що ця частина знайденого підрядка буде збережена окремо. До збереженого підрядка можна потім знову звернутися і використати для інших цілей. Більше деталей є в розділі [Групи та діапазони](/uk/docs/Web/JavaScript/Guide/Regular_Expressions/Groups_and_Ranges#using_groups).

## Застосування регулярних виразів у JavaScript

Регулярні вирази з методами об'єкту {{jsxref("RegExp")}}, такими як {{jsxref("RegExp/test", "test()")}} і {{jsxref("RegExp/exec", "exec()")}}, а також із методами {{jsxref("String")}}: {{jsxref("String/match", "match()")}}, {{jsxref("String/replace", "replace()")}}, {{jsxref("String/search", "search()")}} і {{jsxref("String/split", "split()")}}.

| Метод                                                            | Опис                                                                                                                |
| ---------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| {{jsxref("RegExp.exec", "exec()")}}                              | Виконує пошук збігу в рядку. Повертає масив з інформацією або ж `null`, якщо збігів не знайдено.                    |
| {{jsxref("RegExp.test", "test()")}}                              | Перевіряє рядок на збіг. Повертає `true` або `false`.                                                               |
| {{jsxref("String.match", "match()")}}                            | Повертає масив, що містить всі знайдені збіги, включно з групами захоплення, або ж `null`, якщо збігів не знайдено. |
| {{jsxref("String.matchAll", "matchAll()")}}                      | Повертає ітератор, що містить всі знайдені збіги, включно з групами захоплення.                                     |
| {{jsxref("String.search", "search()")}}                          | Перевіряє рядок на наявність збігів. Повертає індекс збігу, або `-1`, якщо пошук завершився невдачею.               |
| {{jsxref("String.replace", "replace()")}}                        | Виконує пошук збігу в рядку, і заміняє знайдену частину рядка переданим рядком для заміни.                          |
| {{jsxref("String.replaceAll", "replaceAll()")}}                  | Виконує пошук всіх збігів у рядку, і заміняє знайдені частини рядка переданим рядком для заміни.                    |
| {{jsxref("String.split", "split()")}}                            | Використовує регулярний вираз або фіксований рядок для того, щоб розбити початковий рядок на масив підрядків.       |

Якщо потрібно визначити, чи паттерн присутній в рядку, використовуйте методи `test()` або `search()`. Для отримання докладнішої інформації (коштом повільнішого виконання) застосовуйте методи `exec()` чи `match()`.
Якщо використовується метод `exec()` чи `match()`, і знаходиться збіг, ці методи повертають масив, і оновлюють властивості пов'язаного об'єкта регулярного виразу, і також властивості глобального об'єкта `RegExp`. Якщо збіг знайти не вдалося, то метод `exec()` поверне `null` (який зрештою зводиться до `false`).

В наступному прикладі скрипт шукає збіги в рядку за допомогою методу `exec()`.

```js
var myRe = /d(b+)d/g;
var myArray = myRe.exec('cdbbdbsbz');
```

А в цьому скрипті — альтернативний варіант створення масиву `myArray`, на випадок якщо вам не потрібен доступ до властивостей самого регулярного виразу:

```js
var myArray = /d(b+)d/g.exec('cdbbdbsbz');
    // так само, як і з "cdbbdbsbz".match(/d(b+)d/g); однак,
    // "cdbbdbsbz".match(/d(b+)d/g) виводить Array [ "dbbd" ], в той час як
    // /d(b+)d/g.exec('cdbbdbsbz') виводить Array [ 'dbbd', 'bb', index: 1, input: 'cdbbdbsbz' ].
```

(Дивіться більше інформації цю різницю в поведінці у частині [Застосування прапорця глобального пошуку з `exec()`](#using_the_global_search_flag_with_exec).)

Якщо ж потрібно сконструювати регулярний вираз із рядка, ось іще одна альтернатива:

```js
var myRe = new RegExp('d(b+)d', 'g');
var myArray = myRe.exec('cdbbdbsbz');
```

В цих скриптах пошук збігів успішно завершується, повертає масив результатів і оновлює властивості, наведені в таблиці нижче:

<table class="standard-table">
  <caption>
    Результати виконання регулярних виразів.
  </caption>
  <thead>
    <tr>
      <th scope="col">Об'єкт</th>
      <th scope="col">Властивість або індекс</th>
      <th scope="col">Опис</th>
      <th scope="col">В цьому прикладі</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="4"><code>myArray</code></td>
      <td></td>
      <td>Рядок, що збігся, а також всі запам'ятовані підрядки.</td>
      <td><code>['dbbd', 'bb', index: 1, input: 'cdbbdbsbz']</code></td>
    </tr>
    <tr>
      <td><code>index</code></td>
      <td>Індекс позиції (від 0) збігу у вхідному рядку.</td>
      <td><code>1</code></td>
    </tr>
    <tr>
      <td><code>input</code></td>
      <td>Вхідний рядок.</td>
      <td><code>'cdbbdbsbz'</code></td>
    </tr>
    <tr>
      <td><code>[0]</code></td>
      <td>Символи з останнього збігу.</td>
      <td><code>'dbbd'</code></td>
    </tr>
    <tr>
      <td rowspan="2"><code>myRe</code></td>
      <td><code>lastIndex</code></td>
      <td>Індекс, з якого почнеться пошук наступного збігу.
        (Ця властивість встановлюється лише якщо регулярний вираз використовує опцію «g», описану в частині
        <a href="#advanced_searching_with_flags">Поглиблений пошук з прапорцями</a>.)
      </td>
      <td><code>5</code></td>
    </tr>
    <tr>
      <td><code>source</code></td>
      <td>
        Текст паттерну. Оновлюється в момент створення регулярного виразу, не виконання.
      </td>
      <td><code>'d(b+)d'</code></td>
    </tr>
  </tbody>
</table>

Як було показано у другому варіанті цього прикладу, можна використовувати регулярні вирази, створені об'єктним конструктором без присвоєння його змінній. Однак у цьому випадку кожний новий виклик створюватиме новий регулярний вираз. З цієї причини, якщо ця форма використовується без присвоєння виразу змінній, неможливо потім отримати доступ до властивостей цього виразу.
Наприклад, припустімо, у нас є такий скрипт:

```js
var myRe = /d(b+)d/g;
var myArray = myRe.exec('cdbbdbsbz');
console.log('Поле lastIndex має значення ' + myRe.lastIndex);

// "Поле lastIndex має значення 5"
```

Однак, якщо натомість у нас є такий скрипт:

```js
var myArray = /d(b+)d/g.exec('cdbbdbsbz');
console.log('Поле lastIndex має значення ' + /d(b+)d/g.lastIndex);

// "Поле lastIndex має значення 0"
```

Вирази `/d(b+)d/g` у двох інструкціях вище — це насправді різні об'єкти регулярного виразу, і тому вони містять різні значення їхньої властивості `lastIndex`. Якщо потрібно доступитися до властивостей регулярного виразу, створеного об'єктним конструктором, слід спершу присвоїти його змінній.

### Поглиблений пошук з опціями

Регулярні вирази мають необов'язкові опції, що дозволяє використовувати таку функціональність, як глобальний пошук чи пошук без врахування регістру літер. Ці опції можна використовувати окремо або разом, у будь-якому порядку, і вони входять в сам регулярний вираз.

| Прапорець | Опис                                                                                                                                         | Відповідна властивість                                                                                 |
| ---- | --------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| `d`  | Згенерувати індекси для збігів підрядків.                                                                                                                     | [`RegExp.prototype.hasIndices`](/uk/docs/Web/JavaScript/Reference/Global_Objects/RegExp/hasIndices) |
| `g`  | Глобальний пошук.                                                                                                                                      | [`RegExp.prototype.global`](/uk/docs/Web/JavaScript/Reference/Global_Objects/RegExp/global)         |
| `i`  | Пошук, нечутливий до регістру.                                                                                                                            | [`RegExp.prototype.ignoreCase`](/uk/docs/Web/JavaScript/Reference/Global_Objects/RegExp/ignoreCase) |
| `m`  | Багаторядковий пошук.                                                                                                                                  | [`RegExp.prototype.multiline`](/uk/docs/Web/JavaScript/Reference/Global_Objects/RegExp/multiline)   |
| `s`  | Дозволяє `.` позначати символи початку нового рядка.                                                                                                             | [`RegExp.prototype.dotAll`](/uk/docs/Web/JavaScript/Reference/Global_Objects/RegExp/dotAll)         |
| `u`  | "unicode"; сприймає паттерн як послідовність кодів юнікоду.                                                                                    | [`RegExp.prototype.unicode`](/uk/docs/Web/JavaScript/Reference/Global_Objects/RegExp/unicode)       |
| `y`  | Виконує «липкий» пошук, який починає пошук збігів з поточної позиції цільового рядка. Дивіться {{jsxref("RegExp.sticky", "sticky")}}. | [`RegExp.prototype.sticky`](/uk/docs/Web/JavaScript/Reference/Global_Objects/RegExp/sticky)         |

Щоб включити опцію («flag») в регулярний вираз, використовується такий синтаксис:

```js
var re = /pattern/flags;
```

або

```js
var re = new RegExp('pattern', 'flags');
```

Зауважте, що ці опції — це невідокремна частина регулярного виразу. Їх неможливо додати чи прибрати потім.

Наприклад, `re = /\w+\s/g` створює регулярний вираз, що шукає одну або більше літер, за якими слідує пробіл, і він виконує цей пошук по всьому рядку.

```js
var re = /\w+\s/g;
var str = 'fee fi fo fum';
var myArray = str.match(re);
console.log(myArray);

// ["fee ", "fi ", "fo "]
```

Можна замінити цей рядок:

```js
var re = /\w+\s/g;
```

на такий:

```js
var re = new RegExp('\\w+\\s', 'g');
```

і отримати такий самий результат.

Прапорець `m` використовується для вказання, що багаторядковий вхідний текст має сприйматись як декілька різних рядків. Якщо використано прапорець `m`, символи `^` і `$` позначають відповідно початок та кінець кожного рядка всередині вхідної стрічки замість початку і кінця стрічки в цілому.

#### Застосування прапорця глобального пошуку з exec()

Поведінка, що асоціюється з використанням прапорця `g` є дещо іншою, якщо використовується метод `.exec()`. Ролі "класу" та "аргументу" міняються місцями: у випадку з `.match()` клас (або тип даних) рядка володіє методом, а регулярний вираз — лише аргумент, тоді як у випадку з `.exec()` це сам регулярний вираз володіє методом, а рядок — просто аргумент. Порівняємо _`str.match(re)`_ із _`re.exec(str)`_. Прапорець `g` використовується з методом **`.exec()`** для отримання ітеративного виконання.

```js
var xArray; while(xArray = re.exec(str)) console.log(xArray);
// виводить:
// ["fee ", index: 0, input: "fee fi fo fum"]
// ["fi ", index: 4, input: "fee fi fo fum"]
// ["fo ", index: 7, input: "fee fi fo fum"]
```

## Приклади

> **Зауваження:** Декілька прикладів також доступні:
>
> - На довідникових сторінках для {{jsxref("RegExp.exec", "exec()")}}, {{jsxref("RegExp.test", "test()")}}, {{jsxref("String.match", "match()")}}, {{jsxref("String.matchAll", "matchAll()")}}, {{jsxref("String.search", "search()")}}, {{jsxref("String.replace", "replace()")}}, {{jsxref("String.split", "split()")}}
> - У статтях цих настанов: [класи символів](/uk/docs/Web/JavaScript/Guide/Regular_Expressions/Character_Classes), [перевірки](/uk/docs/Web/JavaScript/Guide/Regular_Expressions/Assertions), [групи та діапазони](/uk/docs/Web/JavaScript/Guide/Regular_Expressions/Groups_and_Ranges), [квантори](/uk/docs/Web/JavaScript/Guide/Regular_Expressions/Quantifiers), [екранування полів Unicode](/uk/docs/Web/JavaScript/Guide/Regular_Expressions/Unicode_Property_Escapes)

### Застосування спеціальних символів для перевірки вводу

В цьому прикладі користувач має ввести телефонний номер. Коли користувач натискає кнопку "Check", скрипт перевіряє правильність номера. Якщо номер коректний (збігається з послідовністю символів, заданою регулярним виразом), скрипт показує повідомлення з подякою користувачеві та підтвердженням номеру. Якщо номер некоректний, скрипт інформує користувача про те, що номер введено невірно.

Регулярний вираз шукає:

1. Початок рядку з даними: `^`
2. Далі три цифрових знаки `\d{3}` АБО `|` ліва дужка `\(` з трьома цифрами за нею `\d{3}`, закритими правою дужкою `\)`, і це все об'єднано в групу (без захоплення) `(?:)`
3. Далі один дефіс, коса риска, або десяткова крапка, захоплені в групу `()`
4. Далі іще три цифри `\d{3}`
5. Далі збіг, запам'ятований у першій захопленій групі `\1`
6. Далі іще чотири цифри `\d{4}`
7. І за ними кінець рядка з даними: `$`

Подія `click`, котра спрацьовує під час натискання користувачем клавіші <kbd>Enter</kbd> встановлює значення `phoneInput.value`.

#### HTML

```html
<p>
  Введіть ваш номер телефону (з кодом області) та натисність "Перевірити".
  <br>
  Очікуваний формат номера: ###-###-####.
</p>
<form action="#" onSubmit="return false">
  <input id="phone">
    <button onClick="testInfo(document.querySelector('#phone'));">Перевірити</button>
</form>
<p id="out"></p>
```

#### JavaScript

```js
var re = /^(?:\d{3}|\(\d{3}\))([-\/\.])\d{3}\1\d{4}$/;
function testInfo(phoneInput) {
  var OK = re.exec(phoneInput.value);
  var out = document.querySelector('#out');
  if (!OK) {
    out.textContent = `${phoneInput.value} не є телефонним номером з кодом області!`;
  } else {
    out.textContent = `Дякуємо, ваш телефонний номер — ${OK[0]}`;
  }
}
```

#### Результат

{{ EmbedLiveSample('Using_special_characters_to_verify_input') }}

## Інструменти

- [RegExr](https://regexr.com/)
  - : Онлайн-інструмент для вивчення, побудови та тестування регулярних виразів.
- [Regex tester](https://regex101.com/)
  - : Онлайн-інструмент для побудови та зневадження регулярних виразів
- [Regex visualizer](https://extendsclass.com/regex-tester.html)
  - : Візуальний онлайн-інструмент для тестування регулярних виразів.

{{PreviousNext("Web/JavaScript/Guide/Text_formatting", "Web/JavaScript/Guide/Indexed_collections")}}