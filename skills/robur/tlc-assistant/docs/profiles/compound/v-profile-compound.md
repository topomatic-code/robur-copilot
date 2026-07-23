# `v-profile-compound`

## 📦 Функция

```lisp
(v-profile-compound profile_1 profile_2 ... profile_N)
```

## 📄 Описание

Создание составного профиля.

## 📥 Аргументы

- `(profile)` `profile_#` - профиль.

## 📈 Возвращает

`(profile)` Профиль.

## 💬 Примечания

Функция принимает 2 и более профиля, иначе будет сгенерировано исключение.

## 🧾 Пример использования

```lisp
(let
  ; Объявление переменных
  (profile compound_profile)
  (setq
    ; Определение фигурного профиля
    profile (v-profile-shape
              (vec) (vec -0.5 0.5)
              (vec -0.5 0.5) (vec 0.0 2.0)
              (vec 0.0 2.0) (vec 0.5 0.5)
              (vec 0.5 0.5) (vec))
    ; Определение составного профиля
    compound_profile (v-profile-compound
                       ; Профиль
                       profile
                       ; Профиль повернутый на 90 градусов
                       (v-profile-rotate profile 90)
                       ; Профиль повернутый на 180 градусов
                       (v-profile-rotate profile 180)
                       ; Профиль повернутый на 270 градусов
                       (v-profile-rotate profile 270)))
  ; Объявление блока геометрии
  (defgeometry
    ; Создание 3D-тела путём выдавливания профиля
    (v-extrude compound_profile (vec 0.0 0.0 0.1))))
```
