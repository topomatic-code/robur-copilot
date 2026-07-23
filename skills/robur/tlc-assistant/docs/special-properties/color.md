# Цвет

## 🏷️ Название

Цвет.

## 📖 Описание

Позволяет определить свойство, с возможностью выбора цвета из выпадающего списка или из палитры цветов.
Индексы цветов представляют собой индексы цветов Autocad.

## ⌨️ Синтаксис

```lisp
(defproperty color (v-object-typed "SmdxColor" (defproperty index 40 "Индекс")) "Цвет" (v-property-typed "SmdxColor"))
(defproperty color (v-object-typed "SmdxColor" (setproperty index 40 "Индекс")) "Цвет" (v-property-typed "SmdxColor"))
```

## 🛑 Правила

Начальное значение свойства должно быть задано строго в виде

```lisp
(v-object-typed "SmdxColor" ([prop] index [initial_index] "Индекс")),
```

где вместо "[prop]" следует задать тип свойства ("defproperty" или "setproperty"), а вместо "[initial_index]" - начальный индекс цвета Autocad.

Тип свойства должен быть (v-property-typed "SmdxColor").

Если необходимо определить несколько свойств с цветом, то следует использовать свойство для чтения "setproperty".
Так как "setproperty", в отличие от "defproperty", не вызывает конфликтов глобальных идентификаторов ("index").

## 📈 Возвращает

`(typed_object)` Объект, представляющий цвет.

## 🧾 Пример использования

Пример с запросом одного цвета:

```lisp
(defcomponent "Color example" "SmdxElement"
  ; запрашиваем у пользователя 1 цвет
  (defproperty cube_color (v-object-typed "SmdxColor" (defproperty index 40 "Индекс")) "Цвет кубика" (v-property-typed "SmdxColor"))
  (defgeometry
    (let (cube_color_index)
      (setq cube_color_index (getproperty cube_color "index"))
      (v-colored cube_color_index
        (v-extrude
          (v-profile-rect 0.5)
          (vec 0.5 0 0))))))
```

Пример с запросом нескольких цветов:

```lisp
(defcomponent "Color example" "SmdxElement"
  ; запрашиваем у пользователя несколько цветов
  (defproperty color_1 (v-object-typed "SmdxColor" (setproperty index 1 "Индекс")) "Цвет кубика" (v-property-typed "SmdxColor"))
  (defproperty color_2 (v-object-typed "SmdxColor" (setproperty index 3 "Индекс")) "Цвет кубика" (v-property-typed "SmdxColor"))
  (defgeometry
    (let (color_index_1 color_index_2)
      (setq color_index_1 (getproperty color_1 "index")
            color_index_2 (getproperty color_2 "index"))
      (v-compound
        (v-colored color_index_1
          (v-translate
            (vec -0.75 0.0 0.0)
            (v-extrude
              (v-profile-rect 0.5)
              (vec 0.5 0 0))))
        (v-colored color_index_2
          (v-translate
            (vec 0.25 0.0 0.0)
            (v-extrude
              (v-profile-rect 0.5)
              (vec 0.5 0 0))))))))
```

