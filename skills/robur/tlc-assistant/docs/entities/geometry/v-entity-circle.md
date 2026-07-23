# `v-entity-circle`

## 📦 Функция

```lisp
(v-entity-circle diameter)
(v-entity-circle diameter width)
```

## 📄 Описание

Создание примитива «круг».

## 📥 Аргументы

- `(double)` `diameter` - диаметр;
- `(double)` `width` - толщина линии (по умолчанию равна 0.0).

## 📈 Возвращает

`(entity)` Примитив.

## 🧾 Пример использования

```lisp
; Определение вида
(defview
  ; Вид сверху (план)
  (v-top)
  ; Примитив круг
  (v-entity-circle 1.0 0.1))
```

