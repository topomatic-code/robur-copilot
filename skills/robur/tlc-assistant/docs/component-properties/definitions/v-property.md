# `v-property`

## 📦 Функция

```lisp
(v-property changable id default_value)
(v-property changable id default_value caption)
(v-property changable id default_value caption property_type)
```

## 📄 Описание

Определение свойства конструкции.

## 📥 Аргументы

- `(bool)` `changable` - признак изменяемости значения свойства (t - изменяемое, nil - неизменяемое (readonly));
- `(string)` `id` - идентификатор свойства;
- `(dynamic)` `default_value` - значение свойства по умолчанию;
- `(string)` `caption` - заголовок свойства;
- `(property_type)` `property_type` - тип свойства (по умолчанию свойство неопределённого типа).

## 📈 Возвращает

`(property)` Свойство.

## 🧾 Пример использования

```lisp
(v-property
  t                    ; Признак изменяемости значения свойства
  "name_property"      ; Идентификатор свойства
  "Балка"              ; Значение по умолчанию
  "Имя конструкции"    ; Заголовок в инспекторе свойств
  (v-property-string)) ; Тип свойства

```

