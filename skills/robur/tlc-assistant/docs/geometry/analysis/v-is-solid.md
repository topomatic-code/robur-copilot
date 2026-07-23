# `v-is-solid`

## 📦 Функция

```lisp
(v-is-solid body_1 body_2 … body_N)
(v-is-solid bodies)
```

## 📄 Описание

Проверяет являются ли геометрические объекты корректными твердыми телами (manifold).

## 📥 Аргументы

- `(geometry_object)` `body_#` - 3d-тело;
- `(list)` `bodies` - список 3d-тел.

## 📈 Возвращает

`(bool)` Результат проверки.

## 💬 Примечания

Если объект является корректным твердым телом, значит он будет корректно работать
в булевых операциях и по нему будет корректно рассчитываться объем.

## 🧾 Пример использования

```lisp
; Создание компонента
(defcomponent "Куб" "SmdxElement"
  (let (length width height cube)
    (setq length 1.0
          width  2.0
          height 1.5)
    ; Создание куба
    (setq cube
      (v-extrude
        (v-profile-rect width height)
        (vec length 0.0 0.0)))
    ; Проверка является ли куб твердым телом
    ; с сохранением результата в глобальную переменную
    (setq *is_solid* (v-is-solid cube))
    (defgeometry cube))
  ; Создание свойства только для чтения с результатом проверки
  (setproperty is_solid *is_solid* "Тело"))
```

