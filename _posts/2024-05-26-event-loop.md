---
layout: post
title:  "Event loop"
author: "Evgeniy Petrov"
tags: ["eventloop", "лайфхак"]
---

Допустим, у вас есть админка со странами. Вам нужно удалить все страны, но такой кнопки у вас нет. Чтобы удалить страну, нужно зайти в редактирование, проскроллить страницу вниз, нажать на кнопку “удалить” и потом еще раз нажать на кнопку в окне подтверждения. Вдобавок ко всему, у вас медленный интернет, и дизайнер добавил потрясающие эффекты, которые добавляют задержку в полсекунды на каждое действие (IO Wait). На удаление 9 стран таким образом лично у меня ушло 39 секунд, т.е. 4,33 секунды на каждую страну.

Что делать? К программистам бежать не вариант.

Итак, нам понадобятся:

1. Клавиатура:
   - Ctrl ⌃ + Click — открывает ссылку в отдельной вкладке
   - Ctrl ⌃ + Tab — переходит на следующую вкладку
2. Мелкая моторика рук.

Дальше делаем все пачками — сначала открываем несколько стран, потом все прокручиваем вниз, потом нажимаем на всех кнопку “удалить”, и потом снова нажимаем на всех другую кнопку “удалить”.

В итоге:

- Медленный интернет нам уже не помеха, мы нажимаем на кнопку и сразу переходим к следующей, не дожидаясь загрузки.
- Мы экономим на перемещении курсора (кнопки будут всегда в одном месте).
- Мы удаляем страны со скоростью 1,95 секунд на страну (и это не предел!).

Чуть не забыл, примерно так работают под капотом Nginx, Node.js, Goroutines и многие другие.

P.S. И, пожалуйста, если у вас вдруг появится желание вместо ссылки или submit кнопки сделать свою кнопку с onclick обработчиком, оторвите себе руки.

<iframe width="560" height="315" src="https://www.youtube.com/embed/7nRl2tIxIYE?si=ZIe2dzxKAx64kyWR" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<iframe width="560" height="315" src="https://www.youtube.com/embed/W3nLSGRsbEA?si=WjNLzgepfoYFQNXP" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>