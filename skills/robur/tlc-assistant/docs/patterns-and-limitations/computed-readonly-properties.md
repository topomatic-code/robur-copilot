# Расчет и вывод значений в динамически вычисляемые свойства (объем, признак твердого тела и т.д.)

## 🧷 Тема

Расчет и вывод значений в динамически вычисляемые свойства (объем, признак твердого тела и т.д.).

## 📝 Описание

При динамическом расчете и выводе параметров тел объявления setproperty следует делать после определения defgeometry.
В противном случае свойства не попадут в результирующий элемент информационной модели и не выведутся в инспекторе свойств среды исполнения.

## 🚫 BAD (ANTIPATTERN, DO NOT COPY)

```lisp
(defcomponent "TLC-Компонент" "SmdxElement"
  (v-properties
    (defproperty width  1.0 "Ширина" (v-property-length-m))
    (defproperty height 1.0 "Высота" (v-property-length-m))
    (defproperty len    1.0 "Длина"  (v-property-length-m)))
  (let (cube)
    (setq cube
      (v-extrude
        (v-profile-rect width height)
        (vec len 0.0 0.0)))
    ; следующие свойства просто пропадут
    (setproperty volume (v-volume cube) "Объем")
    (setproperty is_solid (v-is-solid cube) "Тело")
    (defgeometry cube)))
```

## 🟢 GOOD (PATTERN)

```lisp
(defcomponent "TLC-Компонент" "SmdxElement"
  (v-properties
    (defproperty width  1.0 "Ширина" (v-property-length-m))
    (defproperty height 1.0 "Высота" (v-property-length-m))
    (defproperty len    1.0 "Длина"  (v-property-length-m)))
  (let (cube)
    (setq cube
      (v-extrude
        (v-profile-rect width height)
        (vec len 0.0 0.0)))
    ; используем глобальные переменные для хранения значений
    (setq *cube_volume* (v-volume cube))
    (setq *cube_is_solid* (v-is-solid cube))
    (defgeometry cube))
  ; определяем свойства и присваиваем им значения глобальных переменных
  (setproperty volume *cube_volume* "Объем")
  (setproperty is_solid *cube_is_solid* "Тело"))
```

