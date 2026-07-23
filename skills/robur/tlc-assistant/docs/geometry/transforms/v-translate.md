# `v-translate`

## 📦 Функция

```lisp
(v-translate offset bodies)
(v-translate offset body_1 body_2 ... body_N)
```

## 📄 Описание

Перемещение 3d-тел.

## 📥 Аргументы

- `(vector3)` `offset` - вектор смещения;
- `(list)` `bodies` - список изменяемых 3d-тел;
- `(geometry_object)` `body_#` - изменяемое 3d-тело.

## 📈 Возвращает

`(geometry_object)` 3d-тело.

## 🧾 Пример использования

Смещение двух тел на 10 м вдоль оси X; тела передаются в виде списка:

```lisp
(let
  (
    ; Список 3D-тел
    (bodies (list
              (v-extrude (v-profile-round 0.4) (vec 0 0 3))
              (v-extrude (v-profile-round 0.4) (vec 0 1 0)))))
  ; Перемещённое 3D-тело
  (v-translate (vec 10.0 0.0) bodies))
```

Смещение двух тел на 10 м вдоль оси X; тела передаются отдельными аргументами:

```lisp
(let
  (
    ; 3D-тело
    (body1 (v-extrude (v-profile-round 0.4) (vec 0 0 3)))
    ; 3D-тело
    (body2 (v-extrude (v-profile-round 0.4) (vec 0 1 0))))
  ; Перемещённое 3D-тело
  (v-translate (vec 10.0 0.0) body1 body2))
```

