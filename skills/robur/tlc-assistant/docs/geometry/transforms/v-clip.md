# `v-clip`

## 📦 Функция

```lisp
(v-clip normal pivot body_1 body_2 ... body_N)
(v-clip normal pivot bodies)
```

## 📄 Описание

Отсечение части 3d-тела плоскостью.

## 📥 Аргументы

- `(vector3)` `normal` - нормаль плоскости;
- `(vector3)` `pivot` - опорная точка плоскости;
- `(list)` `bodies` - список изменяемых 3d-тел;
- `(geometry_object)` `body_#` - изменяемое 3d-тело.

## 📈 Возвращает

`(geometry_object)` 3d-тело.

## 🧾 Пример использования

Отсечение двух тел плоскостью с нормалью `(-1, -1, -1)`, проходящей через точку `(1, 0, 0)`; тела передаются в виде списка:

```lisp
(let
  (
    ; Список 3D-тел
    (bodies
      (list
        (v-styled
          (v-phong "Синий" (vec 0 0 1))
          (v-extrude
            (v-profile-rect 1.0)
            (vec 2.0 0.0)))
        (v-styled
          (v-phong "Красный" (vec 1 0 0))
          (v-extrude
            (v-profile-rect 2.0)
            (vec 2.0 0.0))))))
  ; Усечённое 3D-тело
  (v-clip
    (vec -1.0 -1.0 -1.0)
    (vec 1.0 0.0 0.0)
    bodies))
```

Отсечение двух тел той же плоскостью; тела передаются отдельными аргументами:

```lisp
(let
  (
    ; 3D-тело
    (body1
      (v-styled
        (v-phong "Синий" (vec 0 0 1))
        (v-extrude
          (v-profile-rect 1.0)
          (vec 2.0 0.0))))
    ; 3D-тело
    (body2
      (v-styled
        (v-phong "Красный" (vec 1 0 0))
        (v-extrude
          (v-profile-rect 2.0)
          (vec 2.0 0.0)))))
  ; Усечённое 3D-тело
  (v-clip
    (vec -1.0 -1.0 -1.0)
    (vec 1.0 0.0 0.0)
    body1
    body2))
```

