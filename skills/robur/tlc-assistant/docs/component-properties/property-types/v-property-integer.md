# `v-property-integer`

## 📦 Функция

```lisp
(v-property-integer units min_limit max_limit)
```

## 📄 Описание

Создание типа свойства: целое число.

## 📥 Аргументы

- `(string)` `units` - единицы измерения;
- `(integer)` `min_limit` - минимальное допустимое значение;
- `(integer)` `max_limit` - максимальное допустимое значение.

## 📈 Возвращает

`(property_type)` Тип свойства.

## 🧾 Пример использования

```lisp
(v-property-integer "n" 0 100)

```

