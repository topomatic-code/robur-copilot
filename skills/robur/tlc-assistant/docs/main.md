# Tlc Reference

Справочник по синтаксису и функциям языка Topomatic Lisp Construction (Tlc).

## Разделы справочника

В справочнике изложена информация с разбивкой на разделы. Этот файл является точкой входа в документацию: здесь собрана общая информация о каждом разделе, а ссылки ведут на страницы конкретных функций, типов, специальных свойств и практических паттернов.

## 📘 Общие понятия

Tlc - это диалект языка программирования Lisp, разработанный компанией Topomatic.

Tlc реализует подмножество базового функционала CommonLisp и предоставляет библиотеку встроенных функций для создания элементов информационных моделей (BIM).

### Tlc-скрипт

Tlc-скрипт представляет собой файл с кодом на языке программирования Lisp, который реализует логику создания Tlc-компонента.

Файл Tlc-скрипта имеет расширение `.tlc`.

### Выполнение Tlc-скрипта

При вставке пользователем Tlc-модели в пространство проекта скрипт этой модели загружается и выполняется.

Результатом выполнения скрипта становится компонент, который содержит:

- 2D-представление;
- 3D-представление;
- набор свойств, отображаемых в инспекторе свойств.

### Повторное выполнение при изменении свойств

Когда пользователь изменяет свойства компонента, Tlc-скрипт выполняется повторно, но уже с новыми значениями свойств.

В результате повторного выполнения создаётся новый компонент с новыми значениями свойств.

## 🧠 Ядро Lisp: управляющие конструкции и определения

В этом разделе перечислены функции, макросы, константы и другие элементы, доступные в Tlc.

### Функционал из стандартного Common Lisp

#### Управляющие конструкции

- `dotimes`, `dolist`
- `when`, `if`
- `let`

#### Логика и сравнение

- `and`, `or`, `not`
- `=`, `/=`, `<`, `<=`, `>`, `>=`
- `eq`, `eql`, `equal`
- `null`, `identity`

#### Списки и пары (`cons`/`list`)

- `cons`, `car`, `cdr`, `list`, `atom`, `consp`, `listp`
- `append`, `nconc`, `reverse`, `nreverse`, `last`
- `assoc`, `member`
- `rplaca`, `rplacd`

#### Доступоры `c[a|d]+r`

- `caar`, `cadr`, `cdar`, `cddr`
- `caaar`, `caadr`, `cadar`, `caddr`
- `cdaar`, `cdadr`, `cddar`, `cdddr`
- `cadddr`, `caddddr`, `cadddddr`, `caddddddr`

#### Функции и макросы

- `defun`, `defmacro`
- `apply`

#### Символы

- `symbol-name`, `intern`, `make-symbol`, `gensym`, `*gensym-counter*`

#### Константы

- `t`
- `nil`

#### Числа и математика

- Арифметика: `+`, `-`, `*`, `/`, `mod`, `min`, `max`
- Округление и деление: `floor`, `ceiling`, `truncate`
- Абсолютное значение и знак: `abs`
- Тригонометрия: `sin`, `cos`, `asin`, `acos`, `atan`
- Гиперболические функции: `sinh`, `cosh`, `tanh`
- Логарифмы, степени и корни: `exp`, `log`, `log10`, `sqrt`

#### Предикаты типов

- `numberp`, `stringp`

#### Строки и вывод

- `format`
- `print`, `princ`, `prin1`, `terpri`

#### Прочее

- `length`

### Функционал из библиотеки Tlc

#### Управляющие конструкции и служебные функции

- `while`
- `letrec`

#### Scheme-подобные функции, совместимость и утилиты

- `assq`, `memq`
- `setcar`, `setcdr`

#### Константы и булевы значения

- `true`, `false`
- `PI`, `2PI`

#### Преобразования и строки

- `str`

#### Математика

- `pow` - аналог `expt` в Common Lisp
- `sqr`
- `%`
- `sign`

#### Массивы и словари

- `array`, `array-add`
- `dict`, `dict-get`, `dict-set`, `dict-keys`, `dict-values`, `dict-remove`

#### Итераторы и перечисления

- `enum-get`, `enum-next`, `enum-current`, `enum-reset`
- `range`
- `reverse` - в Tlc также применяется к коллекциям и итераторам

#### Модули и интроспекция

- `import`
- `dump`
- `*version*`

#### Компоненты, свойства и слоты

