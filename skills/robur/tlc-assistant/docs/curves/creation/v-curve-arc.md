# `v-curve-arc`

## 📦 Функция

```lisp
(v-curve-arc center normal major)
(v-curve-arc center normal major span)
```

## 📄 Описание

Создание кривой в форме дуги.

## 📥 Аргументы

- `(vector3)` `center` - центр дуги окружности;
- `(vector3)` `normal` - нормаль плоскости кривой;
- `(vector3)` `major` - начало кривой;
- `(double)` `span` - градусная мера дуги (по умолчанию равна 360 градусов).

## 📈 Возвращает

`(curve)` Кривая.

## 🧾 Пример использования

```lisp
(v-curve-arc (vec) (vec 0 0 1) (vec 10.0 5.0) 135)
```

