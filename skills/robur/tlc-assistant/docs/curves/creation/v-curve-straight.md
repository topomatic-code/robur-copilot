# `v-curve-straight`

## 📦 Функция

```lisp
(v-curve-straight start_vector end_vector)
```

## 📄 Описание

Создание кривой в форме отрезка.

## 📥 Аргументы

- `(vector3)` `start_vector` - начало отрезка;
- `(vector3)` `end_vector` - конец отрезка.

## 📈 Возвращает

`(curve)` Кривая.

## 🧾 Пример использования

```lisp
(v-curve-straight (vec) (vec 10.0 5.0))
```

