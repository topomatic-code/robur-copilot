# `v-entity-hatch`

## 📦 Функция

```lisp
(v-entity-hatch profile)
(v-entity-hatch profile pattern)
(v-entity-hatch profile pattern scale)
(v-entity-hatch profile pattern scale angle)
(v-entity-hatch contour_1 contour_2 … contour_N)
(v-entity-hatch contour_1 contour_2 … contour_N pattern)
(v-entity-hatch contour_1 contour_2 … contour_N pattern scale)
(v-entity-hatch contour_1 contour_2 … contour_N pattern scale angle)
(v-entity-hatch contours)
(v-entity-hatch contours pattern)
(v-entity-hatch contours pattern scale)
(v-entity-hatch contours pattern scale angle)
```

## 📄 Описание

Создание примитива «штриховка».

## 📥 Аргументы

- `(profile)` `profile` - профиль, по которому будут определены границы штриховки;
- `(dynamic)` `contour_#` - контур, определяющий границы штриховки;
- `(dynamic)` `contours` - список или массив контуров, определяющих границы штриховки;
- `(string)` `pattern` - название паттерна штриховки;
- `(double)` `scale` - масштаб штриховки;
- `(double)` `angle` - угол поворота штриховки.

## 📈 Возвращает

`(entity)` Примитив.

## 💬 Примечания

В качестве набора точек используются векторы типа vector3.

Компоненты X,Y - задают положение вершины, а параметр Z - задает значение Bugle (скругление
сегмента между текущей вершиной и следующей).

Bugle - смещение наиболее удаленной точки дуги относительно сегмента,
образованного текущей и следующей вершиной. Отрицательное значение Bugle смещает дугу влево относительно сегмента, а
положительное - вправо.

При отрисовке штриховки учитывается вложенность контуров. Таким образом можно создавать островки и вложенные штриховки.

## 🧾 Пример использования

Создание штриховки по профилю дуги окружности:

```lisp
; Определение вида
(defview
  ; Вид сверху (план)
  (v-top)
  ; Штриховка на основании профиля
  (v-entity-hatch (v-profile-arc 1.0 0 120)))
```

Создание штриховки ANSI31 по контуру из векторов с дуговым сегментом:

```lisp
; Определение вида
(defview
  ; Вид сверху (план)
  (v-top)
  ; Штриховка на основании списка векторов
  (v-entity-hatch
    (list ; или array
      (vec -1.0  1.0 -0.2) ; значение -0.2 задает дугу между 0 и 1 вершинами, смещенную влево на 0.2 м
      (vec  1.0  1.0)
      (vec  1.0 -1.0)
      (vec -1.0 -1.0))
    "ANSI31"
    0.05
    0.0))
```

Создание штриховки GRAVEL по составному профилю с круглым островком:

```lisp
; Определение вида
(defview
  ; Вид сверху (план)
  (v-top)
  ; Штриховка на основании профиля с островком
  (v-entity-hatch
    (v-profile-compound
      (v-profile-round 1.5)
      (v-profile-round 0.5))
    "GRAVEL"
    0.015
    0.25))
```

Создание штриховки ANSI31 по прямоугольному контуру с двумя прямоугольными островками:

```lisp
; Определение вида
(defview
  ; Вид сверху (план)
  (v-top)
  ; штриховка с островками
  (v-entity-hatch
    (list
      (vec -1.0  1.0)
      (vec  1.0  1.0)
      (vec  1.0 -1.0)
      (vec -1.0 -1.0))
    (list
      (vec -0.5 0.75)
      (vec  0.5 0.75)
      (vec  0.5 0.0)
      (vec -0.5 0.0))
    (list
      (vec -0.5 -0.25)
      (vec  0.5 -0.25)
      (vec  0.5 -0.75)
      (vec -0.5 -0.75))
    "ANSI31"
    0.05
    0.0))
```

