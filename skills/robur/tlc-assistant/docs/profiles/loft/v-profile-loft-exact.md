# `v-profile-loft-exact`

## 📦 Функция

```lisp
(v-profile-loft-exact (cons 0.0 profile_1) (cons u_2 profile_2) ... (cons 1.0 profile_N))
(v-profile-loft-exact transition_func (cons 0.0 profile_1) (cons u_2 profile_2) ... (cons 1.0 profile_N))
```

## 📄 Описание

Создание изменяемого вдоль траектории выдавливания профиля.

## 📥 Аргументы

- `(cons)` `cons_#` - ячейка вида пары «u-профиль»;
- `(lambda)` `transition_func` - фунция перехода между профилями.

## 📈 Возвращает

`(profile)` Профиль.

## 💬 Примечания

Количество контуров, а также количество точек в соответствующих контурах профилей должны совпадать.

Значение u задает положение профиля на траектории выдавливания и может принимать значения от 0.0 до 1.0,
где 0.0 соответствует положению в начале траектории, а 1.0 в конце.

Должно быть задано как минимум 2 профиля: для u = 0.0 и u = 1.0.

При расчете профиля для произвольного u, выбираются два значения: u0 и u1. Где u0 <= u <= u1.

Из профилей, соответствующих u0 и u1, последовательно выбираются пары точек p0 (из профиля u0) и p1 (из профиля u1).

Точка p результирующиего профиля u определяется при помощи линейной интерполляции lerp(p0, p1, t).
Где параметр t - коэффициент интерполляции.

Если transition_func не задана, то рассчитывается как t = (u - u0) / (u1 - u0).

Если transition_func задана, то t = transition_func(u, t). То есть после стандартного расчета t модифицируется возвращаемым значением
пользовательской функции transition_func, позволяя задавать нелинейный переход между профилями.

## 🧾 Пример использования

Создание loft-профиля из трёх квадратных сечений размером 1 × 1 м, 2 × 2 м и 5 × 5 м и его выдавливание вдоль отрезка длиной 2 м:

```lisp
(defcomponent "Loft-операция" "SmdxElement"
  (defgeometry
    (let (profile_1 profile_2 profile_3 multisection_profile)
      ; Определение трех квадратных профилей
      (setq profile_1 (v-profile-rect 1 1)
            profile_2 (v-profile-rect 2 2)
            profile_3 (v-profile-rect 5 5))
      ; Определение loft-профиля, состоящего из 3 сечений
      (setq multisection_profile
        (v-profile-loft-exact (cons 0.0 profile_1)
                              (cons 0.2 profile_2)
                              (cons 1.0 profile_3)))
      (v-sweep
        multisection_profile
        (v-curve-straight (vec 0.0 0.0 0.0) (vec 2.0 0.0 0.0))))))
```

Создание коробчатого пролёта с переходом от профиля 7,5 × 3,5 м к смещённому профилю 7,5 × 1 м по нелинейной функции перехода:

```lisp
(defcomponent "Коробчатый пролет" "SmdxElement"
  (defgeometry
    (let (span_profile_1 span_profile_2 fx transitionCurve)
      (setq span_profile_1  (v-profile-rect 7.5 3.5)
            span_profile_2  (v-profile-translate (v-profile-rect 7.5 1.0) (vec 0.0 1.25))
            fx              (lambda (t) (* t t))
            transitionCurve (lambda (u t) (if (< u 0.5) (- 1.0 (fx (- 1.0 t))) (fx t))))
      (v-sweep
        (v-profile-loft-exact
          transitionCurve
          (cons 0.0 span_profile_1)
          (cons 0.5 span_profile_2)
          (cons 1.0 span_profile_1))
        (v-curve-straight (vec 0.0 0.0 0.0) (vec 20.0 0.0 0.0))))))
```
