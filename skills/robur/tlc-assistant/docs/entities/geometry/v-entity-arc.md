# `v-entity-arc`

## 📦 Функция

```lisp
(v-entity-arc diameter angle span)
(v-entity-arc diameter angle span width)
```

## 📄 Описание

Создание примитива «дуга».

## 📥 Аргументы

- `(double)` `diameter` - диаметр;
- `(double)` `angle` - угол начала дуги;
- `(double)` `span` - градусная мера дуги;
- `(double)` `width` - толщина линии (по умолчанию равна 0.0).

## 📈 Возвращает

`(entity)` Примитив.

## 🧾 Пример использования

```lisp
; Определение вида
(defview
  ; Вид сверху (план)
  (v-top)
  ; Примитив дуга
  (v-entity-arc 1.0 45 135 0.1))
```

