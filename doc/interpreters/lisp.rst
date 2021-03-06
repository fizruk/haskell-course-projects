====
Лисп
====

Описание
--------

В данном задании предлагается реализовать интерпретатор диалекта языка программирования Лисп.

Базовым объектом Лисп является S-выражение и в предлагаемом диалекте оно может быть представлено

- атомом (``IAMATOM``, ``numberp``, ``setf``),
- числовым литералом (``10``, ``34.2``),
- строковым литералом (``"hello, world!"``),
- пустым списком (``nil``, ``()``),
- точечной парой (``(1 . 2)``).

Как обычно, непустой список представляется точечной парой, вторым элементом которой является другой список:
``(1 "asd" atom)`` эквивалентно ``(1 . ("asd" . (atom . nil)))``.

Каждое S-выражение может быть вычислено по следующим правилам:

- числовые, строковые литералы, пустой список и атом вычисляются в себя;
- список ``(f ...)`` вычисляется применением функции (или раскрытием макроса) ``f`` к остальным элементам списка;
- функция перед применением вычисляет все свои аргументы;
- макросы и специальные формы не вычисляют аргументы перед применением.

Программа на этом диалекте состоит из последовательности S-выражений.

Диалект языка выражений может быть расширен:

- встроенными специальными формами:

  - ``quote`` (``'``);
  - ``if``;
  - ``let``;
  - ``macro``;
  - ``setf``;

- пользовательскими функциями: ``lambda``, ``defun``;
- лексическим/динамическим связыванием;
- операциями ввода-вывода;
- функциями с переменным числом аргументов;
- и т.д.

Минимальные требования (базовая часть)
--------------------------------------

Базовая реализация проекта, в которой должны разбираться все участники, должна:

- определять структуру данных для синтаксического дерева;
- содержать раздельно парсер и интерпретатор;
- предоставлять простую интерактивную среду программирования (REPL);
- предоставлять встроенные предикаты и функции:

  - ``atomp``, ``numberp``, ``listp``, ``=``;
  - ``car``, ``cdr``, ``cons``.

Расширенный парсер (дополнительная часть)
-----------------------------------------

Расширенный парсер должен добавлять хотя бы 2 различные возможности к базовому варианту.
Ниже перечислены возможные варианты расширения парсера, однако этим списком они не ограничены:

- разбор расширенного диалекта;
- восстановление после ошибок (например, если пользователь написал лишнюю закрывающую скобку,
  парсер может запомнить эту ошибку и продолжить разбор программы);
- и т.д.

Расширенная интерактивная среда (дополнительная часть)
------------------------------------------------------

Расширенная интерактивная среда должна добавлять хотя бы 2 различные возможности к базовому интерфейсу.
Ниже перечислены возможные варианты расширения интерактивной среды, однако этим списком они не ограничены:

- команды интерпретатора:

  - загрузить программу из файла;
  - провести один шаг вычисления;
  - раскрыть вызовы макросов;

- интерпретация расширенного диалекта;
- дружелюбные сообщения об ошибках (например, при опечатке в имени переменной можно предложить
  имена переменных, отличающихся одной буквой, которые находятся в области видимости);
- и т.д.

Генерация кода (дополнительная часть)
-------------------------------------

Модуль генерации кода — предпоследний этап компиляции.
Генерация кода может быть реализована многими способами, но чтобы простым
образом получить портируемый компилятор, можно генерировать промежуточный код
на низкоуровневом языке программирования, таком как C или еще ниже, например, LLVM.

Генерация кода должна переводить пользовательские функции в соответствующие функции
целевого языка (для этого диалект должен быть расширен возможностью определения пользовательских функций).

Демонстрация генерации кода должна включать в себя программу на любом языке,
использующую сгенерированный объектный код при сборке.

