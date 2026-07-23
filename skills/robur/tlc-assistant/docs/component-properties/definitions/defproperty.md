# `defproperty`

## 📦 Функция

```lisp
(defproperty variable default_value)
(defproperty variable default_value caption)
(defproperty variable default_value caption property_type)
```

## 📄 Описание

Определение изменяемого свойства конструкции.

## 📥 Аргументы

- `(variable)` `variable` - переменная-идентификатор;
- `(dynamic)` `default_value` - значение свойства по умолчанию;
- `(string)` `caption` - заголовок свойства;
- `(property_type)` `property_type` - тип свойства (по умолчанию свойство неопределённого типа).

## 📈 Возвращает

`(property)` Свойство.

## 🧾 Пример использования

```lisp
(defproperty
  efficiency_property              ; Имя переменной для обращения к этому свойству
  5                                ; Установка значения по умолчанию
  "Производительность"             ; Заголовок отображаемый в инспекторе свойств
  (v-property-double "m^3" 0 100)) ; Тип свойства: вещественное число

```

