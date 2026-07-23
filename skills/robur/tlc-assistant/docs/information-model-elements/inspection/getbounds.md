# `getbounds`

## 📦 Функция

```lisp
(getbounds im_element)
```

## 📄 Описание

Определение размера элемента информационной модели.

## 📥 Аргументы

- `(im_element)` `im_element` - элемент информационной модели.

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
                    (vec 1 0))))
    ; Определение элемента ИМ
    im_element (defelement component))
  ; Вывод размера элемента в окно командной строки
  (print (getbounds im_element)))
; Результат вывода в окно командной строки:
; (1.0 0.200000002980232 0.200000002980232)
```

