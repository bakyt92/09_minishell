# 09_minishell

# Парсер

Задача парсера - разделить вводимые данные на токены (то есть на команды с аргументами)

Лексер - функция, которая получает из строки токены. 


Односвязный список в котором будут слова, как связано и с чем



## Разрешенные функции в проекте
| Функции для minishell | Инструкция | Link |
| --- | --- | --- |
| readline (const char *prompt); | Получает данные из командной строки, сохраняет историю, можно обращаться к историческим командам, для введенных char выделяет память через malloc (т.е. надо будет эту память потом освободить) _ENG: readline will read a line from the terminal and return it, using prompt as a prompt. If prompt is NULL or the empty string, no prompt is issued. The line returned is allocated with malloc(3); the caller must free it when finished. The line returned has the final newline removed, so only the text of the line remains. readline offers editing capabilities while the user is entering the line. By default, the line editing commands are similar to those of emacs. A vi-style line editing interface is also available_ | https://www.opennet.ru/man.shtml?topic=readline&category=3&russian=2 |
| void rl_clear_history (void) | RUS: Очищает историю введенных данных в командную строку, по аналогии с clear_history _ENG: Clear the history list by deleting all of the entries, in the same manner as the History library's clear_history() function. This differs from clear_history because it frees private data Readline saves in the history list._ | https://tiswww.case.edu/php/chet/readline/readline.html |
| int rl_on_new_line (void) | RUS: Сообщает функциям, что мы переместились на новую строку - Обычно после того, как была выведена новая строка _ENG: Tell the update functions that we have moved onto a new (empty) line, usually after outputting a newline._ |  |
| void rl_replace_line (const char *text, int clear_undo) | RUS: Заменяет содержание rl_line_buffer текстом. Точка и отметка сохраняются, если это возможно. Если значение clear_undo не равно нулю, the undo list, связанный с текущей строкой, очищается.  _ENG: Replace the contents of rl_line_buffer with text. The point and mark are preserved, if possible. If clear_undo is non-zero, the undo list associated with the current line is cleared_ |  |
| void rl_redisplay (void) | RUS: Меняет текст, что отражается на экране, чтобы показать с текущее содержание rl_line_buffer  _ENG: Change what's displayed on the screen to reflect the current contents of rl_line_buffer._ |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
