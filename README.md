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
	- [Атрибуты и DOM-свойства] (#10_6)
	- [Методы contains и compareDocumentPosition] (#10_7)
	- [Добавление и удаление узлов] (#10_8)
	- [Мультивставка: insertAdjacentHTML и DocumentFragment] (#10_9)
	- [Стили, getComputedStyle] (#10_10)
	- [Размеры и прокрутка элементов] (#10_11)
	- [Размеры и прокрутка страницы] (#10_12)
	- [Координаты в окне и документе] (#10_13)
4. [Основы работы с событиями] (#12)
	- [Введение в браузерные события] (#12_1)
	- [Порядок обработки событий] (#12_2)
	- [Объект события] (#12_3)
	- [Всплытие и перехват] (#12_4)
	- [Делегирование событий] (#12_5)
	- [Приём проектирования "поведение"] (#12_6)
	- [Действия браузера по умолчанию] (#12_7)
	- [Генерация событий на элементах] (#12_8)

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

### <a name="10_6"></a> Атрибуты и DOM-свойства

- Атрибуты – это то, что написано в HTML.
- Свойство – это то, что находится в свойстве DOM-объекта.

Доступ к атрибутам осуществляется при помощи стандартных методов:

- **elem.hasAttribute(name)** – проверяет наличие атрибута
- **elem.getAttribute(name)** – получает значение атрибута
- **elem.setAttribute(name, value)** – устанавливает атрибут
- **elem.removeAttribute(name)** – удаляет атрибут
- **elem.attributes** - содержит псевдо-массив объектов типа **Attr**


- **className**
- **classList**
	- **elem.classList.contains("class")** – возвращает **true/false**, в зависимости от того, есть ли у элемента класс class.
	- **elem.classList.add/remove("class")** – добавляет/удаляет класс class
	- **elem.classList.toggle("class")** – если класса class нет, добавляет его, если есть – удаляет.


Синхронизация между атрибутами и свойствами:

- Стандартные свойства и атрибуты синхронизируются: установка атрибута автоматически ставит свойство DOM. Некоторые свойства синхронизируются в обе стороны.
- Бывает так, что свойство не совсем соответствует атрибуту. Например, «логические» свойства вроде **checked**, **selected** всегда имеют значение **true/false**, а в атрибут можно записать произвольную строку.

Нестандартные атрибуты:

- Нестандартный атрибут (если забыть глюки старых IE) никогда не попадёт в свойство, так что для кросс-браузерного доступа к нему нужно обязательно использовать **getAttribute**.
- Атрибуты, название которых начинается с **data-**, можно прочитать через **dataset**. Эта возможность не поддерживается IE10-.

[наверх](#top)

### <a name="10_7"> Методы contains и compareDocumentPosition

- Для проверки, является ли один узел предком другого, достаточно метода **nodeA.contains(nodeB)**.
- Для расширенной проверки на предшествование есть метод **nodeA.compareDocumentPosition(nodeB)**.

### <a name="10_8"> Добавление и удаление узлов

Методы для создания узлов:

- **document.createElement(tag)** – создает элемент
- **document.createTextNode(value)** – создает текстовый узел
- **elem.cloneNode(deep)** – клонирует элемент, если **deep == true**, то со всеми потомками, если **false** – без потомков.

Вставка и удаление узлов:

- **parent.appendChild(elem)**
- **parent.insertBefore(elem, nextSibling)**
- **parent.removeChild(elem)**
- **parent.replaceChild(newElem, elem)**

Все эти методы возвращают **elem**.

[наверх](#top)

### <a name="10_9"> Мультивставка: insertAdjacentHTML и DocumentFragment

- Манипуляции, меняющие структуру DOM (вставка, удаление элементов), как правило, быстрее с отдельным маленьким узлом, чем с большим DOM, который находится в документе.  
Конкретная разница зависит от внутренней реализации DOM в браузере.

- Семейство методов для вставки HTML/элемента/текста в произвольное место документа:

	- **elem.insertAdjacentHTML(where, html)**
	- **elem.insertAdjacentElement(where, node)**
	- **elem.insertAdjacentText(where, text)**

- **DocumentFragment** позволяет минимизировать количество вставок в большой живой DOM. Эта оптимизация особо эффективна в старых браузерах, в новых эффект от неё меньше или наоборот отрицательный.  
Элементы сначала вставляются в него, а потом – он вставляется в DOM. При вставке **DocumentFragment** «растворяется», и вместо него вставляются содержащиеся в нём узлы.  
**DocumentFragment**, в отличие от **insertAdjacent**, работает с коллекцией DOM-узлов.  
**var fragment = document.createDocumentFragment()**

- Современные методы, работают с любым количеством узлов и текста, желателен полифилл:

	- **append/prepend** – вставка в конец/начало.
	- **before/after** – вставка после/перед.
	- **replaceWith** – замена.
	
[наверх](#top)

### <a name="10_10"> Стили, getComputedStyle

Все DOM-элементы предоставляют следующие свойства.

- Свойство **style** – это объект, в котором CSS-свойства пишутся **вотТакВот**. Чтение и изменение его свойств – это, по сути, работа с компонентами атрибута **style**.

- **style.cssText** – строка стилей для чтения или записи. Аналог полного атрибута **style**.

- Свойство **currentStyle**(IE8-) и метод **getComputedStyle** (IE9+, стандарт) позволяют получить реальное, применённое сейчас к элементу свойство стиля с учётом CSS-каскада и браузерных стилей по умолчанию.

При этом **currentStyle** возвращает значение из CSS, до окончательных вычислений, а **getComputedStyle** – окончательное, непосредственно применённое к элементу (как правило).

[наверх](#top)

### <a name="10_11"> Размеры и прокрутка элементов

У элементов есть следующие метрики:

- **offsetParent** – «родитель по дереву рендеринга» – ближайшая ячейка таблицы, body для статического позиционирования или ближайший позиционированный элемент для других типов позиционирования.
- **offsetLeft/offsetTop** – позиция в пикселях левого верхнего угла блока, относительно его **offsetParent**.
- **offsetWidth/offsetHeight** – «внешняя» ширина/высота блока, включая рамки.
- **clientLeft/clientTop** – отступ области содержимого от левого-верхнего угла элемента. Если операционная система располагает вертикальную прокрутку справа, то равны ширинам левой/верхней рамки, если же слева (ОС на иврите, арабском), то clientLeft включает в себя прокрутку.
- **clientWidth/clientHeight** – ширина/высота содержимого вместе с полями padding, но без полосы прокрутки.
- **scrollWidth/scrollHeight** – ширина/высота содержимого, включая прокручиваемую область. Включает в себя padding и не включает полосы прокрутки.
- **scrollLeft/scrollTop** – ширина/высота прокрученной части документа, считается от верхнего левого угла.

Все свойства, доступны только для чтения, кроме **scrollLeft/scrollTop**. Изменение этих свойств заставляет браузер прокручивать элемент.

[наверх](#top)

### <a name="10_12"> Размеры и прокрутка страницы

**Размеры:**

- Для получения размеров видимой части окна: **document.documentElement.clientWidth/Height**
- Для получения размеров страницы с учётом прокрутки:

	```javascript
	var scrollHeight = Math.max(
	  document.body.scrollHeight, document.documentElement.scrollHeight,
	  document.body.offsetHeight, document.documentElement.offsetHeight,
	  document.body.clientHeight, document.documentElement.clientHeight
	);
	```

**Прокрутка окна:**

- Прокрутку окна можно получить как **window.pageYOffset** (для горизонтальной – **window.pageXOffset**) везде, кроме IE8-.
- На всякий случай – вот самый кросс-браузерный способ, учитывающий IE7- в том числе:

	```javascript
	var html = document.documentElement;
	var body = document.body;

	var scrollTop = html.scrollTop || body && body.scrollTop || 0;
	scrollTop -= html.clientTop; // в IE7- <html> смещён относительно (0,0)
	```

- Установить прокрутку можно при помощи специальных методов:

	- **window.scrollTo(pageX,pageY)** – абсолютные координаты,
	- **window.scrollBy(x,y)** – прокрутить относительно текущего места.
	- **elem.scrollIntoView(top)** – прокрутить, чтобы элемент elem стал виден.

[наверх](#top)

### <a name="10_13"> Координаты в окне и документе

- **elem.getBoundingClientRect()** - возвращает координаты элемента относительно окна.
- Относительно документа **document** – добавляем прокрутку.
- Относительно экрана **screen** – можно узнать координаты браузера, но не элемента. **window.screenX**, **window.screenY**
- **document.elementFromPoint(x, y)** - возвращает элемент, который находится на координатах **(x, y)** относительно окна. Для координат вне окна **elementFromPoint** возвращает **null**.

[наверх](#top)

## <a name="12"> Основы работы с событиями

### <a name="12_1"> Введение в браузерные события

Есть три способа назначения обработчиков событий:

- Атрибут HTML: **onclick="..."**.
- Свойство: **elem.onclick = function**.
- Специальные методы:
	- Современные: **elem.addEventListener( событие, handler[, phase])**, удаление через **removeEventListener**.
	- Для старых IE8-: **elem.attachEvent( on+событие, handler )**, удаление через **detachEvent**.

Сравнение **addEventListener** и **onclick**:

- Некоторые события можно назначить только через **addEventListener**.
- Метод **addEventListener** позволяет назначить много обработчиков на одно событие.
- Обработчик, назначенный через **onclick**, проще удалить или заменить.
- Метод **onclick** кросс-браузерный.

[наверх](#top)

### <a name="12_2"> Порядок обработки событий

- **JavaScript** выполняется в едином потоке. Современные браузеры позволяют порождать подпроцессы **Web Workers**, они выполняются параллельно и могут отправлять/принимать сообщения, но не имеют доступа к **DOM**.
- Обычно события становятся в очередь и обрабатываются в порядке поступления, асинхронно, независимо друг от друга.
Синхронными являются вложенные события, инициированные из кода.
- Чтобы сделать событие гарантированно асинхронным, используется вызов через **setTimeout(func, 0)**.

Отложенный вызов через **setTimeout(func, 0)** используется не только в событиях, а вообще – всегда, когда мы хотим, чтобы некая функция **func** сработала после того, как текущий скрипт завершится.

[наверх] (#top)

### <a name="12_3"> Объект события

- Объект события содержит ценную информацию о деталях события.
- Он передается первым аргументом **event** в обработчик для всех браузеров, кроме IE8-, в которых используется глобальная переменная **window.event**.

[наверх](#top)

### <a name="12_4"> Всплытие и перехват

Алгоритм:

- При наступлении события – элемент, на котором оно произошло, помечается как «целевой» (**event.target**).
- Далее событие сначала двигается вниз от корня документа к **event.target**, по пути вызывая обработчики, поставленные через **addEventListener(...., true)**.
- Далее событие двигается от **event.target** вверх к корню документа, по пути вызывая обработчики, поставленные через **on-** и **addEventListener(...., false)**.

Каждый обработчик имеет доступ к свойствам события:

- **event.target** – самый глубокий элемент, на котором произошло событие.
- **event.currentTarget (=this)** – элемент, на котором в данный момент сработал обработчик (до которого «доплыло» событие).
- **event.eventPhase** – на какой фазе он сработал (погружение =1, всплытие = 3).

Любой обработчик может остановить событие вызовом **event.stopPropagation()**, но делать это не рекомендуется, так как в дальнейшем это событие может понадобиться, иногда для самых неожиданных вещей.

[наверх](#top)

### <a name="12_5"> Делегирование событий

Алгоритм:

- Вешаем обработчик на контейнер.
- В обработчике: получаем **event.target**.
- В обработчике: если **event.target** или один из его родителей в контейнере (**this**) – интересующий нас элемент – обработать его.

Зачем использовать:

- Упрощает инициализацию и экономит память: не нужно вешать много обработчиков.
- Меньше кода: при добавлении и удалении элементов не нужно ставить или снимать обработчики.
- Удобство изменений: можно массово добавлять или удалять элементы путём изменения **innerHTML**.

Конечно, у делегирования событий есть свои ограничения.

- Во-первых, событие должно всплывать. Нельзя, чтобы какой-то промежуточный обработчик вызвал **event.stopPropagation()** до того, как событие доплывёт до нужного элемента.
- Во-вторых, делегирование создает дополнительную нагрузку на браузер, ведь обработчик запускается, когда событие происходит в любом месте контейнера, не обязательно на элементах, которые нам интересны. Но обычно эта нагрузка настолько пустяковая, её даже не стоит принимать во внимание.

[наверх](#top)

### <a name="12_6">  Приём проектирования "поведение"

Приём проектирования «поведение» состоит из двух частей:

- Элементу ставится атрибут, описывающий его поведение.
- При помощи делегирования ставится обработчик на документ, который ловит все клики и, если элемент имеет нужный атрибут, производит нужное действие.

[наверх](#top)

### <a name="12_7"> Действия браузера по умолчанию

- Браузер имеет встроенные действия при ряде событий – переход по ссылке, отправка формы и т.п. Как правило, их можно отменить.
- Есть два способа отменить действие по умолчанию: первый – использовать **event.preventDefault()** (IE8-: **event.returnValue=false**), второй – **return false** из обработчика. Второй способ работает только если обработчик назначен через onсобытие.

[наверх](#top)

### <a name="12_8"> Генерация событий на элементах

- Все браузеры, кроме IE9-11, позволяют генерировать любые события, следуя стандарту DOM4.
	```javascript
	var event = new Event(тип события[, флаги]);
	```
	Где:

	- Тип события – может быть как своим, так и встроенным, к примеру **"click"**.
	- Флаги – объект вида **{ bubbles: true/false, cancelable: true/false }**, где свойство **bubbles** указывает, всплывает ли событие, а **cancelable** – можно ли отменить действие по умолчанию.
	- Флаги по умолчанию: **{bubbles: false, cancelable: false}**.

	Затем, чтобы инициировать событие, запускается **elem.dispatchEvent(event).**
- В IE9+ поддерживается более старый стандарт
	
	Объект события создаётся вызовом document.createEvent:
	```javascript
	var event = document.createEvent(eventInterface);
	var event = document.createEvent("Event");
	```
	
	Далее событие нужно инициализировать:
	```javascript
	event.initEvent(type, boolean bubbles, boolean cancelable);
	```
	
[наверх](#top)

[наверх](#top)

[наверх](#top)

[наверх](#top)

[наверх](#top)

[наверх](#top)
