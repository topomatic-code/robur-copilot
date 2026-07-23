# `v-property-length-cm`

## 📦 Функция

```lisp
(v-property-length-cm)
(v-property-length-cm min_limit)
(v-property-length-cm min_limit max_limit)
```

## 📄 Описание

Создание типа свойства: вещественное число с единицами измерения в сантиметрах.

## 📥 Аргументы

- `(double)` `min_limit` - минимальное допустимое значение;
- `(double)` `max_limit` - максимальное допустимое значение.

## 📈 Возвращает

`(property_type)` Тип свойства.

## 🧾 Пример использования

```lisp
(v-property-length-cm 0 100)

```

