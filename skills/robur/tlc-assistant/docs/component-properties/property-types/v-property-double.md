# `v-property-double`

## 📦 Функция

```lisp
(v-property-double units min_limit max_limit)
```

## 📄 Описание

Создание типа свойства: вещественное число.

## 📥 Аргументы

- `(string)` `units` - единицы измерения;
- `(double)` `min_limit` - минимальное допустимое значение;
- `(double)` `max_limit` - максимальное допустимое значение.

## 📈 Возвращает

`(property_type)` Тип свойства.

## 🧾 Пример использования

```lisp
(v-property-double "m^3/c" 0 100)

```