- `defcomponent`
- `defproperty`, `setproperty`
- `defslots`, `defslot`
- `getproperty`
- `v-property`, `v-properties`, `v-slot`

#### Типы свойств

- `v-property-double`, `v-property-integer`, `v-property-logic`, `v-property-enum`, `v-property-string`, `v-property-typed`
- `v-property-length-m`, `v-property-length-cm`, `v-property-length-mm`, `v-property-length-kg`

#### Утилиты

- `getbounds`
- `v-is-typed`, `v-object-typed`

#### Виды и представления

- `defview`, `defgeometry`
- `v-top`, `v-front`
- `v-element-view`, `v-element-viewbounds`
- `v-clip`

#### Элементы информационной модели

- `defelement`
- `setelement`

#### Геометрия 3D

- Булевы операции и анализ: `v-union`, `v-difference`, `v-intersection`, `v-volume`, `v-is-solid`, `v-simplify`
- Создание и операции тел: `v-sphere`, `v-extrude`, `v-revolve`, `v-sweep`, `v-sweep-miter`, `v-compound`
- Трансформации и качество: `v-translate`, `v-scale`, `v-align`, `v-quality`

#### Профили

- Примитивные профили: `v-profile-rect`, `v-profile-round`, `v-profile-arc`, `v-profile-polygon`, `v-profile-g`, `v-profile-p`, `v-profile-t`, `v-profile-shape`, `v-profile-compound`
- Лофт и модификаторы: `v-profile-loft`, `v-profile-loft-exact`, `v-profile-rotate`, `v-profile-scale`, `v-profile-translate`, `v-profile-mirror`

#### Кривые

- `v-curve-straight`, `v-curve-arc`, `v-curve-polyline`
- `v-curve-d0`, `v-curve-d1`, `v-curve-length`
- `v-curve-selection`

#### 2D-примитивы и оформление

- Примитивы: `v-entity-line`, `v-entity-circle`, `v-entity-arc`, `v-entity-polyline`, `v-entity-text`, `v-entity-text-styled`, `v-entity-hatch`, `v-entity-curve`
- Стили: `v-phong`, `v-colored`, `v-grayed`, `v-styled`

#### Векторы

- Создание и компоненты: `vec`, `vec-x`, `vec-y`, `vec-z`, `vec-len`, `mapscale`
- Алгебра: `vec-add`, `vec-sub`, `vec-mul`, `vec-dot`, `vec-cross`, `vec-normalize`, `vec-lerp`, `vec-clamp`, `vec-min`, `vec-max`, `vec-eq`, `vec-reflect`

#### Прочее

- `create-guid`
- `v-component`, `v-dynamic`
- `v-for`

## 🏛️ Система типов Tlc

Частично система типов Tlc базируется на формате Smdx.

Smdx (Summary MoDel eXtensible) - формат данных для обмена информационными моделями объектов капитального строительства, разработанный в компании Topomatic.

Формат Smdx поддерживается в экосистеме продуктов Topomatic, в частности в платформе проектирования Robur.

В "Топоматик Робур" Smdx - внутренний стандарт обмена данными проектов в информационном моделировании (BIM).

Smdx-типы - это типы элементов информационной модели (ИМ) в программном комплексе "Топоматик Робур". Они описываются в текстовых файлах с расширением `.smdx` с использованием разметки JSON.

Типы объектов определяют набор параметров и характеристик, присущих экземплярам данного типа.

Например, вымышленный тип `SmdxConcretePlate`, представляющий бетонные плиты, условно мог бы содержать такие параметры, как длина, ширина, высота, вес, марка бетона, объем бетона, тип арматуры.

### Типизированный объект

#### 🏷️ Название

`typed_object`

#### 📖 Описание

Типизированный объект.

Тип объекта задает набор свойств, имеющихся у объекта, а также семантику того, что этот объект представляет.

#### ⚙️ Поведение (не доступно из Tlc)

- `getObjectType() : string` - возвращает Smdx-тип объекта;
- `getProperties() : list<im_property>` - возвращает список свойств объекта.

#### ⚡ Функции, взаимодействующие с экземплярами типа (доступно в Tlc)

- Создание экземпляров: `v-object-typed`.
- Использование в качестве параметров: `v-is-typed`, `getproperty`.

### Элемент информационной модели

#### 🏷️ Название

`im_element`

#### 📖 Описание

Элемент информационной модели.

Является типизированным объектом с 2D-видами и 3D-моделью.

