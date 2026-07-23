# `v-element-viewbounds`

## 📦 Функция

```lisp
(v-element-viewbounds im_element view)
```

## 📄 Описание

Определение размера вида элемента информационной модели.

## 📥 Аргументы

- `(im_element)` `im_element` - элемент информационной модели;
- `(view)` `view` - вид.

## 📈 Возвращает

`(list)` Список со значениями (ширина, высота, глубина).

## 🧾 Пример использования

```lisp
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
  ; Вывод размера вида спереди элемента ИМ в окно командной строки
  (print (v-element-viewbounds im_element (v-front))))
; Результат вывода в окно командной строки:
; (0.200000002980232 0.200000002980232)
```

