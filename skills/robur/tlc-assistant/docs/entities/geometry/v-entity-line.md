# `v-entity-line`

## 📦 Функция

```lisp
(v-entity-line start_vector end_vector)
(v-entity-line start_vector end_vector width)
```

## 📄 Описание

Создание примитива «отрезок».

## 📥 Аргументы

- `(vector3)` `start_vector` - вектор начала отрезка;
- `(vector3)` `end_vector` - вектор конца отрезка;
- `(double)` `width` - толщина линии (по умолчанию равна 0.0).

## 📈 Возвращает

`(entity)` Примитив.

## 🧾 Пример использования

```lisp
; Определение вида
(defview
  ; Вид сверху (план)
  (v-top)
  ; Примитив отрезок
  (v-entity-line (vec -0.5 -0.25) (vec 0.5 0.25) 0.15))
```