Если элемент является составным, то есть сборкой, он также содержит локальные вставки дочерних элементов, являющихся экземплярами `im_element`.

#### ♻️ Наследует тип

`typed_object`

Все Tlc-функции, применимые к экземплярам типа `typed_object`, также применимы и к экземплярам типа `im_element`.

#### ⚙️ Поведение (не доступно из Tlc)

- `getGeometryModel() : geometryModel` - возвращает 3D-геометрию (mesh) элемента информационной модели;
- `getReferences() : list<im_element_ref>` - возвращает список вставок дочерних элементов информационной модели;
- `getView(view:view) : dwg_block` - возвращает 2D-блок с чертежом запрашиваемого вида элемента информационной модели.

#### ⚡ Функции, взаимодействующие с экземплярами типа (доступно в Tlc)

- Все функции, взаимодействующие с типом `typed_object`.
- Создание экземпляров: `defelement`.
- Использование в качестве параметров: `setelement`, `getbounds`, `v-element-view`, `v-element-viewbounds`.

### Объект 3D-геометрии

#### 🏷️ Название

`geometry_object`

#### 📖 Описание

Объект 3D-геометрии в Tlc.

Является основной сущностью, используемой в 3D-моделировании.

#### ⚙️ Поведение (не доступно из Tlc)

- `getMesh(material:material, tolerance:double) : geometryModel` - возвращает 3D-геометрию (mesh) объекта геометрии, используется при отрисовке;
- `getSolid(material:material, tolerance:double) : solid` - возвращает твердое тело объекта геометрии, используется для твердотельных операций;
- `getComponents(material:material, tolerance:double) : list<im_element_ref>` - возвращает список вставок дочерних элементов информационной модели;
- `getView(view:view, matrix:matrix, mapscale:double) : dwg_block` - возвращает 2D-блок с чертежом запрашиваемого вида.

#### ⚡ Функции, взаимодействующие с экземплярами типа (доступно в Tlc)

- Создание экземпляров: `v-sweep`, `v-sweep-miter`, `v-revolve`, `v-extrude`, `v-sphere`, `v-union`, `v-difference`, `v-intersection`, `v-simplify`, `setelement`, `v-compound`, `v-quality`, `v-translate`, `v-scale`, `v-align`, `v-styled`, `v-clip`, `v-element-view`.
- Использование в качестве параметров: `defgeometry`, `v-volume`, `v-is-solid`.

### Профиль

#### 🏷️ Название

`profile`

#### 📖 Описание

Представляет собой 2D-профиль, используемый в операциях создания 3D-тел или 2D-отрисовке.

Профиль определяется в зависимости от параметра `u`, где `0.0 <= u <= 1.0`.

- `u == 0` соответствует началу траектории, то есть кривой выдавливания профиля;
- `u == 1` соответствует концу траектории, то есть кривой выдавливания профиля.

#### ⚙️ Поведение (не доступно из Tlc)

- `getProfile(u:double, tolerance:double) : list<list<vector2>>` - возвращает список с 2D-контурами профиля для заданного параметра `u`, где `0.0 <= u <= 1.0`;
- `isConstant() : bool` - возвращает, является ли профиль константным, то есть не зависящим от значения `u`. Это внутренний параметр, используемый для оптимизации.

#### ⚡ Функции, взаимодействующие с экземплярами типа (доступно в Tlc)

- Создание экземпляров: `v-profile-rect`, `v-profile-round`, `v-profile-arc`, `v-profile-polygon`, `v-profile-g`, `v-profile-p`, `v-profile-t`, `v-profile-shape`, `v-profile-compound`, `v-profile-loft-exact`, `v-profile-loft`, `v-profile-rotate`, `v-profile-scale`, `v-profile-translate`, `v-profile-mirror`.
- Использование в качестве параметров: `v-sweep`, `v-sweep-miter`, `v-revolve`, `v-extrude`, `v-entity-hatch`.

### Кривая

#### 🏷️ Название

`curve`

#### 📖 Описание

Представляет собой 3D-кривую.

#### ⚙️ Поведение (не доступно из Tlc)

- `getLength() : double` - возвращает длину кривой;
- `d0(u:double) : vector3` - возвращает точку на кривой для заданного `u`;
- `d1(u:double) : vector3` - возвращает касательную, то есть тангенс кривой, для заданного `u`.

#### ⚡ Функции, взаимодействующие с экземплярами типа (доступно в Tlc)

