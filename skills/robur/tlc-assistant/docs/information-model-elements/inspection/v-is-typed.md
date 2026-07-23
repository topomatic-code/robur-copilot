# `v-is-typed`

## 📦 Функция

```lisp
(v-is-typed smdx_type typed_object)
```

## 📄 Описание

Проверка на соответствие типа объекта указанному Smdx-типу.

## 📥 Аргументы

- `(string)` `smdx_type` - Smdx-тип;
- `(typed_object)` `typed_object` - проверяемый объект.

## 📈 Возвращает

`(bool)` Логическое (истина/ложь).

## 🧾 Пример использования

```lisp
(let
  ; Создание элемента типа "SmdxPoint"
  ((element (v-object-typed "SmdxPoint")))
  ; Вывод в окно командной строки
  (print
    (format
      "Соответствие элемента типу SmdxEntity: {0}"
      (v-is-typed "SmdxEntity" element)))
  (print
    (format
      "Соответствие элемента типу SmdxPoint: {0}"
      (v-is-typed "SmdxPoint" element))))
; Результат вывода в окно командной строки:
; "Соответствие элемента типу SmdxEntity: false"
; "Соответствие элемента типу SmdxPoint: true"
```

