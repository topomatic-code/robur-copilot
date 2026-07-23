# `v-property-length-m`

## 📦 Функция

```lisp
(v-property-length-m)
(v-property-length-m min_limit)
(v-property-length-m min_limit max_limit)
```

## 📄 Описание

Создание типа свойства: вещественное число с единицами измерения в метрах.

## 📥 Аргументы

- `(double)` `min_limit` - минимальное допустимое значение;
- `(double)` `max_limit` - максимальное допустимое значение.

## 📈 Возвращает

`(property_type)` Тип свойства.

## 🧾 Пример использования

```lisp
(v-property-length-m 0 100)

```

