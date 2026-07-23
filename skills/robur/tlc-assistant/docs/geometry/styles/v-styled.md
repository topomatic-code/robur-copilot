# `v-styled`

## 📦 Функция

```lisp
(v-styled style body_1 body_2 ... body_N)
(v-styled style bodies)
```

## 📄 Описание

Изменение цвета 3d-тела.

## 📥 Аргументы

- `(style)` `style` - стиль окрашивания;
- `(list)` `bodies` - список изменяемых 3d-тел;
- `(geometry_object)` `body_#` - изменяемое 3d-тело.

## 📈 Возвращает

`(geometry_object)` 3d-тело.

## 🧾 Пример использования

Назначение синего Phong-стиля двум телам, переданным в виде списка:

```lisp
(let
  (
    ; Список 3D-тел
    (bodies (list
              (v-extrude (v-profile-round 0.4) (vec 0 0 3))
              (v-extrude (v-profile-round 0.4) (vec 0 1 0)))))
  ; 3D-тело с изменённым цветом
  (v-styled (v-phong "Цвет" (vec 0 0 1)) bodies))
```

Назначение синего Phong-стиля двум телам, переданным отдельными аргументами:

```lisp
(let
  (
    ; 3D-тело
    (body1 (v-extrude (v-profile-round 0.4) (vec 0 0 3)))
    ; 3D-тело
    (body2 (v-extrude (v-profile-round 0.4) (vec 0 1 0))))
  ; 3D-тело с изменённым цветом
  (v-styled (v-phong "Цвет" (vec 0 0 1)) body1 body2))
```

