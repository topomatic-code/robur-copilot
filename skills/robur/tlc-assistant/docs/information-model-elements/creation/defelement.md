# `defelement`

## 📦 Функция

```lisp
(defelement component property_1 property_2 ... property_N)
```

## 📄 Описание

Создание элемента информационной модели из компонента.

## 📥 Аргументы

- `(component)` `component` - компонент;
- `(property)` `property_#` - свойство компонента.

## 📈 Возвращает

`(im_element)` Элемент информационной модели.

## 🧾 Пример использования

```lisp
; Сохранение определения встраиваемого компонента
(setq my_component
  (defcomponent "Балка" "SmdxElement"
    (defproperty length_property 1.0 "Длина"
      (v-property-double "m" 0 100))
    (defgeometry
      (v-extrude
        (v-profile-p 0.01 0.2)
        (vec length_property 0)))))
; Создание элемента ИМ из компонента
(defelement my_component
  ; Изменение значения свойства компонента
  (defproperty length_property 2.0 "Длина" (v-property-double "m" 0 100))
  ; Добавление пользовательского свойства thickness_property
  (defproperty thickness_property 15 "Толщина" (v-property-double "mm" 0 100)))
```

