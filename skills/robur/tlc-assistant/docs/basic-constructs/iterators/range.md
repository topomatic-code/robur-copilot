# `range`

## 📦 Функция

```lisp
(range end_number)
(range start_number end_number)
(range start_number end_number step)
```

## 📄 Описание

Получение упорядоченной коллекции чисел.

## 📥 Аргументы

- `(integer)` `start_number` - число начала перечисления, по умолчанию равно `0`;
- `(integer)` `end_number` - число конца перечисления;
- `(integer)` `step` - шаг перечисления, по умолчанию `1`.

## 📈 Возвращает

`(iterator)` Набор значений.

## 🧾 Пример использования

```lisp
(let
  ; Создание коллекций
  (
    (numbers_1 (range 5))
    (numbers_2 (range 5 10))
    (numbers_3 (range 5 10 2)))
  ; Вывод в окно командной строки значений коллекций
  (print "Коллекция 1:")
  (v-for
    (number numbers_1)
    (princ (format "{0} " number)))
  (terpri)

  (print "Коллекция 2:")
  (v-for
    (number numbers_2)
    (princ (format "{0} " number)))
  (terpri)

  (print "Коллекция 3:")
  (v-for
    (number numbers_3)
    (princ (format "{0} " number)))
  (terpri))

; Результат вывода в окно командной строки:
; "Коллекция 1:"
; 0 1 2 3 4
; "Коллекция 2:"
; 5 6 7 8 9
; "Коллекция 3:"
; 5 7 9
```

