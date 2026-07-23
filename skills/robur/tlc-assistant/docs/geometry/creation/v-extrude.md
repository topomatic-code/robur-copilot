# `v-extrude`

## 📦 Функция

```lisp
(v-extrude profile direction)
(v-extrude profile direction orientation)
```

## 📄 Описание

Создание 3d-тела путём выдавливания профиля вдоль вектора.

## 📥 Аргументы

- `(profile)` `profile` - выдавливаемый профиль;
- `(vector3)` `direction` - вектор выдавливания;
- `(vector3)` `orientation` - направление профиля.

## 📈 Возвращает

`(geometry_object)` 3d-тело.

## 💬 Примечания

Во внутренней реализации функция использует `v-sweep`:

- (`v-extrude` profile direction) → (`v-sweep` profile (v-curve-straight (vec) direction));
- (`v-extrude` profile direction orientation) → (`v-sweep` profile (v-curve-straight (vec) direction) orientation).

## 🧾 Пример использования

Выдавливание Т-образного профиля шириной и высотой 0,3 м вдоль оси Z на 1 м:

```lisp
(let
  ; Определение профиля
  ((profile (v-profile-t 0.01 0.3)))
  ; Определение блока геометрии
  (defgeometry
    ; Создание 3D-тела путём выдавливания профиля вдоль вектора
    (v-extrude profile (vec 0 0 1))))
```

Выдавливание того же Т-образного профиля вдоль оси Z на 1 м с ориентацией в направлении отрицательной оси Y:

```lisp
(let
  ; Определение профиля
  ((profile (v-profile-t 0.01 0.3)))
  ; Определение блока геометрии
  (defgeometry
    ; Создание 3D-тела путём выдавливания профиля вдоль вектора
    ; и назначением направления профиля
    (v-extrude profile (vec 0 0 1) (vec 0 -1))
  )
)
```

