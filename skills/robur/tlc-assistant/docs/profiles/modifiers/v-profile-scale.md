# `v-profile-scale`

## 📦 Функция

```lisp
(v-profile-scale profile start_scale)
(v-profile-scale profile start_scale end_scale)
```

## 📄 Описание

Создание профиля с переменным масштабом.

## 📥 Аргументы

- `(profile)` `profile` - масштабируемый профиль;
- `(vector3)` `start_scale` - начальный масштаб;
- `(vector3)` `end_scale` - конечный масштаб.

## 📈 Возвращает

`(profile)` Профиль.

## 🧾 Пример использования

```lisp
(let
  ; Определение профиля с переменным масштабом
  ((profile (v-profile-scale
              (v-profile-polygon 8 1.0)
              (vec 2.0) (vec 1.0))))
  ; Определение блока геометрии
  (defgeometry
    ; Создание 3D-тела
    (v-extrude profile (vec 0 0 1))))
```

