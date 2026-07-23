# `v-property-length-mm`

## 📦 Функция

```lisp
(v-property-length-mm)
(v-property-length-mm min_limit)
(v-property-length-mm min_limit max_limit)
```

## 📄 Описание

Создание типа свойства: вещественное число с единицами измерения в миллиметрах.

## 📥 Аргументы

- `(double)` `min_limit` - минимальное допустимое значение;
- `(double)` `max_limit` - максимальное допустимое значение.

## 📈 Возвращает

`(property_type)` Тип свойства.

## 🧾 Пример использования

```lisp
(v-property-length-mm 0 100)

```

