# Javascript

### Внешние скрипты, порядок исполнения.

1. Скрипты вставляются на страницу как текст в теге **\<script>**, либо как внешний файл через **\<script src="путь">\</script>**
2. Специальные атрибуты **async** и **defer** используются для того, чтобы пока грузится внешний скрипт – браузер показал остальную (следующую за ним) часть страницы. Без них этого не происходит.
3. Разница между **async** и **defer**: атрибут **defer** сохраняет относительную последовательность скриптов, а **async** – нет. Кроме того, **defer** всегда ждёт, пока весь HTML-документ будет готов, а **async** – нет.

### Шесть типов данных, typeof

1. Есть 5 «примитивных» типов: **number**, **string**, **boolean**, **null**, **undefined** и 6-й тип – объекты **object**.
2. Оператор **typeof x** позволяет выяснить, какой тип находится в x, возвращая его в виде строки.

### Операторы сравнения и логические значения

1. В JavaScript есть логические значения **true** (истина) и **false** (ложь). Операторы сравнения возвращают их.
2. Строки сравниваются побуквенно.
3. Значения разных типов приводятся к числу при сравнении, за исключением строгого равенства === (!==).
4. Значения **null** и **undefined** равны == друг другу и не равны ничему другому. В других сравнениях (с участием >,<) их лучше не использовать, так как они ведут себя не как 0. **null** приводится к 0. **undefined** - к **NaN**, которое не равно ничему, даже самому себе.

### Побитовые операторы

1. Бинарные побитовые операторы: & | ^ << >> >>>.
2. Унарный побитовый оператор один: ~.
3. Как правило, битовое представление числа используется для:
  - Округления числа: (12.34^0) = 12, (\~~12.34) = 12.
  - Проверки на равенство -1: if (~n) { n не -1 }.
  - Упаковки нескольких битововых значений («флагов») в одно значение. Это экономит память и позволяет проверять наличие комбинации флагов одним оператором &.
  - Других ситуаций, когда нужны битовые маски.

### Взаимодействие с пользователем: alert, prompt, confirm

1. **alert** выводит сообщение. (alert(сообщение);)
2. **prompt** выводит сообщение и ждёт, пока пользователь введёт текст, а затем возвращает введённое значение или null, если ввод отменён (CANCEL/Esc). (result = prompt(title, default);)
3. **confirm** выводит сообщение и ждёт, пока пользователь нажмёт «OK» или «CANCEL» и возвращает true/false. (result = confirm(question);)


### Условные операторы: if, '?'

В логическом контексте:

- Число 0, пустая строка "", null и undefined, а также NaN являются false,
- Остальные значения – true.

### Условные операторы: if, '?'

В логическом контексте:
	
- Число 0, пустая строка "", null и undefined, а также NaN являются false,
- Остальные значения – true.

### Логические операторы

Логический оператор возвращает то значение, на котором остановились вычисления. Причём, не преобразованное к логическому типу.

### Преобразование типов для примитивов

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

### Функции

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
