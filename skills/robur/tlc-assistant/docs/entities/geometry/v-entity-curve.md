# `v-entity-curve`

## 📦 Функция

```lisp
(v-entity-curve curve)
(v-entity-curve curve start_trim)
(v-entity-curve curve start_trim end_trim)
(v-entity-curve curve start_trim end_trim width)
(v-entity-curve curve_object)
(v-entity-curve curve_object start_trim)
(v-entity-curve curve_object start_trim end_trim)
(v-entity-curve curve_object start_trim end_trim width)
```

## 📄 Описание

Создание примитива «кривая».

## 📥 Аргументы

- `(curve)` `curve` - кривая;
- `(typed_object)` `curve_object` - объект, представляющий кривую;
- `(double)` `start_trim` - длина усечения кривой с начала (по умолчанию равна 0.0);
- `(double)` `end_trim` - длина усечения кривой с конца (по умолчанию равна 0.0);
- `(double)` `width` - толщина линии (по умолчанию равна 0.0).

## 📈 Возвращает

`(entity)` Примитив.

## 🧾 Пример использования

```lisp
; Определение вида
(defview
  ; Вид сверху (план)
  (v-top)
  ; Примитив кривая
  (v-entity-curve
    (v-curve-arc (vec) (vec 0.0 0.0 1.0) (vec 1.0 0.0) 270)
    1.2 1.2 0.1))
```

