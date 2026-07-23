# `defcomponent`

## 📦 Функция

```lisp
(defcomponent component_name smdx_type block_1 block_2 ... block_N)
```

## 📄 Описание

Определение компонента.

## 📥 Аргументы

- `(string)` `component_name` - имя компонента;
- `(string)` `smdx_type` - тип элемента информационной модели;
- `(dynamic)` `block_#` - блоки компонента: геометрия, свойства, описания видов.

## 📈 Возвращает

`(component)` Компонент.

## 💬 Примечания

Основной компонент должен быть последней инструкцией скрипта.

## 🧾 Пример использования

```lisp
; Определение компонента
(defcomponent "My Custom Construction" "SmdxElement"
  ; Объявление свойства компонента
  (defproperty
    CustomIntProperty 5 "Cвойство с целым числом"
    (v-property-integer "n" 0 100))
  ; Объявление блока геометрии
  (defgeometry
    (v-extrude
      (v-profile-round 2)
      (vec 0 0 5))))
```