- Создание экземпляров: `v-curve-straight`, `v-curve-polyline`, `v-curve-arc`.
- Использование в качестве параметров: `v-sweep`, `v-sweep-miter`, `v-curve-d0`, `v-curve-d1`, `v-curve-length`, `v-curve-selection`, `v-entity-curve`.

## 🗃️ Базовые конструкции и структуры данных Tlc

Раздел описывает базовые функции вывода, массивы, словари, символы, итераторы, импорт внешних скриптов и вспомогательные функции.

### Вывод в командную строку

Функции вывода текста и перевода строки в окне командной строки.

- [`princ`](basic-constructs/output/princ.md)
- [`prin1`](basic-constructs/output/prin1.md)
- [`print`](basic-constructs/output/print.md)
- [`terpri`](basic-constructs/output/terpri.md)

### Массивы

Создание массивов и добавление элементов.

- [`array`](basic-constructs/arrays/array.md)
- [`array-add`](basic-constructs/arrays/array-add.md)

### Словари

Создание словарей, чтение, изменение и перечисление записей.

- [`dict`](basic-constructs/dictionaries/dict.md)
- [`dict-get`](basic-constructs/dictionaries/dict-get.md)
- [`dict-set`](basic-constructs/dictionaries/dict-set.md)
- [`dict-keys`](basic-constructs/dictionaries/dict-keys.md)
- [`dict-values`](basic-constructs/dictionaries/dict-values.md)
- [`dict-remove`](basic-constructs/dictionaries/dict-remove.md)

### Символы

Создание символов и получение имени символа.

- [`gensym`](basic-constructs/symbols/gensym.md)
- [`make-symbol`](basic-constructs/symbols/make-symbol.md)
- [`intern`](basic-constructs/symbols/intern.md)
- [`symbol-name`](basic-constructs/symbols/symbol-name.md)

### Итераторы и перечисления

Получение итераторов, обход коллекций, обратный порядок и диапазоны чисел.

- [`enum-get`](basic-constructs/iterators/enum-get.md)
- [`enum-next`](basic-constructs/iterators/enum-next.md)
- [`enum-current`](basic-constructs/iterators/enum-current.md)
- [`enum-reset`](basic-constructs/iterators/enum-reset.md)
- [`v-for`](basic-constructs/iterators/v-for.md)
- [`reverse`](basic-constructs/iterators/reverse.md)
- [`range`](basic-constructs/iterators/range.md)

### Импорт внешних скриптов

Импорт Lisp-скриптов из отдельных файлов.

- [`import`](basic-constructs/import/import.md)

### Прочее

Вспомогательные функции общего назначения.

- [`create-guid`](basic-constructs/misc/create-guid.md)

## 🔺 Векторы

Раздел описывает функционал для создания векторов и выполнения операций над 3D-векторами.

### Значения аргументов типа `vector3`

Если для аргумента указан тип `vector3`, значением этого аргумента могут быть:

- 3D-вектор;
- число;
- строка, конвертируемая в вещественное число;
- набор объектов, конвертируемых в вещественное число.

Например, функция `vec-len` рассчитывает длину 3D-вектора, принимаемого в качестве единственного аргумента:

```lisp
(vec-len vector)
```

Примеры допустимых значений аргумента:

```lisp
; 3D-вектор с координатами X=1.0, Y=5.0, Z=0.0
(vec-len (vec 1.0 5.0 0.0))

; Вещественное число, преобразуемое в 3D-вектор X=1.0, Y=1.0, Z=1.0
(vec-len 1.0)

; Строка, преобразуемая в вещественное число, затем в 3D-вектор X=1.0, Y=1.0, Z=1.0
(vec-len "1,0")

; Набор объектов, преобразуемых в 3D-вектор X=1.0, Y=5.0, Z=0.0
(vec-len (list 1.0 "5,0" 0.0))
(vec-len (array "1,0" 5.0 0.0))
```

### Создание векторов

Создание 3D-векторов.

- [`vec`](vectors/creation/vec.md)

### Координаты и длина

Получение координат и длины вектора.

- [`vec-x`](vectors/components/vec-x.md)
- [`vec-y`](vectors/components/vec-y.md)
- [`vec-z`](vectors/components/vec-z.md)
- [`vec-len`](vectors/components/vec-len.md)

### Векторная алгебра

Скалярное и векторное произведение, сложение, вычитание и умножение на скаляр.

