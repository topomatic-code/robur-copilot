# Точка

## 🏷️ Название

Точка.

## 📖 Описание

Определяет редактируемую пользователем 3d-точку.
На плане проекта появляется 2d-грип, позволяющий пользователю изменять ее положение.
При изменении положения точки, скрипт выполняется заново с обновленным значением точки.

Точку представляет объект typed_object с Smdx-типом "SmdxPoint".
Объект содержит свойства с идентификаторами: "x", "y", "z".

Допускается задавать nil в качестве начального значения.
В этом случае происходит следующее:
1. Происходит первое выполнение всего скрипта. Платформа Robur "видит", какие свойства создал пользователь. Специальное свойство имеет значение nil.
2. Обнаруживается специальное свойство запроса точки на плане.
3. Платформа предлагает пользователю ввести точку на плане (вид сверху).
4. После ввода точки платформа присваивает специальному свойству в качестве значения объект (типа typed_object), представляющий введенную точку.
5. Скрипт выполняется второй раз. Специальное свойство имеет значение, отличное от nil.

Если определить несколько специальных свойств с точками, то платформа запросит у пользователя последовательный ввод нескольких точек.

Если точка расположена над поверхностью, то значение z (отметка) будет браться с поверхности.

Тем не менее в инспекторе свойств, при выборе модели Tlc в проекте, пользователь сможет вручную указать любые значения координатам точки.

Несмотря на то, что точка вводится пользователем в мировой системе координат проекта, в свойство она попадает уже с пересчетом в локальную систему координат Tlc-модели. Таким образом в Tlc-скриптах можно использовать точки "как есть", без каких-либо дополнительных преобразований.

## ⌨️ Синтаксис

```lisp
(defproperty point
  (v-object-typed "SmdxPoint"
    (defproperty x 0.0 "X" (v-property-length-m))
    (defproperty y 0.0 "Y" (v-property-length-m))
    (defproperty z 0.0 "Z" (v-property-length-m)))
  "Точка"
  (v-property-typed "SmdxPoint"))
(defproperty point
  (v-object-typed "SmdxPoint"
    (setproperty x 0.0 "X" (v-property-length-m))
    (setproperty y 0.0 "Y" (v-property-length-m))
    (setproperty z 0.0 "Z" (v-property-length-m)))
  "Точка"
  (v-property-typed "SmdxPoint"))
(defproperty point nil "Точка" (v-property-typed "SmdxPoint"))
```

## 🛑 Правила

Начальное значение свойства должно быть nil, либо задано строго в виде:

```lisp
(v-object-typed "SmdxPoint"
  ([prop] x [initial_x] "X" (v-property-length-m))
  ([prop] y [initial_y] "Y" (v-property-length-m))
  ([prop] z [initial_z] "Z" (v-property-length-m)))
```

где вместо "[prop]" следует задать тип свойства ("defproperty" или "setproperty"),
а вместо "[initial_x]", "[initial_y]", "[initial_z]" следует подставить начальные значения
x, y и z координат соответственно.

Тип свойства должен быть (v-property-typed "SmdxPoint").

ВАЖНО: если нужно определить несколько специальных свойств с точками, то в качестве начального значения нужно задавать либо nil, либо использовать свойство для чтения "setproperty". Так как "setproperty", в отличие от "defproperty", не вызывает конфликтов глобальных идентификаторов ("x", "y", "z").

## 📈 Возвращает

`(typed_object)` Объект, представляющий точку (Smdx-тип "SmdxPoint").

## 🧾 Пример использования

Пример с двумя точками:

```lisp
(defcomponent "Points" "SmdxElement"
  ; определяем две точки с возможностью перемещать их на плане с помощью грипов
  (defproperty
    point_A
    (v-object-typed "SmdxPoint"
      (setproperty x 1.0 "X" (v-property-length-m))
      (setproperty y 2.0 "Y" (v-property-length-m))
      (setproperty z 0.0 "Z" (v-property-length-m)))
    "Точка A"
    (v-property-typed "SmdxPoint"))
  (defproperty
    point_B
    (v-object-typed "SmdxPoint"
      (setproperty x 5.0 "X" (v-property-length-m))
      (setproperty y 3.0 "Y" (v-property-length-m))
      (setproperty z 0.0 "Z" (v-property-length-m)))
    "Точка B"
    (v-property-typed "SmdxPoint"))
  ; соединяем точки полилинией и рисуем ее на плане (вид сверху)
  (defview
    (v-top)
    (let (p1 p2)
      (setq p1 (vec (getproperty point_A "x") (getproperty point_A "y") (getproperty point_A "z"))
            p2 (vec (getproperty point_B "x") (getproperty point_B "y") (getproperty point_B "z")))
      (v-entity-polyline (list p1 p2)))))
```

Пример с последовательным запросом трёх точек:

```lisp
(defcomponent "Points" "SmdxElement"
  ; запрашиваем последовательно у пользователя ввод сразу трех точек с возможностью перемещать их на плане с помощью грипов
  (defproperty point_A nil "Точка A" (v-property-typed "SmdxPoint"))
  (defproperty point_B nil "Точка B" (v-property-typed "SmdxPoint"))
  (defproperty point_C nil "Точка C" (v-property-typed "SmdxPoint"))
  (defun has-point (point)
    (when (eql (eql point nil) false)))
  ; если все точки введены - соединяем их полилинией и рисуем ее на плане (вид сверху)
  (when (and (has-point point_A) (has-point point_B) (has-point point_C))
    (defview
      (v-top)
      (let (p1 p2 p3)
        (setq p1 (vec (getproperty point_A "x") (getproperty point_A "y") (getproperty point_A "z"))
              p2 (vec (getproperty point_B "x") (getproperty point_B "y") (getproperty point_B "z"))
              p3 (vec (getproperty point_C "x") (getproperty point_C "y") (getproperty point_C "z")))
        (v-entity-polyline (list p1 p2 p3))))))
```

