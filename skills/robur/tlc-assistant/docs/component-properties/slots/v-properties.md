# `v-properties`

## 📦 Функция

```lisp
(v-properties property_1 ... property_N)
```

## 📄 Описание

Определение коллекции свойств.

## 📥 Аргументы

- `(property)` `property_#` - свойство.

## 📈 Возвращает

`(property)` Свойство.

## 🧾 Пример использования

```lisp
(v-properties
  (defproperty property_1 nil "Свойство_1" (v-property-string))
  (defproperty property_2 nil "Свойство_2" (v-property-length-m))
  (defproperty property_3 nil "Свойство_3" (v-property-logic)))

```

