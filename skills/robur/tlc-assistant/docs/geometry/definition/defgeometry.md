# `defgeometry`

## 📦 Функция

```lisp
(defgeometry body_1 body_2 body_3 ... body_N)
```

## 📄 Описание

Определение геометрии.

## 📥 Аргументы

- `(geometry_object)` `body_#` - 3d-тело.

## 📈 Возвращает

`(geometry)` Геометрия.

## 🧾 Пример использования

```lisp
; Объявление блока геометрии
(defgeometry
  ; Объединение 3D-тел в составное 3D-тело
  (v-compound
    ; Добавление фундамента
    (v-extrude (v-profile-rect 0.2) (vec 0 0 0.5))
    ; Добавление столба
    (v-translate (vec 0 0 0.5) (v-extrude (v-profile-round 0.1) (vec 0 0 2.0)))
    ; Добавление щита
    (v-translate
      (vec 0 0.05 2.5)
      (v-extrude (v-profile-round 0.7) (vec 0.0 0.01 0.0)))))
```

