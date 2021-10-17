# Инструкция по работе с Git

## `Что такое Git`?
**Git** - одна из реализаций распределенных систем контроля версий. Позволяет контролировать версионность файлов как локально, так и на удаленном сервере. Самая популярная система контроля версий.

## `Первоначальная настройка`
Сначала нужно указать информацию о пользователе локальных репозиториев. Это делается с помощью команд

>git config --global user.name "имя"

>git config --global user.email "почта"

## `Подготовка репозитория`
**Репозиторий** - это хранилище файлов, поддерживающее версионность. Создать репозиторий в папке можно с помощью команды *`git init`*, применив эту команду в папке с репозиторием.

Для просмотра текущего состояния репозитория и проверки наличия в нем изменений, а также файлов, которые необходимо зафиксировать, использовать команду

>git status

## `Создание "сохранений"`
Перед тем, как создавать "сохранение", нужно добавить все новые или измененные файлы в отслеживание с помощью команды *`git add`*. Команда имеет вид:
>git add <имя файла.расширение>

Создать "сохранения", они же фиксации или коммиты мы можем с помощью команды *`git commit`*. Для этого необходимо написать команду 
>*git commit -m <сообщение коммита>*. 

Сообщение к коммиту писать **ОБЯЗАТЕЛЬНО**. Все файлы должны быть добавлены в коммит с помощью команды *`git add`*. Если файлы не добавлены, то можно использовать флаг *`-а`* и команда приобретет вид 
>*git commit -а -m <сообщение коммита>*

## `Журнал изменений`
Чтобы просмотреть журнал всех изменений (коммитов), необходимо использовать команду *`git log`*. При этом будет выведен список всех коммитов, у каждого коммита есть свой хэш-код или номер, используя который можно выполнять операции с коммитами (переключение, удаление).
Чтобы просмотреть журнал изменений с графическим отображением веток, необходимо добавить флаг *`--graph`* и команда прибретет вид 
>*git log --graph*.

## `Перемещение между "сохранениями"`
Для переключения между "сохранениями" (коммитами) необходимо использовать команду *`git checkout`* следующим образом: 
>*git checkout <номер коммита для переключения>*. 

Номер коммита, на который нужно переключиться, берется из истории коммитов. Для переключения между коммитами достаточно использовать первые 4-5 символов идентификатора коммита.
Для возврата в главную ветку необходимо использовать команду *`git checkout master`*

Команды *`git reset`* и *`git revert`* позволяют отменять изменения. Команда *git revert* возвращает к указанному коммиту, создавая новый коммит, а команда *git reset* возвращает к указанному коммиту, затирая историю изменений до указанного коммита. Применяются эти команды следующим образом:
>*git revert <номер коммита>* 

или 
>*git reset --hard <номер коммита>*

## `Ветки в Git`
Чтобы просмотреть все имеющиеся в репозитории ветки, необходимо использовать команду *`git branch`*. При этом текущая ветка будет выделена зеленым цветом и звездочкой.
Чтобы создать новую ветку, необходимо использовать команду 
>*git branch <имя новой ветки>*.

Чтобы переключиться между ветками, необходимо использовать команду *`git checkout`*
>*git checkout <имя ветки, на которую нужно переключиться>*.

## `Слияние веток и решение конфликтов`
Чтобы выполнить слияние двух веток, необходимо проверить, сохранена ли в них вся информация. Затем необходимо переключиться на главную ветку, в которую будут добавлены изменения из другой ветки. Слияние веток выполняется с помощью команды 
>*git merge <имя другой ветки>*.

Если над файлом одновременно велась работа в разных ветках и информация отличается, то при слиянии веток непременно возникнет **КОНФЛИКТ**! Система предлагает несколько вариантов:

* оставить изменения только из текущей ветки
* оставить изменения только из другой ветки
* оставить изменения из обеих веток
* сравнить в графическом виде, чем отличаются файлы из разных веток

Если ни один из предложенных системой вариантов не подходит, ответственное лицо должно решить конфликт **вручную**, сравнив изменения в файлах из разных веток и оставив только то, что нужно. После того, как файл будет отредактирован вручную, необходимо добавить новый коммит!

## `Удаление веток`
Чтобы удалить ненужную ветку, необходимо выйти в главную ветку и выполнить команду 
>*git branch -d <имя удаляемой ветки>*

## `Скачивание удаленного репозитория`
Чтобы скачать удаленный репозиторий, необходимо создать для него папку, зайти в нее и выполнить команду
>*git clone <URL адрес удаленного репозитория>*

## `Отправка изменений в удаленный репозиторий`
Чтобы отправить файлы локального репозитория в удаленный репозиторий, необходимо выполнить команды:
Связываем наш локальный репозиторий с удаленным репозиторием с помощью команды
>*git remote add origin <URL адрес удаленного репозитория на github>*

Далее указываем ветку, которую будем использовать в качестве основной
>*git branch -M main*

Далее когда наш локальный репозиторий уже подружился с удаленным репозиторием, непосредственно отправка изменений в удаленный репозиторий осуществляется командой 
>*git push -u origin main*

## `Скачивание изменений из удаленного репозитория`
Чтобы скачать актуальную версию файлов из удаленного репозитория, необходимо выполнить команду:
>*git pull*

PS при этом команда *`git pull`* пытается выполнить операцию *`merge`* с файлами локального репозитория.