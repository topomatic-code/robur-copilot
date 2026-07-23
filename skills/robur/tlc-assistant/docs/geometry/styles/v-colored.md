# `v-colored`

## 📦 Функция

```lisp
(v-colored color_index body_1 body_2 ... body_N)
(v-colored color_index bodies)
```

## 📄 Описание

Изменение цвета 3d-тела.

## 📥 Аргументы

- `(integer)` `color_index` - индекс цвета (из системы индексов цветов Autocad);
- `(list)` `bodies` - список окрашиваемых 3d-тел;
- `(geometry_object)` `body_#` - окрашиваемое 3d-тело.

## 📈 Возвращает

`(geometry_object)` Окрашенное 3d-тело.

## 🧾 Пример использования

```lisp
(defcomponent "Раскраска 3d-моделей" "SmdxElement"
  (defproperty color_index 1 "Индекс цвета Autocad" (v-property-integer "n" 0 255))
  (defgeometry
    (v-colored
      color_index
      (v-extrude
        (v-profile-rect 0.5)
        (vec 0.5 0.0 0.0)))))
```

