# 09_minishell

# Парсер

Задача парсера - разделить вводимые данные на токены (то есть на команды с аргументами)

Лексер - функция, которая получает из строки токены. 


Односвязный список в котором будут слова, как связано и с чем



## Разрешенные функции в проекте
| Функции для minishell | Инструкция | Link |
| --- | --- | --- |
| readline (const char *prompt); | Получает данные из командной строки, сохраняет историю, можно обращаться к историческим командам, для введенных char выделяет память через malloc (т.е. надо будет эту память потом освободить) | https://www.opennet.ru/man.shtml?topic=readline&category=3&russian=2 |
| void rl_clear_history (void) | RUS: Очищает историю введенных данных в командную строку, по аналогии с clear_history _ENG: Clear the history list by deleting all of the entries, in the same manner as the History library's clear_history() function. This differs from clear_history because it frees private data Readline saves in the history list._ | https://tiswww.case.edu/php/chet/readline/readline.html |
| int rl_on_new_line (void) | RUS: Сообщает функциям, что мы переместились на новую строку - Обычно после того, как была выведена новая строка _ENG: Tell the update functions that we have moved onto a new (empty) line, usually after outputting a newline._ |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
