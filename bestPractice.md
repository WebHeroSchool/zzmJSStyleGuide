# JSBestStyleGuide

### Содержание:
1. [Глобальные переменные](#global)
2. [Локальные переменные](#local)
3. [Объявления сверху](#naming)
4. [Инициализация переменных](#initialize)
5. [Объявление объектов](#declare)
6. [new Object()](#newObj)
7. [Автоматическое преобразование типов](#convers)
8. [Строгое сравнение](#comparison)
9. [Параметры по умолчанию](#default)
10. [Switch](#switch)

---
## <a name=#global>1. Глобальные переменные</a>

Минимизируйте использование глобальных переменных.
Это включает в себя все типы данных, объекты и функции.
Глобальные переменные и функции могут быть перезаписаны другими скриптами.
Вместо этого используйте локальные переменные и узнайте, как использовать `замыкания`.

---
## <a name=#local>2. Локальные переменные</a>

Все переменные, используемые в функции, должны быть объявлены как **локальные** переменные.
Локальные переменные **должны** быть объявлены с `var` ключевым словом или `let` ключевым словом, иначе они станут глобальными переменными.

Строгий режим не допускает необъявленных переменных.

---
## <a name=#naming>3. Объявления сверху</a>

Хорошей практикой написания кода является размещение всех объявлений в начале каждого скрипта или функции.

Это позволяет:
- Сделать код чище
- Предоставить единственное место для поиска локальных переменных
- Облегчить избежание нежелательных глобальных переменных
- Уменьшить возможность нежелательных повторных объявлений

``` js
// Declare at the beginning
var firstName, lastName, price, discount, fullPrice;

// Use later
firstName = "John";
lastName = "Doe";

price = 19.90;
discount = 0.10;

fullPrice = price * 100 / discount;
```
Это также относится к переменным цикла:
```js
// Declare at the beginning
var i;

// Use later
for (i = 0; i < 5; i++) {
```

---
## <a name=#initialize>4. Инициализация переменных</a>

Хорошей практикой программирования является инициализация переменных при их объявлении.

Это позволяет:
- Сделать код чище
- Предоставить единственное место для инициализации переменных
- Избежать неопределенных значений

```js
// Declare and initiate at the beginning
var firstName = "",
lastName = "",
price = 0,
discount = 0,
fullPrice = 0,
myArray = [],
myObject = {};
```

---
## <a name=#declare>5. Объявление объектов</a>

Никогда не объявляйте числовые, строковые или логические объекты.
Всегда обрабатывайте числа, строки или логические значения как примитивные значения. Не как объекты.

Объявление этих типов как объектов замедляет скорость выполнения и вызывает неприятные побочные эффекты:

```js
var x = "John";             
var y = new String("John");
(x === y) // is false because x is a string and y is an object.
```
Или еще хуже
```js
var x = new String("John");             
var y = new String("John");
(x == y) // is false because you cannot compare objects.
```

---
## <a name=#newObj>6. new Object()</a>

Не используйте new Object()
- Используйте `{}` вместо `new Object()`
- Используйте `""` вместо `new String()`
- Используйте `0` вместо `new Number()`
- Используйте `false` вместо `new Boolean()`
- Используйте `[]` вместо `new Array()`
- Используйте `/()/` вместо `new RegExp()`
- Используйте `function (){}` вместо `new Function()`

```js
var x1 = {};           // new object
var x2 = "";           // new primitive string
var x3 = 0;            // new primitive number
var x4 = false;        // new primitive boolean
var x5 = [];           // new array object
var x6 = /()/;         // new regexp object
var x7 = function(){}; // new function object
```

---
## <a name=#convers>7. Автоматическое преобразование типов</a>
Остерегайтесь автоматических преобразований типов.

Помните, что числа могут быть случайно преобразованы в строки или `NaN`(не число).JavaScript слабо типизирован. Переменная может содержать разные типы данных и так же может изменять свой тип данных:
```js
var x = "Hello";     // typeof x is a string
x = 5;               // changes typeof x to a number
```
При выполнении математических операций JavaScript может преобразовывать числа в строки:
```js
var x = 5 + 7;       // x.valueOf() is 12,  typeof x is a number
var x = 5 + "7";     // x.valueOf() is 57,  typeof x is a string
var x = "5" + 7;     // x.valueOf() is 57,  typeof x is a string
var x = 5 - 7;       // x.valueOf() is -2,  typeof x is a number
var x = 5 - "7";     // x.valueOf() is -2,  typeof x is a number
var x = "5" - 7;     // x.valueOf() is -2,  typeof x is a number
var x = 5 - "x";     // x.valueOf() is NaN, typeof x is a number
```
Вычитание строки из строки не приводит к ошибке, но возвращает NaN(не число):
```js
"Hello" - "Dolly"    // returns NaN
```

---
## <a name=#comparison>8. Строгое сравнение</a>

Используйте `===` Сравнение

Оператор `==` сравнения всегда преобразуется (в соответствующие типы) перед сравнением.

Оператор `===` заставляет сравнивать значения и тип:

```js
0 == "";        // true
1 == "1";       // true
1 == true;      // true

0 === "";       // false
1 === "1";      // false
1 === true;     // false
```

---
## <a name=#default>9. Параметры по умолчанию</a>

Используйте параметры по умолчанию.

Если функция вызывается с отсутствующим аргументом, устанавливается значение отсутствующего аргумента `undefined`.
Неопределенные значения могут нарушить ваш код. Это хорошая привычка назначать значения по умолчанию для аргументов.

```js
function myFunction(x, y) {
  if (y === undefined) {
    y = 0;
  }
}
```

---
## <a name=#switch>10. Switch</a>

Всегда заканчивайте свои инструкции `switch` значением по умолчанию `default`. Даже если вы думаете, что в этом нет никакой необходимости.

```js
switch (new Date().getDay()) {
  case 0:
    day = "Sunday";
    break;
  case 1:
    day = "Monday";
    break;
  case 2:
    day = "Tuesday";
    break;
  case 3:
    day = "Wednesday";
    break;
  case 4:
    day = "Thursday";
    break;
  case 5:
    day = "Friday";
    break;
  case 6:
    day = "Saturday";
    break;
  default:
    day = "Unknown";
}
```