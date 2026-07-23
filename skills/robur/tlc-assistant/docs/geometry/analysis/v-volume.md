# `v-volume`

## 📦 Функция

```lisp
(v-volume body_1 body_2 … body_N)
(v-volume bodies)
```

## 📄 Описание

Вычисляет объем твердого тела.

## 📥 Аргументы

- `(geometry_object)` `body_#` - 3d-тело;
- `(list)` `bodies` - список 3d-тел.

## 📈 Возвращает

`(double)` Вычисленный объем.

## 💬 Примечания

Если тела являются составными (подсборками, состоящими из отдельных деталей) – суммирует
объемы всех деталей, входящих в состав подсборок.

## 🧾 Пример использования

```lisp
; Создание компонента
(defcomponent "Объем куба" "SmdxElement"
  (let (length width height cube)
    (setq length 1.0
          width  2.0
          height 1.5)
    ; Создание куба
    (setq cube
      (v-extrude
        (v-profile-rect width height)
        (vec length 0.0 0.0)))
    ; Расчет объема куба и сохранение его в глобальную переменную
    (setq *tot_volume* (v-volume cube))
    (defgeometry cube))
  ; Создание свойства только для чтения со значением объема куба
  (setproperty volume *tot_volume* "Объем")) ; В инспекторе свойств отобразится значение 3.0
```

