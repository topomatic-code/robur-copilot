# Проверка доступности функционала (функций, макросов, констант, системных переменных и т.д.)

## 🧷 Тема

Проверка доступности функционала (функций, макросов, констант, системных переменных и т.д.).

## 📝 Описание

Необходимость проверки доступности функций, констант и системных переменных может возникать в случаях, когда скрипт
приходится выполнять на различных версиях платформы Topomatic Robur. В более новых версиях может появляться новый функционал.
Реализовать такую проверку можно при помощи функции dump, которая возвращает список всех определенных в текущем скрипте идентификаторов (symbol's).

## 🟢 GOOD (PATTERN)

```lisp
(defun has-symbol (symbol_name)
  (defun next (symbols)
    (if symbols
      (if (eql (symbol-name (car symbols)) symbol_name)
        true
        (next (cdr symbols)))
      false))
  (next (dump)))
(defcomponent "Symbols check" "SmdxElement"
  (print (has-symbol "v-union")) ; -> true
  (print (has-symbol "super-function"))) ; -> false
```

