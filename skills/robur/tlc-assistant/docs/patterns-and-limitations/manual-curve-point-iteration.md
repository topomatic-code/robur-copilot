# Перебор точек кривой, полученной от пользователя

## 🧷 Тема

Перебор точек кривой, полученной от пользователя.

## 📝 Описание

При решении некоторых задач возникает необходимость перебора точек кривой, запрошенной у пользователя.
Рассмотрим 3 основных способа:
- перебор сегментов кривой с малым шагом через v-curve-selection;
- запрос вершин (x, y, z) у объекта кривой;
- запрос точек плана (x, y, bugle) у объекта кривой.

## 🟢 GOOD (PATTERN)

Аппроксимация кривой точками с шагом 1 м с помощью `v-curve-selection`:

```lisp
; Перебор сегментов кривой с малым шагом через v-curve-selection.
; Минусы данного подхода:
; - точек будет очень много и скорость выполнения будет медленной;
; - точность и скорость аппроксимации кривой зависят от шага step;
; - создается много точек, для ряда задач это избыточно;
; - невозможно идеально описать кривую, т.к. она будет разбита на приближенные сегменты.
; Такой способ можно использовать тогда, когда не требуется высокая точность аппроксимации и длина кривой не будет слишком большой.
(defcomponent "TLC-Компонент" "SmdxElement"
  (defproperty axis nil "Ось" (v-property-typed "SmdxManualPolyline"))
  (defun has-axis (axis) (eql (eql axis nil) false))
  (if (has-axis axis)
    ; создаем точки вдоль кривой с шагом step
    (let (step selection points is_first_point)
      (setq step      1.0
            selection (v-curve-selection axis 0.001 (dict step nil) 0.0 0.0 1)
            points    (list))
      ; т.к. точки на стыках будут дублироваться - определяем флаг, является ли точка первой
      (setq is_first_point true)
      (v-for (sector selection)
        (let (u0 u1 p0 p1)
          (setq u0 (car sector)
                u1 (cadr sector)
                p0 (v-curve-d0 axis u0)
                p1 (v-curve-d0 axis u1))
          ; если первая точка была добавлена - отбрасываем дублирующиеся точки на стыках
          (when is_first_point
            (setq points (cons p0 points))
            (setq is_first_point false))
          (setq points (cons p1 points))))
      ; разворачиваем список, чтобы точки шли по порядку
      (setq points (reverse points))
      ; выводим полученные точки в консоль
      (v-for (p points)
        (print (format "x: {0}, y: {1}, z: {2}" (vec-x p) (vec-y p) (vec-z p))))
      ; рисуем полученные точки на виде сверху
      (defview
        (v-top)
        ; создаем 2d-точки, так как v-entity-polyline трактует z-компоненту как bugle
        (let (points_2d)
          (setq points_2d (list))
          (v-for (p (reverse points))
            (setq points_2d (cons (vec (vec-x p) (vec-y p)) points_2d)))
          (v-entity-polyline points_2d))))))
```

Получение трёхмерных вершин кривой через свойство `verteces`:

```lisp
; Запрос вершин (x, y, z) у объекта кривой.
; Позволяет получить z координату точки.
; Минусом данного подхода является то, что не получится получить величину закругления кривой в плане для круговых кривых.
; Если кривая определена над поверхностью, то в каждое пересечение кривой с гранями треугольников поверхности будет добавлена
; точка, что может значительно увеличить количество точек и скорость работы скрипта.
; Такой способ можно использовать в следующих случаях:
; - если кривая представляет собой ломаную линию в плане (в этом случае будет полное совпадение);
; - если необходимо учитывать z-компоненты точек;
; - если нужно учитывать переломы поверхности, над которой определена кривая.
(defcomponent "TLC-Компонент" "SmdxElement"
  (defproperty axis nil "Ось" (v-property-typed "SmdxManualPolyline"))
  (defun has-axis (axis) (eql (eql axis nil) false))
  (if (has-axis axis)
    ; запрашиваем значение свойства "verteces" у оси и получаем typed_object, представляющий набор точек
    (let (points_prop points)
      (setq points_prop (getproperty axis "verteces") ; typed_object, представляющий набор точек
            points      (list))
      ; перебираем объекты точек (каждая точка тоже typed_object)
      (v-for (point_obj points_prop)
        (let (x y z p)
          (setq x      (getproperty point_obj "x") ; у объекта точки запрашиваем значение свойства x
                y      (getproperty point_obj "y") ; у объекта точки запрашиваем значение свойства y
                z      (getproperty point_obj "z") ; у объекта точки запрашиваем значение свойства z
                p      (vec x y z) ; создаем 3d-точку в виде вектора
                points (cons p points)))) ; помещаем 3d-точку в список точек
      ; разворачиваем список, чтобы точки шли по порядку
      (setq points (reverse points))
      ; выводим полученные точки в консоль
      (v-for (p points)
        (print (format "x: {0}, y: {1}, z: {2}" (vec-x p) (vec-y p) (vec-z p))))
      ; рисуем полученные точки на виде сверху
      (defview
        (v-top)
        ; создаем 2d-точки, так как v-entity-polyline трактует z-компоненту как bugle
        (let (points_2d)
          (setq points_2d (list))
          (v-for (p (reverse points))
            (setq points_2d (cons (vec (vec-x p) (vec-y p)) points_2d)))
          (v-entity-polyline points_2d))))))
```

Получение плановых точек и значений bugle через свойство `mverteces`:

```lisp
; Запрос точек плана (x, y, bugle) у объекта кривой.
; Позволяет получить закругления (bugle) кривой.
; Такой способ можно использовать в следующих случаях:
; - если 2d-координат плана для решения поставленной задачи будет достаточно;
; - необходимо точное совпадение с круговыми кривыми в плане (и будет дальнейшая обработка значений bugle).
; Этот способ является наиболее быстрым, так как кривые часто задаются над поверхностью и точки "mverteces" не вписываются
; в каждое пересечение кривой с гранями треугольников поверхности, в отличие от вершин "verteces".
(defcomponent "TLC-Компонент" "SmdxElement"
  (defproperty axis nil "Ось" (v-property-typed "SmdxManualPolyline"))
  (defun has-axis (axis) (eql (eql axis nil) false))
  (if (has-axis axis)
    ; запрашиваем значение свойства "mverteces" у оси и получаем typed_object, представляющий набор 2d-точек плана
    (let (points_prop points)
      (setq points_prop (getproperty axis "mverteces") ; typed_object, представляющий набор точек
            points      (list))
      ; перебираем объекты точек (каждая точка тоже typed_object)
      (v-for (point_obj points_prop)
        (let (x y bugle p)
          (setq x      (getproperty point_obj "x") ; у объекта точки запрашиваем значение свойства x
                y      (getproperty point_obj "y") ; у объекта точки запрашиваем значение свойства y
                bugle  (getproperty point_obj "bugle") ; у объекта точки запрашиваем значение свойства bugle
                p      (vec x y bugle) ; создаем 2d-точку в виде вектора и помещаем значение bugle в z-компоненту
                points (cons p points)))) ; помещаем точку в список
      ; разворачиваем список, чтобы точки шли по порядку
      (setq points (reverse points))
      ; выводим полученные точки в консоль
      (v-for (p points)
        (print (format "x: {0}, y: {1}, bugle: {2}" (vec-x p) (vec-y p) (vec-z p))))
      ; рисуем полученные точки на виде сверху
      ; bugle представлен z-компонентой вектора точки, поэтому v-entity-polyline отработает корректно
      (defview
        (v-top)
        (v-entity-polyline points)))))
```

