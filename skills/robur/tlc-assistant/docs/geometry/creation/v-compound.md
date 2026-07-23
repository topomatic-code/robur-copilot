# `v-compound`

## 📦 Функция

```lisp
(v-compound object_1 object_2 ... object_N)
```

## 📄 Описание

Создание составного 3d-тела.

## 📥 Аргументы

- `(geometry_object)` `object_#` - объединяемые 3d-тела.

## 📈 Возвращает

`(geometry_object)` 3d-тело.

## 🧾 Пример использования

```lisp
(v-compound
  ; Определение 3D-тела
  (v-extrude
    (v-profile-round 0.4)
    (vec 0 0 0.5))
  ; Определение 3D-тела
  (v-translate
    (vec 0.0 0.0 0.5)
    (v-extrude
      (v-profile-rect 0.1)
      (vec 0 0 2))))
```

