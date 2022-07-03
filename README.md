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
| int rl_on_new_line (void) | RUS: Сообщает функциям, что мы переместились на новую строку - Обычно после того, как была выведена новая строка _ENG: Tell the update functions that we have moved onto a new (empty) line, usually after outputting a newline._ | https://tiswww.case.edu/php/chet/readline/readline.html |
| void rl_replace_line (const char *text, int clear_undo) | RUS: Заменяет содержание rl_line_buffer текстом. Точка и отметка сохраняются, если это возможно. Если значение clear_undo не равно нулю, the undo list, связанный с текущей строкой, очищается.  _ENG: Replace the contents of rl_line_buffer with text. The point and mark are preserved, if possible. If clear_undo is non-zero, the undo list associated with the current line is cleared_ | https://tiswww.case.edu/php/chet/readline/readline.html |
| void rl_redisplay (void) | RUS: Меняет текст, что отражается на экране, чтобы показать с текущее содержание rl_line_buffer  _ENG: Change what's displayed on the screen to reflect the current contents of rl_line_buffer._ | https://tiswww.case.edu/php/chet/readline/readline.html |
| void add_history (char *string) | RUS: Поместить string в конец перечня истории. В связанном поле данных (если оно есть) - устанавливается NULL _ENG: Place **string** at the end of the history list. The associated data field (if any) is set to NULL._ | http://www.math.utah.edu/docs/info/hist_2.html |
| #include<io.h> int access(const char * filename, int amode); | access проверяет файл c именем filename для определения, существует  ли  он,  может  ли он быть прочитан, записан или выполнен. _Список значений параметра amode:  06   проверка разрешения на чтение и запись;                    04   проверка разрешения на чтение;                    02   проверка разрешения на запись;                   01   проверка на выполнение (игнорируется);                    00   проверка на существование файла;            Примечание. Под  управлением  операционной  системы DOS  все  существующие файлы имеют доступ на чтение (amode равен 04),  поэтому 00 и 04 дают один и  тот же результат.  По той же причине значения параметра amode эквивалентны,  поскольку под DOS  доступ  для записи включает и доступ по чтению. Если параметр    filename   является   ссылкой   на директорию,  функция   access   просто   проверяет, существует данная директория или нет._ | http://www.codenet.ru/progr/cpp/spr/005.php |
| #include <sys/types.h> #include <unistd.h> pid_t fork(void);   | fork создает процесс-потомок, который отличается от родительского только значениями PID (идентификатор процесса) и PPID (идентификатор родительского процесса), а также тем фактом, что счетчики использования ресурсов установлены в 0. Блокировки файлов и сигналы, ожидающие обработки, не наследуются. Под Linux fork реализован с помощью "копирования страниц при записи" (copy-on-write, COW), поэтому расходы на fork сводятся к копирования таблицы страниц родителя и созданию уникальной структуры, описывающей задачу | https://www.opennet.ru/man.shtml?topic=fork&category=2 |
| #include <sys/types.h> #include <sys/wait.h> **pid_t wait(int *status)**; **pid_t waitpid(pid_t pid, int *status, int options)**;   | Функция wait приостанавливает выполнение текущего процесса до тех пор, пока дочерний процесс не завершится, или до появления сигнала, который либо завершает текущий процесс, либо требует вызвать функцию-обработчик. Если дочерний процесс к моменту вызова функции уже завершился (так называемый "зомби" ("zombie")), то функция немедленно возвращается. Системные ресурсы, связанные с дочерним процессом, освобождаются. Функция waitpid приостанавливает выполнение текущего процесса до тех пор, пока дочерний процесс, указанный в параметре pid, не завершит выполнение, или пока не появится сигнал, который либо завершает текущий процесс либо требует вызвать функцию-обработчик. Если указанный дочерний процесс к моменту вызова функции уже завершился (так называемый "зомби"), то функция немедленно возвращается. Системные ресурсы, связанные с дочерним процессом, освобождаются. Параметр pid может принимать несколько значений | https://www.opennet.ru/man.shtml?topic=wait&category=2&russian=0 |
| #include <sys/types.h> #include <sys/time.h> #include <sys/resource.h> #include <sys/wait.h> pid_t **wait3(int *status, int options,struct rusage *rusage)**; **pid_t wait4(pid_t pid, int *status, int options, struct rusage *rusage)**; | Функция wait3 приостанавливает исполнение текущего процесса до того, как дочерний процесс завершит свою работу, или он не получит сигнал, прекращающий его работу, или не будет произведен вызов обработчика прерывания. Если дочерний процесс уже прекратил свою работу на момент вызова этой функции (такой процесс называется "зомби" ("zombie")), то функция немедленно возвращается. Все системные ресурсы, использованные дочерним процессом, будут освобождены. Функция wait4 приостанавливает исполнение текущего процесса до того, как свою работу завершит дочерний процесс с номером pid, или этот процесс не получит сигнал, прекращающий его работу, или не будет произведен вызов обработчика прерывания. Если дочерний процесс pid уже прекратил свою работу на момент вызова этой функции (такой процесс называется "зомби"), то функция немедленно возвращается. Все системные ресурсы, использованные дочерним процессом, будут освобождены. | https://www.opennet.ru/man.shtml?topic=wait3&category=2&russian=0 |
| #include <signal.h> typedef void (*sighandler_t)(int); sighandler_t signal(int signum, sighandler_t handler); | Системный вызов signal() устанавливает новый обработчик сигнала с номером signum в соответствии с параметром sighandler, который может быть функцией пользователя, SIG_IGN или SIG_DFL. При получении процессом сигнала с номером signum происходит следующее: если устанавливаемое значение обработчика равно SIG_IGN, то сигнал игнорируется; если оно равно SIG_DFL, то выполняются стандартные действия, связанные с сигналом (см. signal(7)). Наконец, если обработчик установлен в функцию sighandler, то сначала устанавливает значение обработчика в SIG_DFL или выполняется зависимая от реализации блокировка сигнала, а затем вызывается функция sighandler с параметром signum. | https://www.opennet.ru/man.shtml?topic=signal&category=2&russian=0 |
| #include <signal.h> **int sigaction(int signum, const struct sigaction *act, struct sigaction *oldact)**; **int sigprocmask(int how, const sigset_t *set, sigset_t *oldset)**; **int sigpending(sigset_t *set)**; **int sigsuspend(const sigset_t *mask)**;  | Системный вызов sigaction используется для изменения действий процесса при получении соответствующего сигнала. Параметр signum задает номер сигнала и может быть равен любому номеру, кроме SIGKILL и SIGSTOP. Если параметр act не равен нулю, то новое действие, связянное с сигналом signum, устанавливается соответственно act. Если oldact не равен нулю, то предыдущее действие записывается в oldact. | https://www.opennet.ru/man.shtml?topic=sigaction&category=2&russian=0 |
| #include <signal.h> **int sigemptyset(sigset_t *set)**; **int sigfillset(sigset_t *set)**; **int sigaddset(sigset_t *set, int signum)**; **int sigdelset(sigset_t *set, int signum)**; **int sigismember(const sigset_t *set, int signum)**; | Функции sigsetops(3) позволяют производить операции над наборами сигналов POSIX. _sigemptyset_ инициализирует набор сигналов, указанный в set, и "очищает" его от всех сигналов. _sigfillset_ полностью инициализирует набор set, в котором содержатся все сигналы. _sigaddset_ и _sigdelset_ добавляют сигналы signum к set и удаляют эти сигналы из набора соответственно. _sigismember_ проверяет, является ли signum членом set. | https://www.opennet.ru/man.shtml?topic=sigemptyset&category=3&russian=0 | 
| #include <sys/types.h> #include <signal.h> **int kill(pid_t pid, int sig)**; | Системный вызов kill может быть использован для посылки какого-либо сигнала какому-либо процессу или группе процесса. Если значение pid является положительным, сигнал sig посылается процессу с идентификатором pid. Если pid равен 0, то sig посылается каждому процессу, который входит в группу текущего процесса. Если pid равен -1, то sig посылается каждому процессу, за исключением процесса с номером 1 (init), но есть нюансы, которые описываются ниже. Если pid меньше чем -1, то sig посылается каждому процессу, который входит в группу процесса -pid. Если sig равен 0, то никакой сигнал не посылается, а только выполняется проверка на ошибку. | https://www.opennet.ru/man.shtml?topic=kill&category=2&russian=0 |
| #include <unistd.h> #include <stdlib.h> **void _Exit(int status)**; | _exit "немедленно" завершает работу программы. Все дескрипторы файлов, принадлежащие процессу, закрываются; все его дочерние процессы начинают управляться процессом 1 (init), а родительскому процессу посылается сигнал SIGCHLD. Значение status возвращается родительскому процессу как статус завершаемого процесса; он может быть получен с помощью одной из функций семейства wait. Функция _Exit эквивалентна функции _exit.  | https://www.opennet.ru/man.shtml?topic=exit&category=2&russian=0 |
| #include <unistd.h> **char *getcwd(char *buf, size_t size)**; **char *get_current_dir_name(void)**; **char *getwd(char *buf)**; | Функция **getcwd**() копирует абсолютный путь к текущему рабочему каталогу в массиве, на который указывает buf, имеющий длину size. Если текущий абсолютный путь требует буфера, длина которого превышает size, то возвращается NULL, а errno принимает значение ERANGE; приложение должно проверить, возникла эта ошибка или нет и, если необходимо, выделить буфер большего размера. Если buf равно NULL, то поведение getcwd() становится неопределенным. Расширение стандарта POSIX.1 для Linux (libc4, libc5, glibc) предусматривает следующее: если при вызове buf равно NULL, getcwd(), то буфер выделяется динамически с помощью функции malloc(). В этом случае выделенный буфер имеет размер size; если size равно нулю, то выделяется buf необходимого размера. Возможно (и даже рекомендуется) после использования освободить выделенные таким образом буферы с помощью free().  get_current_dir_name (которая имеет прототип только в том случае, если определено значение _GNU_SOURCE) выделит с помощью malloc(3) массив, достаточно большой для помещения в него имени текущего каталога. Если установлена и имеет правильное значение переменная окружения PWD, то будет возвращено ее значение. getwd (имеющая прототип только в том случае, если определено значение _BSD_SOURCE или _XOPEN_SOURCE_EXTENDED) не будет выделять память с помощью malloc(3). Аргумент buf должен быть указателем на массив длиной как минимум PATH_MAX байтов. getwd возвращает только первые PATH_MAX байтов реального пути. | https://www.opennet.ru/man.shtml?topic=getcwd&category=3&russian=0 |
| #include <unistd.h> **int chdir(const char *path)**; **int fchdir(int fd)**; | **chdir** изменяет текущий каталог каталог на path. fchdir идентично chdir, только каталог задан в виде открытого файлового дескриптора. | https://www.opennet.ru/cgi-bin/opennet/man.cgi?topic=chdir&category=2 |
| #include <sys/types.h> #include <sys/stat.h> #include <unistd.h> **int stat(const char *file_name, struct stat *buf)**; **int fstat(int filedes, struct stat *buf)**; **int lstat(const char *file_name, struct stat *buf)**; | Эти функции возвращают информацию об указанном файле. Для этого не требуется иметь права доступа к файлу, хотя потребуются права поиска во всех каталогах, указанных в полном имени файла. stat возвращает информацию о файле file_name и заполняет буфер buf. lstat идентична stat, но в случае символьных сылок она возвращает информацию о самой ссылке, а не о файле, на который она указывает. fstat идентична stat, только возвращается информация об открытом файле, на который указывает filedes (возвращаемый open(2)), а не о file_name. | https://www.opennet.ru/man.shtml?topic=stat&category=2&russian=0 |
|  |  |  |
|  |  |  |
|  |  |  |

