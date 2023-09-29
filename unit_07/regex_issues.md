# Вопросы и задания по теме [регулярные выражения](./regex.md)

Шестнадцатиричный цвет.
Символ `#` (необязательно), затем слово, состоящее из букв от `a` до `f` или цифр, длиной `3` или `6`.
`#FFFFFF` `#000` `101011`

---

XML тэг.
За открывающей скобкой `<` должно стоять слово из букв — имя элемента,
затем могут быть атрибуты — любые символы, кроме закрывающей скобки `>`.
Далее — любой текст (содержимое) и закрывающий тэг, т.е. `<имя />`, или как минимум один пробел,
слэш и закрывающаю скобка (самозакрывающийся тэг).

---

Email.
Общий вид — `логин@поддомен.домен`.
Логин, как и поддомен — слова из букв, цифр, подчёркиваний, дефисов и точек.
А домен (имеется в виду 1го уровня) — это от `2` до `6` букв и точек.

---

URL.
Первым делом — необязательный протокол (`http://` или `https://`),
затем последовательность букв, цифр, дефисов, подчёркиваний и точек (домены уровня > 1),
потом домен нулевого уровня (от `2` до `6` букв и точек) и, наконец, файловая структура —
набор слов из букв, цифр, дефисов, подчёркиваний и точек со слэшем в конце.
Всё это может завершаться опять-таки слэшем.

---

IP адрес.
4 группы цифр (от `1` до `3` цифр в каждой) разделены точками.
Группа содержит число в диапазоне от 1 до 255.

---

### [Назад к оглавлению](./README.md)