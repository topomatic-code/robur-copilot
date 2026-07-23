# `getproperty`

## 📦 Функция

```lisp
(getproperty variable)
(getproperty typed_object variable_name)
```

## 📄 Описание

Получение значения свойства конструкции или элемента информационной модели.

## 📥 Аргументы

- `(variable)` `variable` - переменная-идентификатор;
- `(typed_object)` `typed_object` - объект, содержащий свойство;
- `(string)` `variable_name` - строковый идентификатор переменной.

## 📈 Возвращает

`(dynamic)` Значение свойства.

## 🧾 Пример использования

Получение значения свойства конструкции:

```lisp
; Определяем свойство конструкции
(defproperty name_property "Имя" "Имя конструкции" (v-property-string))
; Выводим значение свойства в командную строку
(print (getproperty name_property))
; или
(print (getproperty 'name_property))
```

Получение значения свойства элемента информационной модели:

```lisp
(let
  ; Создаём элемент информационной модели типа "SmdxElement"
  ; и добавляем в него свойство
  ((im_element
    (v-object-typed "SmdxElement"
      (defproperty im_element_property 10.0 "Свойство элемента информационной модели" (v-property-length-m)))))
  ; Выводим значение свойства в командную строку
  (print (getproperty im_element "im_element_property"))
  ; или
  (print (getproperty im_element 'im_element_property)))
```
