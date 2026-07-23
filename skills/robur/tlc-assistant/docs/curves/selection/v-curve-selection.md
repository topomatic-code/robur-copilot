# `v-curve-selection`

## 📦 Функция

```lisp
(v-curve-selection curve tolerance map)
(v-curve-selection curve tolerance map start_parameter)
(v-curve-selection curve tolerance map start_parameter end_parameter)
(v-curve-selection curve tolerance map start_parameter end_parameter mode)
(v-curve-selection curve_object tolerance map)
(v-curve-selection curve_object tolerance map start_parameter)
(v-curve-selection curve_object tolerance map start_parameter end_parameter)
(v-curve-selection curve_object tolerance map start_parameter end_parameter mode)
```

## 📄 Описание

Разбивка кривой на участки.

## 📥 Аргументы

- `(curve)` `curve` - кривая;
- `(typed_object)` `curve_object` - объект, представляющий кривую;
- `(double)` `tolerance` - допуск отклонения от прямого направления при разбивке;
- `(map)` `map` - карта разбивки. Словарь пар ключ-значение типа «double-body», где ключами являются допустимые величины участков для разбивки;
- `(double)` `start_parameter` - параметр кривой начала разбивки (по умолчанию равен 0.0);
- `(double)` `end_parameter` - параметр кривой конца разбивки (по умолчанию равен 1.0);
- `(int)` `mode` - режим (по умолчанию равен 0). Доступные значения:
                                             - 0 - Равномерная раскладка с учётом вертикальной составляющей;
                                             - 1 - Равномерная раскладка без учёта вертикальной составляющей;
                                             - 2 - Раскладка встык с учётом вертикальной составляющей;
                                             - 3 - Раскладка встык без учёта вертикальной составляющей.

## 📈 Возвращает

`(list)` Перечень массивов, содержащих:
       1. Параметр кривой начала участка;
       2. Параметр кривой конца участка;
       3. Длина участка из словаря map;
       4. Объект соответствующий длине участка из словаря map.

## 🧾 Пример использования

```lisp
; Раскладка труб длиной 2.5, 5.0 и 10.0 метров вдоль кривой
(setq
  ; Компонент трубы длиной 2,5 метра жёлтого цвета
  pipe_2_5 (defcomponent "Pipe_2.5m" "SmdxElement"
           (defgeometry
             (v-styled (v-phong "Жёлтый" (vec 1 1 0))
               (v-extrude (v-profile-round 0.4) (vec 0 2.5 0)))))
  ; Компонент трубы длиной 5 метров голубого цвета
  pipe_5 (defcomponent "Pipe_5m" "SmdxElement"
           (defgeometry
             (v-styled (v-phong "Голубой" (vec 0 1 1))
               (v-extrude (v-profile-round 0.4) (vec 0 5 0)))))
  ; Компонент трубы длиной 10 метров фиолетового цвета
  pipe_10 (defcomponent "Pipe_10m" "SmdxElement"
           (defgeometry
             (v-styled (v-phong "Фиолетовый" (vec 1 0 1))
               (v-extrude (v-profile-round 0.4) (vec 0 10 0)))))
  ; Карта разбивки
  ; Ключи — величины участков для разбивки
  ; Значения — элемент информационной модели
  map (dict
        ; Ключ    ; Значение
        2.5       (defelement pipe_2_5)
        5.0       (defelement pipe_5)
        10.0      (defelement pipe_10)))
; Определение компонента
(defcomponent "My Custom Construction" "SmdxElement"
  ; Свойство позволяющее получить кривую из линейного объекта
  (defproperty axis_curve nil "Ось" (v-property-typed "SmdxPolyline"))
  ; Определение геометрии
  (defgeometry
    (let
      ; Объявление временных переменных
      (
        selection start_param end_param im_element
        start_point end_point ox oy oz)
      ; Разбивка кривой на участки от начала до конца
      ; с допуском отклонения 1 мм от прямого направления
      ; без равномерного распределения по длине кривой (встык)
      (setq
        selection (v-curve-selection axis_curve 0.001 map 0.0 0.0 2))
      ; Обработка результатов разбивки
      (v-for
        (
          ; Временная переменная участка
          sector
          ; Коллекция участков
          selection)
        (setq
          ; Параметр кривой в начале участка
          start_param (car sector)
          ; Параметр кривой в конце участка
          end_param (cadr sector)
          ; Элемент ИМ для вставки соответствующий
          ; длине участка из карты разбивки
          im_element (cadddr sector)
          ; Точка начала участка на кривой
          start_point (v-curve-d0 axis_curve start_param)
          ; Точка конца участка на кривой
          end_param (v-curve-d0 axis_curve end_param)
          ; Вектор направления участка
          ox (vec-normalize (vec-sub start_point end_param))
          ; Вектор направления элемента ИМ
          oy (vec-normalize (vec-cross (vec 0 0 1) ox))
          ; Вектор нормали плоскости
          oz (vec-cross ox oy))
        ; Расположение элемента ИМ в пространстве
        (v-align start_point oz oy
          ; Вставка элемента ИМ
          (setelement "pipe" im_element))))))
```

