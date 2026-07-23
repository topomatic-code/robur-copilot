# `v-quality`

## 📦 Функция

```lisp
(v-quality quality bodies)
(v-quality quality body_1 body_2 ... body_N)
```

## 📄 Описание

Изменение детализации 3d-тел.

## 📥 Аргументы

- `(double)` `quality` - степень детализации в диапазоне 0.01 - 1.00;
- `(list)` `bodies` - список изменяемых 3d-тел;
- `(geometry_object)` `body_#` - изменяемое 3d-тело.

## 📈 Возвращает

`(geometry_object)` 3d-тело.

## 🧾 Пример использования

Установка детализации 0,1 для двух тел, переданных в виде списка:

```lisp
(let
  (
    ; Список 3D-тел
    (bodies (list
              (v-extrude (v-profile-round 0.4) (vec 0 0 3))
              (v-extrude (v-profile-round 0.4) (vec 0 1 0)))))
  ; 3D-тело с изменённой детализацией
  (v-quality 0.1 bodies))
```

Установка детализации 0,1 для двух тел, переданных отдельными аргументами:

```lisp
(let
  (
    ; 3D-тело
    (body1 (v-extrude (v-profile-round 0.4) (vec 0 0 3)))
    ; 3D-тело
    (body2 (v-extrude (v-profile-round 0.4) (vec 0 1 0))))
  ; 3D-тело с изменённой детализацией
  (v-quality 0.1 body1 body2))
```

