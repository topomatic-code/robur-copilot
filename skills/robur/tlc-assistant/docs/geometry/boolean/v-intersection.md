# `v-intersection`

## 📦 Функция

```lisp
(v-intersection body_1 body_2 … body_N)
```

## 📄 Описание

Выполняет булеву операцию пересечения над 3d-телами.

## 📥 Аргументы

- `(geometry_object)` `body_#` - 3d-тело.

## 📈 Возвращает

`(geometry_object)` Результат пересечения 3d-тел.

## 💬 Примечания

Если тела являются составными (подсборками, состоящими из отдельных деталей) - вычитает
из тел первой подсборки тела остальных подсборок.

## 🧾 Пример использования

```lisp
; Создание компонента
(defcomponent "Пересечение куба и сферы" "SmdxElement"
  (defgeometry
    (let (size radius cube sphere)
      ; Определение размеров куба и сферы
      (setq size   1.5
            radius 1.0)
      ; Создание куба
      (setq cube
        (v-sweep
          (v-profile-rect size size)
          (v-curve-straight
            (vec (- (* 0.5 size)) 0.0 0.0)
            (vec (* 0.5 size) 0.0 0.0))))
      ; Создание сферы
      (setq sphere (v-sphere radius))
      ; Булева операция пересечения куба и сферы
      (v-intersection cube sphere))))
```

