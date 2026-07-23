# `v-object-typed`

## 📦 Функция

```lisp
(v-object-typed smdx_type property_1 property_2 ... property_N)
```

## 📄 Описание

Создание объекта заданного Smdx-типа.

## 📥 Аргументы

- `(string)` `smdx_type` - тип элемента информационной модели;
- `(property)` `property_#` - определяемое свойство.

## 📈 Возвращает

`(typed_object)` Объект заданного Smdx-типа с заданным набором свойств.

## 🧾 Пример использования

```lisp
; Создание элемента ИМ типа "SmdxPoint"
(v-object-typed "SmdxPoint"
  ; Инициализация значений свойств уже существующих в типе "SmdxPoint"
  (defproperty x 1.0 "X" (v-property-length-m))
  (defproperty y 0.0 "Y" (v-property-length-m))
  (defproperty z 0.0 "Z" (v-property-length-m))
  ; Добавление пользовательского свойства elevation
  (defproperty elevation 0.0 "Elevation" (v-property-length-m)))
```

