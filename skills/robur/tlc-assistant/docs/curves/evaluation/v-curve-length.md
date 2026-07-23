# `v-curve-length`

## 📦 Функция

```lisp
(v-curve-length curve)
(v-curve-length curve_object)
```

## 📄 Описание

Вычисление длины кривой.

## 📥 Аргументы

- `(curve)` `curve` - кривая;
- `(typed_object)` `curve_object` - объект, представляющий кривую.

## 📈 Возвращает

`(double)` Длина кривой.

## 🧾 Пример использования

```lisp
(let
  ; Создание кривой
  ((curve (v-curve-arc (vec) (vec 0 0 1) (vec 10.0 5.0) 135)))
  ; Вывод в окно командной строки
  (print
    ; Длина кривой
    (v-curve-length curve)))
; Результат вывода в командную строку:
; 26.3430552414027
```

