# `enum-get`

## 📦 Функция

```lisp
(enum-get collection)
```

## 📄 Описание

Получение итератора коллекции.

## 📥 Аргументы

- `(dynamic)` `collection` - коллекция значений.

## 📈 Возвращает

`(iterator)` Итератор.

## 🧾 Пример использования

```lisp
(let
  ; Создание коллекций
  (
    ; Словарь
    (dic (dict "key_1" "value_1" "key_2" "value_2"))
    ; Список
    (lst (list "value_1" "value_2" "value_3"))
    ; Массив
    (arr (array "value_1" "value_2" "value_3")))
  ; Получение перечислителя словаря
  (enum-get dic)
  ; Получение перечислителя списка
  (enum-get lst)
  ; Получение перечислителя массива
  (enum-get arr))
```

