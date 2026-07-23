# `v-simplify`

## 📦 Функция

```lisp
(v-simplify body_1 body_2 … body_N)
(v-simplify bodies)
```

## 📄 Описание

Упрощает переданные тела.

## 📥 Аргументы

- `(geometry_object)` `body_#` - 3d-тело;
- `(list)` `bodies` - список 3d-тел.

## 📈 Возвращает

`(geometry_object)` Составной геометрический объект (подсборку) с упрощенными 3d-телами.

## 💬 Примечания

Объединяет соседние грани твердотельной (brep) модели, лежащие в одной плоскости.
Уменьшает общий вес тел и количество полигонов у их 3д моделей.

## 🧾 Пример использования

Упрощение двух тел, каждое из которых получено объединением двух кубов; тела передаются отдельными аргументами:

```lisp
; Создание компонента
(defcomponent "Упрощение твердого тела" "SmdxElement"
  (defgeometry
    (let (size cube cube_1 cube_2 cube_3 cube_4)
      ; Определение размера куба
      (setq size 1.5)
      ; Создание прототипа куба
      (setq cube
        (v-sweep
          (v-profile-rect size size)
          (v-curve-straight
            (vec (- (* 0.5 size)) 0.0 0.0)
            (vec (* 0.5 size) 0.0 0.0))))
      ; Создание копий куба в нужных координатах
      (setq cube_1 (v-translate (vec (* size -0.5) (- (* size -0.5) 0.1) 0.0) cube))
      (setq cube_2 (v-translate (vec (* size  0.5) (- (* size -0.5) 0.1) 0.0) cube))
      (setq cube_3 (v-translate (vec (* size -0.5) (+ (* size  0.5) 0.1) 0.0) cube))
      (setq cube_4 (v-translate (vec (* size  0.5) (+ (* size  0.5) 0.1) 0.0) cube))
      ; Упрощение твердых тел
      (v-simplify
        ; После объединения двух кубов у твердого тела появятся грани,
        ; лежащие в одной плоскости, которые можно объединить
        (v-union cube_1 cube_2)
        ; После объединения двух кубов у твердого тела появятся грани,
        ; лежащие в одной плоскости, которые можно объединить
        (v-union cube_3 cube_4)))))
```

Упрощение тех же двух тел, переданных функции в виде списка:

```lisp
; Создание компонента
(defcomponent "Упрощение твердого тела" "SmdxElement"
  (defgeometry
    (let (size cube cube_1 cube_2 cube_3 cube_4 bodies)
      ; Определение размера куба
      (setq size 1.5)
      ; Создание прототипа куба
      (setq cube
        (v-sweep
          (v-profile-rect size size)
          (v-curve-straight
            (vec (- (* 0.5 size)) 0.0 0.0)
            (vec (* 0.5 size) 0.0 0.0))))
      ; Создание копий куба в нужных координатах
      (setq cube_1 (v-translate (vec (* size -0.5) (- (* size -0.5) 0.1) 0.0) cube))
      (setq cube_2 (v-translate (vec (* size  0.5) (- (* size -0.5) 0.1) 0.0) cube))
      (setq cube_3 (v-translate (vec (* size -0.5) (+ (* size  0.5) 0.1) 0.0) cube))
      (setq cube_4 (v-translate (vec (* size  0.5) (+ (* size  0.5) 0.1) 0.0) cube))
      (setq bodies
        (list
          ; После объединения двух кубов у твердого тела появятся грани,
          ; лежащие в одной плоскости, которые можно объединить
          (v-union cube_1 cube_2)
          ; После объединения двух кубов у твердого тела появятся грани,
          ; лежащие в одной плоскости, которые можно объединить
          (v-union cube_3 cube_4)))
      ; Упрощение твердых тел
      (v-simplify bodies))))
```

