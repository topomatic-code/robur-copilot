# `v-grayed`

## 📦 Функция

```lisp
(v-grayed color_index body_1 body_2 ... body_N)
(v-grayed color_index bodies)
```

## 📄 Описание

Окрашивает 3d-тело серым цветом (фактически убирает всю окраску).

## 📥 Аргументы

- `(list)` `bodies` - список окрашиваемых 3d-тел;
- `(geometry_object)` `body_#` - окрашиваемое 3d-тело.

## 📈 Возвращает

`(geometry_object)` Окрашенное 3d-тело.

## 🧾 Пример использования

```lisp
(defcomponent "Серое 3d-тело" "SmdxElement"
  (defgeometry
    (v-grayed
      (v-extrude
        (v-profile-rect 0.5)
        (vec 0.5 0.0 0.0)))))
```

