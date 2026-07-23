# `v-phong`

## 📦 Функция

```lisp
(v-phong name diffuse)
(v-phong name diffuse ambient)
(v-phong name diffuse ambient specular)
(v-phong name diffuse ambient specular transparency)
(v-phong name diffuse ambient specular transparency specular_level)
(v-phong name diffuse ambient specular transparency specular_level shininess)
```

## 📄 Описание

Определение стиля окрашивания.

## 📥 Аргументы

- `(string)` `name` - имя стиля;
- `(vector3)` `diffuse` - основной цвет;
- `(vector3)` `ambient` - фоновый подсвет;
- `(vector3)` `specular` - отражения;
- `(double)` `transparency` - прозрачность;
- `(double)` `specular_level` - интенсивность отражения;
- `(double)` `shininess` - степень гладкости поверхности (жесткость блика).

## 📈 Возвращает

`(style)` Стиль.

## 🧾 Пример использования

Создание Phong-стиля с чёрным основным цветом:

```lisp
; Стиль с черным цветом
(v-phong "Цвет" (vec 0.0 0.0 0.0))
```

Создание Phong-стиля с белым основным цветом:

```lisp
; Стиль с белым цветом
(v-phong "Цвет" (vec 1.0 1.0 1.0))
```

Создание Phong-стиля с красным основным цветом:

```lisp
; Стиль с красным цветом
(v-phong "Цвет" (vec 1.0 0.0 0.0))
```

Создание Phong-стиля с зелёным основным цветом:

```lisp
; Стиль с зеленым цветом
(v-phong "Цвет" (vec 0.0 1.0 0.0))
```

Создание Phong-стиля с синим основным цветом:

```lisp
; Стиль с синим цветом
(v-phong "Цвет" (vec 0.0 0.0 1.0))
```

Создание Phong-стиля с тёмно-фиолетовым основным цветом:

```lisp
; Стиль с тёмно-фиолетовым цветом
(v-phong "Цвет" (vec 0.4 0.0 0.6))
```