- [`vec-dot`](vectors/algebra/vec-dot.md)
- [`vec-cross`](vectors/algebra/vec-cross.md)
- [`vec-add`](vectors/algebra/vec-add.md)
- [`vec-sub`](vectors/algebra/vec-sub.md)
- [`vec-mul`](vectors/algebra/vec-mul.md)

### Ограничения, интерполяция и нормализация

Отражение, выбор минимальных и максимальных координат, ограничение диапазоном, интерполяция, нормализация и сравнение.

- [`vec-reflect`](vectors/operations/vec-reflect.md)
- [`vec-min`](vectors/operations/vec-min.md)
- [`vec-max`](vectors/operations/vec-max.md)
- [`vec-clamp`](vectors/operations/vec-clamp.md)
- [`vec-lerp`](vectors/operations/vec-lerp.md)
- [`vec-normalize`](vectors/operations/vec-normalize.md)
- [`vec-eq`](vectors/operations/vec-eq.md)

## 🧩 Компонент

Компонент - это параметрический объект, обладающий набором свойств и способный менять своё геометрическое состояние и отображение на различных видах в соответствии с установленными значениями его свойств.

Один компонент может представлять собой целое семейство элементов информационной модели.

Компонент является основным объектом при работе со скриптами Tlc.

Создание компонента осуществляется функцией [`defcomponent`](component/defcomponent.md).

Результатом работы скрипта при вставке 3D-сборки должен быть компонент, поэтому функция `defcomponent` должна быть последней инструкцией в теле основного Tlc-скрипта разрабатываемой конструкции.

### Функции

- [`defcomponent`](component/defcomponent.md)

## 🔧 Свойства компонента

Раздел описывает создание свойств компонента, чтение значений свойств, типы свойств, слоты и группировку свойств в инспекторе.

### Практические темы

- [Применение `defproperty`, `setproperty` и `v-property`](component-properties/property-creation-patterns.md)
- [Единицы измерения свойств](component-properties/property-units.md)
- [Группировка свойств](component-properties/property-groups.md)

### Определение свойств

Создание изменяемых, неизменяемых и универсальных свойств компонента.

- [`defproperty`](component-properties/definitions/defproperty.md)
- [`setproperty`](component-properties/definitions/setproperty.md)
- [`v-property`](component-properties/definitions/v-property.md)

### Слоты и коллекции свойств

Создание слотов, коллекций свойств и получение значений свойств.

- [`defslot`](component-properties/slots/defslot.md)
- [`v-slot`](component-properties/slots/v-slot.md)
- [`v-properties`](component-properties/slots/v-properties.md)
- [`getproperty`](component-properties/slots/getproperty.md)

### Типы свойств

Создание объектов `property_type`, используемых при объявлении свойств.

- [`v-property-double`](component-properties/property-types/v-property-double.md)
- [`v-property-integer`](component-properties/property-types/v-property-integer.md)
- [`v-property-logic`](component-properties/property-types/v-property-logic.md)
- [`v-property-enum`](component-properties/property-types/v-property-enum.md)
- [`v-property-string`](component-properties/property-types/v-property-string.md)
- [`v-property-typed`](component-properties/property-types/v-property-typed.md)
- [`v-property-length-m`](component-properties/property-types/v-property-length-m.md)
- [`v-property-length-cm`](component-properties/property-types/v-property-length-cm.md)
- [`v-property-length-mm`](component-properties/property-types/v-property-length-mm.md)
- [`v-property-length-kg`](component-properties/property-types/v-property-length-kg.md)

## 🧬 Специальные свойства

Специальные свойства являются одним из основных способов взаимодействия с платформой Robur.
С помощью них можно сообщить платформе о необходимости применения особого поведения к Tlc-модели.
Платформа может использовать особые способы запроса значений у пользователя для этих свойств.
Например, специальные выпадающие списки, цветовые палитры, графический запрос набора точек, кривых, полилиний и т.д.
Для определения специальных свойств создаются обычные Tlc-свойства, реализующие определенные соглашения (определенные идентификаторы, типы и т.п.).

### Свойства

- [Обновлять отметку](special-properties/update-z.md)
- [Имя блока](special-properties/block-name.md)
- [Цвет](special-properties/color.md)
- [Полилиния по точкам](special-properties/manual-polyline.md)
- [Точка](special-properties/point.md)

## 🗺️ Виды компонента

