# `setproperty`

## 📦 Функция

```lisp
(setproperty variable default_value)
(setproperty variable default_value caption)
(setproperty variable default_value caption property_type)
```

## 📄 Описание

Определение неизменяемого (readonly) свойства конструкции.

## 📥 Аргументы

- `(variable)` `variable` - переменная-идентификатор;
- `(dynamic)` `default_value` - значение свойства по умолчанию;
- `(string)` `caption` - заголовок свойства;
- `(property_type)` `property_type` - тип свойства (по умолчанию свойство неопределённого типа).

## 📈 Возвращает

`(property)` Свойство.

## 🧾 Пример использования

```lisp
(setproperty
  length_property                ; Имя переменной для обращения к этому свойству
  5                              ; Установка значения по умолчанию
  "Длина"                        ; Заголовок отображаемый в инспекторе свойств
  (v-property-double "m" 0 100)) ; Тип свойства: вещественное число

```

