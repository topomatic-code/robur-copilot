# `v-profile-rotate`

## 📦 Функция

```lisp
(v-profile-rotate profile start_angle)
(v-profile-rotate profile start_angle end_angle)
```

## 📄 Описание

Создание составного профиля.

## 📥 Аргументы

- `(profile)` `profile` - вращаемый профиль;
- `(double)` `start_angle` - начальный угол поворота;
- `(double)` `end_angle` - конечный угол поворота.

## 📈 Возвращает

`(profile)` Профиль.

## 🧾 Пример использования

```lisp
(let
  ; Определение профиля с переменным углом поворота
  ((profile (v-profile-rotate
              (v-profile-polygon 8 1.0)
              0 180)))
  ; Определение блока геометрии
  (defgeometry
    ; Создание 3D-тела
    (v-extrude profile (vec 0 0 1))))
```