Вид - это плоское отображение компонента с одной из его сторон.

В рабочих окнах программного комплекса Topomatic Robur компонент будет отображаться по-разному в зависимости от того, какой вид программа запрашивает у компонента для соответствующего рабочего окна.

Например, при отображении компонента на плане используется вид компонента сверху, а при построении сечений используется вид компонента спереди.

По умолчанию виды компонента генерируются автоматически на основе его геометрии.

Если у компонента переопределён какой-то вид, то на этом виде будут отображаться только описанные в нём примитивы.

### Функции

- [`defview`](component-views/defview.md)
- [`v-top`](component-views/v-top.md)
- [`v-front`](component-views/v-front.md)

## 📐 Профили

Объект Профиль (profile) не является отображаемым элементом. Профиль - это виртуальный эскиз, используемый при построении 3D-тел путём выдавливания или вращения.

### Примитивные профили

Создание прямоугольных, круглых, дуговых, многоугольных и стандартных профильных сечений.

- [`v-profile-rect`](profiles/primitive/v-profile-rect.md)
- [`v-profile-round`](profiles/primitive/v-profile-round.md)
- [`v-profile-arc`](profiles/primitive/v-profile-arc.md)
- [`v-profile-polygon`](profiles/primitive/v-profile-polygon.md)
- [`v-profile-g`](profiles/primitive/v-profile-g.md)
- [`v-profile-p`](profiles/primitive/v-profile-p.md)
- [`v-profile-t`](profiles/primitive/v-profile-t.md)

### Фигурные и составные профили

Создание произвольных и составных профилей.

- [`v-profile-shape`](profiles/compound/v-profile-shape.md)
- [`v-profile-compound`](profiles/compound/v-profile-compound.md)

### Изменяемые профили

Создание профилей, изменяющихся вдоль траектории выдавливания.

- [`v-profile-loft-exact`](profiles/loft/v-profile-loft-exact.md)
- [`v-profile-loft`](profiles/loft/v-profile-loft.md)

### Модификаторы профилей

Поворот, масштабирование, перемещение и отражение профилей.

- [`v-profile-rotate`](profiles/modifiers/v-profile-rotate.md)
- [`v-profile-scale`](profiles/modifiers/v-profile-scale.md)
- [`v-profile-translate`](profiles/modifiers/v-profile-translate.md)
- [`v-profile-mirror`](profiles/modifiers/v-profile-mirror.md)

## 🌀 Геометрия

Раздел описывает функции для создания 3D-тел, выполнения булевых операций, анализа, трансформаций, отсечения и визуального оформления геометрии.

### Определение геометрии

Определение блока геометрии компонента.

- [`defgeometry`](geometry/definition/defgeometry.md)

### Создание 3D-тел

Создание 3D-тел выдавливанием, вращением, протягиванием, сферой, составным телом или вставкой элемента ИМ.

- [`v-sweep`](geometry/creation/v-sweep.md)
- [`v-sweep-miter`](geometry/creation/v-sweep-miter.md)
- [`v-revolve`](geometry/creation/v-revolve.md)
- [`v-extrude`](geometry/creation/v-extrude.md)
- [`v-sphere`](geometry/creation/v-sphere.md)
- [`setelement`](geometry/creation/setelement.md)
- [`v-compound`](geometry/creation/v-compound.md)

### Булевы операции и упрощение

Объединение, разность, пересечение и упрощение 3D-тел.

- [`v-union`](geometry/boolean/v-union.md)
- [`v-difference`](geometry/boolean/v-difference.md)
- [`v-intersection`](geometry/boolean/v-intersection.md)
- [`v-simplify`](geometry/boolean/v-simplify.md)

### Анализ геометрии

Расчёт объёма и проверка корректности твёрдых тел.

- [`v-volume`](geometry/analysis/v-volume.md)
- [`v-is-solid`](geometry/analysis/v-is-solid.md)

### Трансформации и отсечение

Изменение детализации, перемещение, масштабирование, ориентация и отсечение 3D-тел.

- [`v-quality`](geometry/transforms/v-quality.md)
- [`v-translate`](geometry/transforms/v-translate.md)
- [`v-scale`](geometry/transforms/v-scale.md)
- [`v-align`](geometry/transforms/v-align.md)
- [`v-clip`](geometry/transforms/v-clip.md)

### Стили и окрашивание

Назначение стилей и цветов 3D-тел.

