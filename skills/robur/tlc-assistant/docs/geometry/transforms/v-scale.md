# `v-scale`

## 📦 Функция

```lisp
(v-scale scale bodies)
(v-scale scale body_1 body_2 ... body_N)
```

## 📄 Описание

Масштабирование 3d-тел.

## 📥 Аргументы

- `(vector3)` `scale` - вектор масштаба;
- `(list)` `bodies` - список изменяемых 3d-тел;
- `(geometry_object)` `body_#` - изменяемое 3d-тело.

## 📈 Возвращает

`(geometry_object)` 3d-тело.

## 🧾 Пример использования

Масштабирование двух тел в 2 раза вдоль оси X; тела передаются в виде списка:

```lisp
(let
  (
    ; Список 3D-тел
    (bodies (list
              (v-extrude (v-profile-round 0.4) (vec 0 0 3))
              (v-extrude (v-profile-round 0.4) (vec 0 1 0)))))
  ; Масштабированное 3D-тело
  (v-scale (vec 2.0 1.0 1.0) bodies))
```

Масштабирование двух тел в 2 раза вдоль оси X; тела передаются отдельными аргументами:

```lisp
(let
  (
    ; 3D-тело
    (body1 (v-extrude (v-profile-round 0.4) (vec 0 0 3)))
    ; 3D-тело
    (body2 (v-extrude (v-profile-round 0.4) (vec 0 1 0))))
  ; Масштабированное 3D-тело
  (v-scale (vec 2.0 1.0 1.0) body1 body2))
```

