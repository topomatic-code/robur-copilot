# `setelement`

## 📦 Функция

```lisp
(setelement name element)
```

## 📄 Описание

Создание 3d-тела из элемента ИМ.

## 📥 Аргументы

- `(string)` `name` - имя вставки;
- `(im_element)` `element` - элемент информационной модели.

## 📈 Возвращает

`(geometry_object)` 3d-тело.

## 🧾 Пример использования

Создание элемента информационной модели из компонента «Балка» и его вставка в геометрию:

```lisp
; Сохранение определения встраиваемого компонента
(setq my_component (defcomponent "Балка" "SmdxElement"
                     (defgeometry
                       (v-extrude
                         (v-profile-p 0.01 0.2)
                         (vec length_property 0)))))
; Определение геометрии
(defgeometry
  (let
    ; Создание элемента ИМ из компонента
    ((im_element (defelement my_component)))
    ; Создание 3D-тела из элемента ИМ
    (setelement "Вставка" im_element)))
```

Вставка элемента информационной модели, выбранного пользователем в свойстве компонента:

```lisp
; Cвойство компонента
; с выбором объекта из библиотеки 3D-моделей
(defproperty
  slot_element nil "Элемент"
  (v-property-typed "SmdxElement"))
; Определение геометрии
(defgeometry
  ; Создание 3D-тела из элемента ИМ
  (setelement "Вставка" slot_element))
```