- [`v-styled`](geometry/styles/v-styled.md)
- [`v-colored`](geometry/styles/v-colored.md)
- [`v-grayed`](geometry/styles/v-grayed.md)
- [`v-phong`](geometry/styles/v-phong.md)

## 🏗️ Элементы информационной модели

Информационная модель - это трёхмерное графическое представление о взаимном расположении существующих и проектных объектов
в пространстве с заданной системой координат.
Элементы информационной модели - это объекты, которые могут обладать объёмными моделями, а так же семантическими свойствами.

### Создание объектов и элементов

Создание типизированных объектов и элементов информационной модели из компонентов.

- [`v-object-typed`](information-model-elements/creation/v-object-typed.md)
- [`defelement`](information-model-elements/creation/defelement.md)

### Проверка и размеры

Проверка Smdx-типа и получение габаритов элементов.

- [`v-is-typed`](information-model-elements/inspection/v-is-typed.md)
- [`getbounds`](information-model-elements/inspection/getbounds.md)

### Виды элементов

Получение 2D-вида элемента информационной модели и его размеров.

- [`v-element-view`](information-model-elements/views/v-element-view.md)
- [`v-element-viewbounds`](information-model-elements/views/v-element-viewbounds.md)

## 〰️ Кривые

Раздел описывает функции для создания кривых, вычисления точек и касательных, расчёта длины и разбивки кривой на участки.

### Создание кривых

Создание прямых, полилиний и дуг.

- [`v-curve-straight`](curves/creation/v-curve-straight.md)
- [`v-curve-polyline`](curves/creation/v-curve-polyline.md)
- [`v-curve-arc`](curves/creation/v-curve-arc.md)

### Вычисления на кривой

Получение точки, касательной и длины кривой.

- [`v-curve-d0`](curves/evaluation/v-curve-d0.md)
- [`v-curve-d1`](curves/evaluation/v-curve-d1.md)
- [`v-curve-length`](curves/evaluation/v-curve-length.md)

### Разбивка кривой

Разбивка кривой на участки по карте доступных длин.

- [`v-curve-selection`](curves/selection/v-curve-selection.md)

## 🔷 Примитивы

Раздел описывает 2D-примитивы, используемые при определении видов компонента: геометрические примитивы, текст и штриховку.

### Геометрические примитивы

Создание окружностей, дуг, отрезков, полилиний и примитивов на основе кривых.

- [`v-entity-circle`](entities/geometry/v-entity-circle.md)
- [`v-entity-arc`](entities/geometry/v-entity-arc.md)
- [`v-entity-line`](entities/geometry/v-entity-line.md)
- [`v-entity-polyline`](entities/geometry/v-entity-polyline.md)
- [`v-entity-curve`](entities/geometry/v-entity-curve.md)

### Текстовые примитивы

Создание обычного и стилизованного текста.

- [`v-entity-text`](entities/text/v-entity-text.md)
- [`v-entity-text-styled`](entities/text/v-entity-text-styled.md)

### Штриховка

Создание штриховки по профилям или контурам.

- [`v-entity-hatch`](entities/hatch/v-entity-hatch.md)

## 🧭 Практические паттерны и ограничения

Раздел содержит типовые паттерны использования языка Tlc, распространённые ошибки и рекомендуемые способы решения практических задач.

### Темы

- [Инициализация и вычисление значений переменных](patterns-and-limitations/variable-initialization.md)
- [Определение идентификатора длины - "length"](patterns-and-limitations/reserved-length-identifier.md)
- [Расчет и вывод значений в динамически вычисляемые свойства (объем, признак твердого тела и т.д.)](patterns-and-limitations/computed-readonly-properties.md)
- [Перебор точек кривой, полученной от пользователя](patterns-and-limitations/manual-curve-point-iteration.md)
- [Проверка доступности функционала (функций, макросов, констант, системных переменных и т.д.)](patterns-and-limitations/feature-availability-check.md)
- [Создание уникальных имен. Вывод блоков чертежа плана с уникальными именами](patterns-and-limitations/unique-plan-block-names.md)

## Шаблоны и правила документирования

- [Шаблон документирования специальных свойств](documentation-templates/special-properties.md)
- [Шаблон документирования типов Tlc](documentation-templates/types.md)
- [Шаблон документирования функций](documentation-templates/functions.md)
- [Шаблон документирования паттернов](documentation-templates/patterns.md)
- [Условные обозначения](documentation-templates/notation.md)
