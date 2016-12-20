# <a name="top"> Javascript

#### Содержание

1. [Основы](#1)
	- [Внешние скрипты, порядок исполнения](#1_1)
	- [Шесть типов данных, typeof](#1_2)
	- [Операторы сравнения и логические значения](#1_3)
	- [Побитовые операторы](#1_4)
	- [Взаимодействие с пользователем: alert, prompt, confirm](#1_5)
	- [Условные операторы: if, '?'](#1_6)
	- [Логические операторы](#1_7)
	- [Преобразование типов для примитивов](#1_8)
	- [Функции](#1_9)
	- [Функциональные выражения](#1_10)
	- [Именованные функциональные выражения](#1_11)
2. [Структуры данных](#2)
	- [Числа](#2_1)
	- [Строки](#2_2)
	- [Объекты как ассоциативные массивы](#2_3)
	- [Объекты: перебор свойств](#2_4)
	- [Объекты: передача по ссылке](#2_5)
	- [Массивы с числовыми индексами](#2_6)
	- [Массивы: методы](#2_7)
	- [Массив: перебирающие методы](#2_8)
	- [Псевдомассив аргументов "arguments"](#2_9)
	- [Дата и Время](#2_10)
3. [Документ и объекты страницы](#10)
	- [Окружение: DOM, BOM и JS] (#10_1)
	- [Дерево DOM] (#10_2)
	- [Навигация по DOM-элементам] (#10_3)
	- [Поиск: getElement* и querySelector*] (#10_4)
	- [Свойства узлов: тип, тег и содержимое] (#10_5)

## <a name="1"> Основы

### <a name="1_1"> Внешние скрипты, порядок исполнения.

1. Скрипты вставляются на страницу как текст в теге **\<script>**, либо как внешний файл через **\<script src="путь">\</script>**
2. Специальные атрибуты **async** и **defer** используются для того, чтобы пока грузится внешний скрипт – браузер показал остальную (следующую за ним) часть страницы. Без них этого не происходит.
3. Разница между **async** и **defer**: атрибут **defer** сохраняет относительную последовательность скриптов, а **async** – нет. Кроме того, **defer** всегда ждёт, пока весь HTML-документ будет готов, а **async** – нет.

[наверх](#top)

### <a name="1_2"> Шесть типов данных, typeof

1. Есть 5 «примитивных» типов: **number**, **string**, **boolean**, **null**, **undefined** и 6-й тип – объекты **object**.
2. Оператор **typeof x** позволяет выяснить, какой тип находится в x, возвращая его в виде строки.

### <a name="1_3"> Операторы сравнения и логические значения

1. В JavaScript есть логические значения **true** (истина) и **false** (ложь). Операторы сравнения возвращают их.
2. Строки сравниваются побуквенно.
3. Значения разных типов приводятся к числу при сравнении, за исключением строгого равенства === (!==).
4. Значения **null** и **undefined** равны == друг другу и не равны ничему другому. В других сравнениях (с участием >,<) их лучше не использовать, так как они ведут себя не как 0. **null** приводится к 0. **undefined** - к **NaN**, которое не равно ничему, даже самому себе.

[наверх](#top)

### <a name="1_4"> Побитовые операторы

1. Бинарные побитовые операторы: & | ^ << >> >>>.
2. Унарный побитовый оператор один: ~.
3. Как правило, битовое представление числа используется для:
  - Округления числа: (12.34^0) = 12, (\~~12.34) = 12.
  - Проверки на равенство -1: if (~n) { n не -1 }.
  - Упаковки нескольких битововых значений («флагов») в одно значение. Это экономит память и позволяет проверять наличие комбинации флагов одним оператором &.
  - Других ситуаций, когда нужны битовые маски.

### <a name="1_5"> Взаимодействие с пользователем: alert, prompt, confirm

1. **alert** выводит сообщение. (alert(сообщение);)
2. **prompt** выводит сообщение и ждёт, пока пользователь введёт текст, а затем возвращает введённое значение или null, если ввод отменён (CANCEL/Esc). (result = prompt(title, default);)
3. **confirm** выводит сообщение и ждёт, пока пользователь нажмёт «OK» или «CANCEL» и возвращает true/false. (result = confirm(question);)

[наверх](#top)

### <a name="1_6"> Условные операторы: if, '?'

В логическом контексте:
	
- Число 0, пустая строка "", null и undefined, а также NaN являются false,
- Остальные значения – true.

### <a name="1_7"> Логические операторы

Логический оператор возвращает то значение, на котором остановились вычисления. Причём, не преобразованное к логическому типу.

[наверх](#top)

### <a name="1_8"> Преобразование типов для примитивов

В **JavaScript** есть три преобразования:

1. Строковое: **String(value)** – в строковом контексте или при сложении со строкой. Работает очевидным образом.
2. Численное: **Number(value)** – в численном контексте, включая унарный плюс +value. Происходит при сравнении разных типов, кроме строгого равенства.
  - undefined		-	NaN
  - null				-	0
  - true / false	-	1 / 0
  - Строка			-	Пробельные символы по краям обрезаются.
  Далее, если остаётся пустая строка, то 0, иначе из непустой строки "считывается" число, при ошибке результат NaN.
3. Логическое: **Boolean(value)** – в логическом контексте, можно также сделать двойным НЕ: **!!value**.

Особым случаем является проверка равенства с **null** и **undefined**. Они равны друг другу, но не равны чему бы то ни было ещё, этот случай прописан особо в спецификации.

[наверх](#top)

### <a name="1_9"> Функции

Объявление функции имеет вид:
```javascript
function имя(параметры, через, запятую) {
  код функции
}
```

- Передаваемые значения копируются в параметры функции и становятся локальными переменными.
- Параметры функции копируются в её локальные переменные.
- Можно объявить новые локальные переменые при помощи **var**.
- Значение возвращается оператором **return ...**.
- Вызов **return** тут же прекращает функцию.
- Если **return;** вызван без значения, или функция завершилась без **return**, то её результат равен **undefined**.

[наверх](#top)

### <a name="1_10"> Функциональные выражения

Функции в JavaScript являются значениями. Их можно присваивать, передавать, создавать в любом месте кода.

- Если функция объявлена в основном потоке кода, то это **Function Declaration**.
- Если функция создана как часть выражения, то это **Function Expression**.

```javascript
// Function Expression
var f = function() { ... }

// Function Declaration
function f() { ... }
```
Существует ещё один способ создания функции, который используется очень редко, но упомянем и его для полноты картины.

Он позволяет создавать функцию полностью «на лету» из строки, вот так:

```javascript
var sum = new Function('a,b', ' return a+b; ');

var result = sum(1, 2);
alert( result ); // 3
```

То есть, функция создаётся вызовом **new Function(params, code)**

[наверх](#top)

### <a name="1_11"> Именованные функциональные выражения

Если функция задана как Function Expression, ей можно дать имя.

Оно будет доступно только внутри функции (кроме IE8-).

Это имя предназначено для надёжного рекурсивного вызова функции, даже если она записана в другую переменную.

Обратим внимание, что с Function Declaration так поступить нельзя. Такое «специальное» внутреннее имя функции задаётся только в синтаксисе Function Expression.

[наверх](#top)

## <a name="2"> Структуры данных

### <a name="2_1"> Числа

1. Числа могут быть записаны в шестнадцатиричной, восьмеричной системе, а также «научным» способом.
2. В JavaScript существует числовое значение бесконечность **Infinity**.
3. Ошибка вычислений дает **NaN**.
Арифметические и математические функции преобразуют строку в точности в число, игнорируя начальные и конечные пробелы.
Функции **parseInt/parseFloat** делают числа из строк, которые начинаются с числа.
4. Есть четыре способа округления: **Math.floor**, **Math.round**, **Math.ceil** и битовый оператор. Для округления до нужного знака используйте **+n.toFixed(p)** или трюк с умножением и делением на 10 в степени p.
5. Дробные числа дают ошибку вычислений. При необходимости ее можно отсечь округлением до нужного знака.
6. Случайные числа от 0 до 1 генерируются с помощью **Math.random()**, остальные – преобразованием из них.

[наверх](#top)

### <a name="2_2"> Строки

1. Строки в JavaScript имеют внутреннюю кодировку Юникод. При написании строки можно использовать специальные символы, например **\n** и вставлять юникодные символы по коду.
2. Мы познакомились со свойством **length** и методами **charAt**, **toLowerCase/toUpperCase**, **substring/substr/slice** (предпочтителен **slice**). Есть и другие методы, например **trim** обрезает пробелы с начала и конца строки, **split** получает массив из строки.
3. Строки сравниваются побуквенно. Поэтому если число получено в виде строки, то такие числа могут сравниваться некорректно, нужно преобразовать его к типу **number**.
4. При сравнении строк следует иметь в виду, что буквы сравниваются по их кодам. Поэтому большая буква меньше маленькой, а буква **ё** вообще вне основного алфавита.
5. Для правильного сравнения существует целый стандарт ECMA 402. Это не такое простое дело, много языков и много правил. Он поддерживается во всех современных браузерах, кроме IE10-. Такое сравнение работает через вызов **str1.localeCompare(str2)**.

[наверх](#top)

### <a name="2_3"> Объекты как ассоциативные массивы

Объекты – это ассоциативные массивы с дополнительными возможностями:

1. Доступ к элементам осуществляется:
	- Напрямую по ключу obj.prop = 5
	- Через переменную, в которой хранится ключ:
	```javascript
	var key = "prop";
	obj[key] = 5
	```
2. Удаление ключей: **delete obj.name**.
3. Существование свойства может проверять оператор **in**: if ("prop" in obj), как правило, работает и просто сравнение if (obj.prop !== undefined).

[наверх](#top)

### <a name="2_4"> Объекты: перебор свойств

1. Цикл по ключам: **for (key in obj)**.
2. Порядок перебора соответствует порядку объявления для нечисловых ключей, а числовые – сортируются (в современных браузерах).
3. Если нужно, чтобы порядок перебора числовых ключей соответствовал их объявлению в объекте, то используют трюк: числовые ключи заменяют на похожие, но содержащие не только цифры. Например, добавляют в начало +, а потом, в процессе обработки, преобразуют такие ключи в числа.

### <a name="2_5"> Объекты: передача по ссылке

Объект присваивается и копируется «по ссылке». То есть, в переменной хранится не сам объект а, условно говоря, адрес в памяти, где он находится.

1. Если переменная-объект скопирована или передана в функцию, то копируется именно эта ссылка, а объект остаётся один в памяти.
2. Это – одно из ключевых отличий объекта от примитива (числа, строки…), который при присвоении как раз копируется «по значению», то есть полностью.

[наверх](#top)

### <a name="2_6"> Массивы с числовыми индексами

Массивы существуют для работы с упорядоченным набором элементов.

Объявление:

```javascript
// предпочтительное
var arr = [элемент1, элемент2...];

// new Array
var arr = new Array(элемент1, элемент2...);
```

При этом **new Array(число)** создаёт массив заданной длины, без элементов. Чтобы избежать ошибок, предпочтителен первый синтаксис.

Свойство **length** – длина массива. Если точнее, то последний индекс массива плюс 1. Если её уменьшить вручную, то массив укоротится. Если **length** больше реального количества элементов, то отсутствующие элементы равны **undefined**.

Массив можно использовать как очередь или стек.

Операции с концом массива:

- **arr.push(элемент1, элемент2...)** добавляет элементы в конец.
- **var elem = arr.pop()** удаляет и возвращает последний элемент.

Операции с началом массива:

- **arr.unshift(элемент1, элемент2...)** добавляет элементы в начало.
- **var elem = arr.shift()** удаляет и возвращает первый элемент.

Эти операции перенумеровывают все элементы, поэтому работают медленно.

[наверх](#top)

### <a name="2_7"> Массивы: методы

1. **push/pop**, **shift/unshift**, **splice** – для добавления и удаления элементов.
2. **join/split** – для преобразования строки в массив и обратно.
3. **slice** – копирует участок массива.
4. **splice** - вставка, удаление.
5. **sort** – для сортировки массива. Если не передать функцию сравнения – сортирует элементы как строки.
6. **reverse** – меняет порядок элементов на обратный.
7. **concat** – объединяет массивы.
8. **indexOf/lastIndexOf** – возвращают позицию элемента в массиве (не поддерживается в IE8-).
9. **Object.keys(obj)** - свойства объекта в виде массива.

[наверх](#top)

### <a name="2_8"> Массив: перебирающие методы

1. **forEach** – для перебора массива.
2. **filter** – для фильтрации массива.
3. **every/some** – для проверки массива.
4. **map** – для трансформации массива в массив.
5. **reduce/reduceRight** – для прохода по массиву с вычислением значения.

Во многих ситуациях их использование позволяет написать код короче и понятнее, чем обычный перебор через **for**.

### <a name="2_9"> Псевдомассив аргументов "arguments"

1. Полный список аргументов, с которыми вызвана функция, доступен через **arguments**.
2. Это псевдомассив, то есть объект, который похож на массив, в нём есть нумерованные свойства и **length**, но методов массива у него нет.
3. Для указания аргументов по умолчанию, в тех случаях, когда они заведомо не **false**, удобен оператор **||**.

В тех случаях, когда возможных аргументов много и, в особенности, когда большинство их имеют значения по умолчанию, вместо работы с **arguments** организуют передачу данных через объект, который как правило называют **options**.

Возможен и гибридный подход, при котором первый аргумент обязателен, а второй – **options**, который содержит всевозможные дополнительные параметры:

```javascript
function showMessage(text, options) {
  // показать сообщение text, настройки показа указаны в options
}
```

[наверх](#top)

### <a name="2_10"> Дата и Время

1. Дата и время представлены в JavaScript одним объектом: **Date**. Создать «только время» при этом нельзя, оно должно быть с датой. Список методов **Date** вы можете найти в справочнике Date или выше.
2. Отсчёт месяцев начинается с нуля.
3. Отсчёт дней недели (для **getDay()**) тоже начинается с нуля (и это воскресенье).
4. Объект **Date** удобен тем, что автокорректируется. Благодаря этому легко сдвигать даты.
5. При преобразовании к числу объект **Date** даёт количество миллисекунд, прошедших с **1 января 1970 UTC**. Побочное следствие – даты можно вычитать, результатом будет разница в миллисекундах.
6. Для получения текущей даты в миллисекундах лучше использовать **Date.now()**, чтобы не создавать лишний объект Date (кроме IE8-)
7. Для бенчмаркинга лучше использовать **performance.now()** (кроме IE9-), он в 1000 раз точнее.

[наверх](#top)

## <a name="10"></a> Документ и объекты страницы 

### <a name="10_1"></a> Окружение: DOM, BOM и JS

![](https://learn.javascript.ru/article/browser-environment/windowObjects@2x.png)

[наверх](#top)

### <a name="10_2"></a> Дерево DOM

1. DOM-модель – это внутреннее представление HTML-страницы в виде дерева.
2. Все элементы страницы, включая теги, текст, комментарии, являются узлами DOM.
3. У элементов DOM есть свойства и методы, которые позволяют изменять их.

[наверх](#top)

### <a name="10_3"></a> Навигация по DOM-элементам

![](https://learn.javascript.ru/article/traversing-dom/dom-links@2x.png)
![](https://learn.javascript.ru/article/traversing-dom/dom-links-elements@2x.png)

[наверх](#top)

### <a name="10_4"></a> Поиск: getElement* и querySelector*

Есть 6 основных методов поиска элементов DOM:

- getElementById
- getElementsByName
- getElementsByTagName
- getElementsByClassName
- querySelector
- querySelectorAll

Кроме того:

- Есть метод **elem.matches(css)**, который проверяет, удовлетворяет ли элемент CSS-селектору. Он поддерживается большинством браузеров в префиксной форме **(ms, moz, webkit)**.
- Метод **elem.closest(css)** ищет ближайший элемент выше по иерархии DOM, подходящий под CSS-селектор css. Сам элемент тоже включается в поиск.

[наверх](#top)

### <a name="10_5"></a> Свойства узлов: тип, тег и содержимое

![](https://learn.javascript.ru/article/basic-dom-node-properties/hierarchy.png)

Основные свойства DOM-узлов:

1. **nodeType**
Тип узла. Самые популярные типы: "1" – для элементов и "3" – для текстовых узлов. Только для чтения.
2. **nodeName/tagName**
Название тега заглавными буквами. nodeName имеет специальные значения для узлов-неэлементов. Только для чтения.
3. **innerHTML**
Внутреннее содержимое узла-элемента в виде HTML. Можно изменять.
4. **outerHTML**
Полный HTML узла-элемента. При записи в elem.outerHTML переменная elem сохраняет старый узел.
5. **nodeValue/data**
Содержимое текстового узла или комментария. Свойство nodeValue также определено и для других типов узлов. Можно изменять. На некоторых узлах, где data нет, nodeValue есть и имеет значение null, поэтому лучше использовать data.
6. **textContent**
Содержит только текст внутри элемента, за вычетом всех тегов. Можно использовать для защиты от вставки произвольного HTML кода
7. Свойство и атрибут **hidden**
Скрыть элемент можно с помощью установки свойства hidden в true или с помощью атрибута
8. Узлы DOM также имеют другие свойства, в зависимости от тега. Например, у **INPUT** есть свойства **value** и **checked**, а у **A** есть **href** и т.д. Мы рассмотрим их далее.

[наверх](#top)
