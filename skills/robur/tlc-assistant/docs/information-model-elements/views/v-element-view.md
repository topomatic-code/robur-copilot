# `v-element-view`

## 📦 Функция

```lisp
(v-element-view im_element view)
```

## 📄 Описание

Получение вида элемента информационной модели.

## 📥 Аргументы

- `(im_element)` `im_element` - элемент информационной модели;
- `(view)` `view` - вид.

## 📈 Возвращает

`(geometry_object)` Объект, не имеющий 3д представления, но имеющий 2д отрисовку.

## 🧾 Пример использования

```lisp
; Определение вида компонента
(defview
  ; Вид сверху
  (v-top)
  (let
    ; Объявление переменных
    (component im_element)
    (setq
      ; Определение компонента
      component (defcomponent "Балка" "SmdxElement"
                  (defgeometry
                    (v-extrude
                      (v-profile-p 0.01 0.2)
                      (vec 0 1))))
      ; Определение элемента ИМ
      im_element (defelement component))
    ; Получение вида спереди элемента ИМ
    (v-element-view im_element (v-front))))
```

