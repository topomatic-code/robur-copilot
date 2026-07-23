# `defview`

## 📦 Функция

```lisp
(defview side entity_1 entity_2 ... entity_N)
```

## 📄 Описание

Определение вида компонента.

## 📥 Аргументы

- `(side)` `side` - сторона вида;
- `(dynamic)` `entity_#` - примитив. Может принимать тип `entity` или `view`.

## 📈 Возвращает

`nil`.

## 🧾 Пример использования

```lisp
(setq
  ; Определение компонента
  component (defcomponent "Балка" "SmdxElement"
              (defgeometry
                (v-extrude
                  (v-profile-p 0.02 0.4)
                  (vec 0 1))))
  ; Определение элемента ИМ
  im_element (defelement component))
; Определение вида
(defview
  ; Вид сверху (план)
  (v-top)
  ; Примитив кривая
  (v-entity-curve
    (v-curve-arc (vec) (vec 0.0 0.0 1.0) (vec 0.5 0.0) 270)
    0.6 0.6 0.1)
  ; Примитив кривая
  (v-entity-curve
    (v-curve-arc (vec) (vec 0.0 0.0 1.0) (vec -0.5 0.0) 270)
    0.6 0.6 0.1)
  ; Вид спереди элемента ИМ
  (v-element-view im_element (v-front)))
```