##### Отличия wait3 / wait4 от waitpid и wait
В wait3/4 есть аргумент rusage, который в формате структуры возникает из команды getrusage (как я понял)

getrusage возвращает текущие ограничения на ресурсы для who, который может быть или RUSAGE_SELF или RUSAGE_CHILDREN. Первое запрашивает информацию о ресурсах используемых текущим процессом, а второе о тех порожденных процессах, которые завершились или завершение которых ожидается.

struct rusage {
        struct timeval ru_utime;        /* время работы пользователя */
        struct timeval ru_stime;        /* использованное системное время */
        long    ru_maxrss;              /* максимальный rss */
        long    ru_ixrss;               /* общий объем разделяемой памяти */
        long    ru_idrss;               /* общий объем неразделяемых данных */
        long    ru_isrss;               /* общий объем неразделяемых стеков */
        long    ru_minflt;              /* количество процессов подгрузки страницы */
        long    ru_majflt;              /* количество ошибок при обращении к странице */
        long    ru_nswap;               /* количество обращений к диску при подкачке */
        long    ru_inblock;             /* количество операций блокового ввода */
        long    ru_oublock;             /* количество операций блокового вывода */
        long    ru_msgsnd;              /* количество отправленных сообщений */
        long    ru_msgrcv;              /* количество принятых сообщений */
        long    ru_nsignals;            /* количество принятых сигналов */
        long    ru_nvcsw;               /* количество переключений контекста процессом */
        long    ru_nivcsw;              /* количество принудительных переключений контекста */
};

##### Структура для функции stat

Все эти функции возвращают структуру stat, которая содержит следующие поля:

struct stat {
    dev_t         st_dev;      /* устройство */
    ino_t         st_ino;      /* inode */
    mode_t        st_mode;     /* режим доступа */
    nlink_t       st_nlink;    /* количество жестких ссылок */
    uid_t         st_uid;      /* идентификатор пользователя-владельца */
    gid_t         st_gid;      /* идентификатор группы-владельца */
    dev_t         st_rdev;     /* тип устройства */
                               /* (если это устройство) */
    off_t         st_size;     /* общий размер в байтах */
    blksize_t     st_blksize;  /* размер блока ввода-вывода */
                               /* в файловой системе */
    blkcnt_t      st_blocks;   /* количество выделенных блоков */
    time_t        st_atime;    /* время последнего доступа */
    time_t        st_mtime;    /* время последней модификации */
    time_t        st_ctime;    /* время последнего изменения */
};
