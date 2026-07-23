# `v-profile-translate`

## 📦 Функция

```lisp
(v-profile-translate profile start_position)
(v-profile-translate profile start_position end_position)
```

## 📄 Описание

Создание профиля с переменным положением.

## 📥 Аргументы

- `(profile)` `profile` - перемещаемый профиль;
- `(vector3)` `start_position` - начальное положение;
- `(vector3)` `end_position` - конечное положение.

## 📈 Возвращает

`(profile)` Профиль.

## 🧾 Пример использования

```lisp
(let
  ; Определение профиля с переменным положением
  ((profile (v-profile-translate
              (v-profile-polygon 8 1.0)
              (vec) (vec 1.0 1.0))))
  ; Определение блока геометрии
  (defgeometry
    ; Создание 3D-тела
    (v-extrude profile (vec 0 0 1))))
```

