![logo](logo.jpeg)
# Работа с GIT
## 1. Проверка наличия установленного GIT
В терминале выполнить команду `git --version`. Если GIT установлен, появится сообщеие о версии программы, иначе будет сообщение об ошибке.

## Установка  GIT
  Загружаем последнюю версию GIT с [сайта] (http://git-scm.com/downloads)
Устанавливаем с настройками по умолчанию.

## Настройка Git
Для нстрйоки Git необходимо представиться. Для этого открываем консоль (терминал) и выводим следующие команды:
> git config --global user.name "<ваше_имя>"

> git config --global user.email "<адрес_почты@email.com>"

## Подготовка (создание) репозитория
Для создания репозитария, открываем нужную папку (файл) и набираем команду: 
> `git init`

## Добавление изменений
Чтобы добавить изменения в файл необходимо написать команду:
> git add `<имя_файла>`

или 
> git add . или git add --all
## Создание коммитов
Для создания коммитов необходимо написать команду:
> git commit -m "`<комментарий>`"
## Просмотр состояния репозитория
Для просмотра состояния репозитария пишем:
> git status

## Просмотр истории коммитов
Для просмотра всех выполненных фиксаций можно воспользоваться историей коммитов. Она содержит сведения о каждом проведенном коммите проекта. Запросить ее можно при помощи команды:

`git log`

В ней содержится вся информация о каждом отдельном коммите, с указанием его хэша, автора, списка изменений и даты, когда они были сделаны. 

## Перемещение между сохранениями
Отследить интересующие вас операции в списке изменений, можно по хэшу коммита, при помощи команды **git show** :
``git show hash_commit``
Ну а если вдруг нам нужно переделать commit message и внести туда новый комментарий, можно написать следующую конструкцию:
``git commit --amend -m 'Новый комментарий'``

В данном случае сообщение последнего коммита перезапишется. Но злоупотреблять этим не стоит, поскольку эта операция опасная и лучше ее делать до отправки коммита на сервер.

## Игнорирование файлов
Для того, чтобы исключить из отслеживания файлы или папки, необходимо создать файл `gitignore` и записать в него их названия или шаблоны, соответствующие папкам или файлам.

## Создание веток
По умолчанию имя основной ветки в Git - `master`
Создать ветку можно командой:
```Bash
git branch <имя новой ветки>
```

Список веток в репозитории можно посмотреть с помощью команды:
```Bash
git branch
```
Текущая ветка будет отмечена звездочкой: **\**master***

Для создания ветки и перехода в нее также можнос использовать команду:
![command](Screenshot.png)
или
```Bash
git checkout -b <имя ветки>
```
Если нужно получить список определенного множества веток, то тогда можно воспользоваться ключами. Одними из самых распространенных будут:
 - `r`  — при использовании этого ключа мы получим список удаленных веток,
- `a` — используя этот параметр, в выводе будут удаленные и локальные ветки.

## Слияние веток и разрешение конфликтов
Для слияния выбранной ветки с текущей нужно выполнить команду:
```Bash
git merge <название выбранной ветки>
```
Если была изменена одна и таже часть файла в обеих ветках, то может возникнуть конфликт, который потребует участия пользователя. VSCode предлагает варианты разрешения.
После разрешения конфликта нужно выполнить коммит слияние.

## Удаление веток
Для удаления ветки нужно набрать команду:
`git branch -d <имя ветки>`
Необходимо помнить: 
1. Нельзя удалить ветку, в которой находишься.
2. Git не позволит удалить ветку, в которой есть несохраненные изменения.
Если же мы уверены, что изменения в этой версии не нужны и их можно смело удалять, то вместо флага `-d` используем `-D`:
```Bash
git branch -D <имя ветки>
```

## Работа с удаленным репозиторием

1. Создать аккаунт на Github
2. Создать локальный репозиторий
3. Создать удаленный репозиторий
4. Связать удаленный репозиторий с локальным

Добавить удаленный репозиторий к проекту:
```Bash
git remote add <имя репозитория> <URL адрес репозитория в сети>
```
Для получения и слияния изменений из удаленного репозитория используется команда:
`git pull`
Отправить изменения локального репозитория в удаленный: `git push`

Чтобы переслать наш локальный коммит на сервер существует команда, предназначенная для этого - `push`. Она принимает два параметра: имя удаленного репозитория (мы назвали наш origin) и ветку, в которую необходимо внести изменения (master — это ветка по умолчанию для всех репозиториев).
```Bash
$ git push origin master
Counting objects: 3, done.
Writing objects: 100% (3/3), 212 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/tutorialzine/awesome-project.git
* [new branch] master -> master
```
Эта команда немного похожа на `git fetch`, с той лишь разницей, что при помощи fetch мы импортируем коммиты в локальную ветку, а применив push, мы экспортируем их из локальной в удаленную. Если вам необходимо настроить удаленную ветку используйте `git remote`. Однако пушить надо осторожно, ведь рассматриваемая команда перезаписывает безвозвратно все изменения. В большинстве случаев, ее используют, чтобы опубликовать выгружаемые локальные изменения в центральный репозиторий. А еще ее применяют для того, чтобы поделиться, внесенными в локальный репозиторий, нововведениями, с коллегами или другими удаленными участниками разработки проекта. Подытожив сказанное, можно назвать git push - командой выгрузки, а git pull и git fetch - командами загрузки или скачивания. После того как вы успешно запушили измененные данные, их необходимо внедрить или интегрировать, при помощи команды слияния git merge.
В зависимости от сервиса, который вы используете, вам может потребоваться аутентифицироваться, чтобы изменения отправились. Если все сделано правильно, то когда вы посмотрите в удаленный репозиторий при помощи браузера, вы увидите файл hello.txt

*Запрос изменений с сервера*
Если вы сделали изменения в вашем удаленном репозитории, другие пользователи могут скачать изменения при помощи команды pull.
```Bash
$ git pull origin master
From https://github.com/tutorialzine/awesome-project
* branch master -> FETCH_HEAD
Already up-to-date.
```
Так как новых коммитов с тех пор, как мы склонировали себе проект, не было, никаких изменений доступных для скачивания нет.