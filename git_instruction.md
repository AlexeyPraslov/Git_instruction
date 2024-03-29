<img src="./img/logo.png" width="130" height="50">

# Инструкция для работы с Git

Git - это специальная программа, которая позволяет отслеживать любые изменения в файлах, хранить их версии и оперативно возвращаться в любое сохранённое состояние.

## <span style="color:red">Настройка Git</span>

После установки git, необходимо добавить немного настроек. Есть довольно много опций, с которыми можно играть, но мы настроим самые важные: наше имя пользователя и адрес электронной почты. 
><span style="color:grey">*Откройте терминал и запустите команды:*</span>
>```sh
>$ git config --global user.name "My Name"
>
>$ git config --global user.email myEmail@example.com
>```
><span style="color:grey"> *Теперь каждое наше действие будет отмечено именем и почтой. Таким образом, пользователи всегда будут в курсе, кто отвечает за какие изменения — это вносит порядок.*</span>

## <span style="color:red">Создание нового репозитория</span>

Git хранит свои файлы и историю прямо в папке проекта. Чтобы создать новый репозиторий, нам нужно открыть терминал, зайти в папку нашего проекта и выполнить команду init. Это включит приложение в этой конкретной папке и создаст скрытую директорию .git, где будет храниться история репозитория и настройки.
><span style="color:grey">Создайте на рабочем столе папку под названием git_exercise. Для этого в окне терминала введите:</span>
>```
>$ mkdir Desktop/git_exercise/
>
>$ cd Desktop/git_exercise/
>
>$ git init
>```
><span style="color:grey">Командная строка должна вернуть что-то вроде:</span>
>```
>Initialized empty Git repository in /home/user/Desktop/git_exercise/.git/
>```
><span style="color:grey">Это значит, что наш репозиторий был успешно создан, но пока что пуст.</span>

## <span style="color:red">Определение состояния</span>

status — это еще одна важнейшая команда, которая показывает информацию о текущем состоянии репозитория: актуальна ли информация на нём, нет ли чего-то нового, что поменялось, и так далее. 

><span style="color:grey">*Запуск git status на нашем свежесозданном репозитории должен выдать:*</span>
>```
>$ git status
>On branch master
>Initial commit
>Untracked files:
>(use "git add ..." to include in what will be committed)
>hello.txt
>```
><span style="color:grey">*Сообщение говорит о том, что файл hello.txt неотслеживаемый. Это значит, что файл новый и система еще не знает, нужно ли следить за изменениями в файле или его можно просто игнорировать. Для того, чтобы начать отслеживать новый файл, нужно его специальным образом объявить.*</span>

## <span style="color:red">Подготовка файлов</span>

В git есть концепция области подготовленных файлов. Можно представить ее как холст, на который наносят изменения, которые нужны в коммите. Сперва он пустой, но затем мы добавляем на него файлы (или части файлов, или даже одиночные строчки) командой add и, наконец, коммитим все нужное в репозиторий (создаем слепок нужного нам состояния) командой commit.

><span style="color:grey"> *В нашем случае у нас только один файл, так что добавим его:*</span>
>
>```
>$ git add hello.txt 
>```
><span style="color:grey">*Проверим статус снова, на этот раз мы должны получить другой ответ:*</span>
>
>```
>$ git status
>
>On branch master
>Initial commit
>Changes to be committed:
>(use "git rm --cached ..." to unstage)
>new file: hello.txt


Файл готов к коммиту. Сообщение о состоянии также говорит нам о том, какие изменения относительно файла были проведены в области подготовки — в данном случае это новый файл, но файлы могут быть модифицированы или удалены.

## <span style="color:red">Фиксация изменений</span>
### <span style="color:red">Как сделать коммит</span>

Представим, что нам нужно добавить пару новых блоков в html-разметку (index.html) и стилизовать их в файле style.css. Для сохранения изменений, их необходимо закоммитить. Но сначала, мы должны обозначить эти файлы для Гита, при помощи команды git add, добавляющей (или подготавливающей) их к коммиту.

><span style="color:grey">*Добавлять их можно по отдельности:*</span>
>```
>$ git add index.html
>
>$ git add css/style.css
>```
><span style="color:grey">*или вместе - всё сразу:*</span>
>```
>$ git add --all
>```

><span style="color:grey">Теперь создадим непосредственно сам коммит</span>
>```
>$ git commit -m 'Add some code'
>```
Флажок -m задаст commit message - комментарий разработчика. Он необходим для описания закоммиченных изменений. И здесь работает золотое правило всех комментариев в коде: «Максимально ясно, просто и содержательно обозначь написанное!»

### <span style="color:red">Как посмотреть коммиты</span>

Для просмотра все выполненных фиксаций можно воспользоваться историей коммитов. Она содержит сведения о каждом проведенном коммите проекта.

><span style="color:grey">*Запросить ее можно при помощи команды:*</span>
>```
>$ git log
>```

В ней содержится вся информация о каждом отдельном коммите, с указанием его хэша, автора, списка изменений и даты, когда они были сделаны.

><span style="color:grey">*Отследить интересующие вас операции в списке изменений, можно по хэшу коммита, при помощи команды git show:*</span>
>```
>$ git show hash_commit
>```

><span style="color:grey">*Ну а если вдруг нам нужно переделать commit message и внести туда новый комментарий, можно написать следующую конструкцию:*</span>
>```
>$ git commit --amend -m 'Новый комментарий'
>```
><span style="color:grey">*В данном случае сообщение последнего коммита перезапишется. Но злоупотреблять этим не стоит, поскольку эта операция опасная и лучше ее делать до отправки коммита на сервер.*</span>

### <span style="color:red">Удаленные репозитории</span>

Репозиторий, хранящийся в облаке, на стороннем сервисе, специально созданном для работы с git имеет ряд преимуществ. Во-первых - это своего рода резервная копия вашего проекта, предоставляющая возможность безболезненной работы в команде. А еще в таком репозитории можно пользоваться дополнительными возможностями хостинга. К примеру -визуализацией истории или возможностью разрабатывать вашу программу непосредственно в веб-интерфейсе.

### <span style="color:red">Клонирование</span>

Клонирование - это когда вы копируете удаленный репозиторий к себе на локальный ПК. Это то, с чего обычно начинается любой проект. При этом вы переносите себе все файлы и папки проекта, а также всю его историю с момента его создания. Чтобы склонировать проект, сперва, необходимо узнать где он расположен и скопировать ссылку на него. В нашем руководстве мы будем использовать адрес https://github.com/tutorialzine/awesome-project, но вам посоветуем, попробовать создать свой репозиторий в GitHub, BitBucket или любом другом сервисе:

>```
>$ git clone https://github.com/tutorialzine/awesome-project
>```

При клонировании в текущий каталог, там будет создана папка, в которую поместятся все проектные файлы и скрытая директория .git, с самим репозиторием, или с необходимой информацией о нем. В такой ситуации, для клонируемого репозитория, по умолчанию, будет создана папка с одноименным названием, но его можно залить и в другую директорию, например:

>```
>$ git clone https://github.com/tutorialzine/awesome-project new-folder
>```

### <span style="color:red">Подключение к удаленному репозиторию</span>

Чтобы загрузить что-нибудь в удаленный репозиторий, сначала нужно к нему подключиться. Регистрация и установка может занять время, но все подобные сервисы предоставляют хорошую документацию.

><span style="color:grey">*Чтобы связать наш локальный репозиторий с репозиторием на GitHub, выполним следующую команду в терминале. Обратите внимание, что нужно обязательно изменить URI репозитория на свой.*</span>
>```
>This is only an example. Replace the URI with your own repository address.
>
>git remote add origin https://github.com/tutorialzine/awesome-project.git
>```

Проект может иметь несколько удаленных репозиториев одновременно. Чтобы их различать, мы дадим им разные имена. Обычно главный репозиторий называется origin.

### <span style="color:red">Отправка изменений на сервер</span>

Сейчас самое время переслать наш локальный коммит на сервер. Этот процесс происходит каждый раз, когда мы хотим обновить данные в удаленном репозитории.
Команда, предназначенная для этого - push. Она принимает два параметра: имя удаленного репозитория (мы назвали наш origin) и ветку, в которую необходимо внести изменения (master — это ветка по умолчанию для всех репозиториев).

>```
>$ git push origin master
>
>Counting objects: 3, done.
>Writing objects: 100% (3/3), 212 bytes | 0 bytes/s, done.
>Total 3 (delta 0), reused 0 (delta 0)
>To https://github.com/tutorialzine/awesome-project.git
>[new branch] master -> master
>```

 Если все сделано правильно, то когда вы посмотрите в удаленный репозиторий при помощи браузера, вы увидите файл hello.txt

 ### <span style="color:red">Запрос изменений с сервера</span>

 Если вы сделали изменения в вашем удаленном репозитории, другие пользователи могут скачать изменения при помощи команды pull.

>```
>$ git pull origin master
>
>From https://github.com/tutorialzine/awesome-project
>* branch master -> FETCH_HEAD
>Already up-to-date.

Так как новых коммитов с тех пор, как мы склонировали себе проект, не было, никаких изменений доступных для скачивания нет.

### <span style="color:red">Как удалить локальный репозиторий</span>

Вам не понравился один из ваших локальных Git-репозиториев и вы хотите стереть его со своей машины. Для этого вам всего лишь надо удалить скрытую папку «.git» в корневом каталоге репозитория. Сделать это можно 3 способами:

1. Проще всего вручную удалить эту папку «.git» в корневом каталоге «Git Local Warehouse».

2. Также удалить, не устраивающий вас, репозиторий можно на github. Открываете нужный вам объект и переходите в пункт меню Настройки. Там, прокрутив ползунок вниз, вы попадете в зону опасности, где один из пунктов будет называться «удаление этого хранилища».

3. Последний метод удаления локального хранилища через командную строку, для этого в терминале необходимо ввести следующую команду:
>```
>$ cd repository-path
>
>$ rm -r .git
>```

## <span style="color:red">Ветвление</span>

Во время разработки новой функциональности считается хорошей практикой работать с копией оригинального проекта, которую называют веткой. Ветви имеют свою собственную историю и изолированные друг от друга изменения до тех пор, пока вы не решаете слить изменения вместе. Это происходит по набору причин:

* Уже рабочая, стабильная версия кода сохраняется.
* Различные новые функции могут разрабатываться параллельно разными программистами.
* Разработчики могут работать с собственными ветками без риска, что кодовая база поменяется из-за чужих изменений.
* В случае сомнений, различные реализации одной и той же идеи могут быть разработаны в разных ветках и затем сравниваться.

### <span style="color:red">Создание новой ветки</span>

><span style="color:grey">*Основная ветка в каждом репозитории называется master. Чтобы создать еще одну ветку, используем команду branch_(name)*</span>
>```
>$ git branch amazing_new_feature
>```
><span style="color:grey">*Это создаст новую ветку, пока что точную копию ветки master.*</span>

### <span style="color:red">Переключение между ветками</span>

><span style="color:grey">*Сейчас, если мы запустим branch, мы увидим две доступные опции:*</span>
>```
>$ git branch
>
>amazing_new_feature<br>
>* master
>```
><span style="color:grey">*master — это активная ветка, она помечена звездочкой.*</span>

><span style="color:grey">*Чтобы переключиться на другую ветку, воспользуемся командой checkout, она принимает один параметр — имя ветки, на которую необходимо переключиться.*</span>
>```
>$ git checkout amazing_new_feature
>```

В Git ветка — это отдельная линия разработки. Git checkout позволяет нам переключаться как между удаленными, так и между локальными ветками. Это один из способов получить доступ к работе коллеги или соавтора, обеспечивающий более высокую продуктивность совместной работы. Однако тут надо помнить, что пока вы не закомитили изменения, вы не сможете переключиться на другую ветку.

### <span style="color:red">Слияние веток</span>

 ><span style="color:grey">*Cоздадим файл feature.txt, добавим и закоммитим:*</span>
 >```
 >$ git add feature.txt
 >$ git commit -m "New feature complete.”
 >```

><span style="color:grey">*Изменения завершены, теперь мы можем переключиться обратно на ветку master.*</span>
>```
>$ git checkout master
>```

><span style="color:grey">*Теперь, если мы откроем наш проект в файловом менеджере, мы не увидим файла feature.txt, потому что мы переключились обратно на ветку master, в которой такого файла не существует. Чтобы он появился, нужно воспользоваться merge для объединения веток (применения изменений из ветки amazing_new_feature к основной версии проекта).*</span>
>```
>$ git merge amazing_new_feature
>```

><span style="color:grey">*Теперь ветка master актуальна. Ветка amazing_new_feature больше не нужна, и ее можно удалить.*</span>
>```
>$ git branch -d awesome_new_feature
>```

## <span style="color:red">Как удалять ветки в Git?</span>

Бывают ситуации, когда после слива каких-то изменений из рабочей ветки в исходную версию проекта, ее, по правилам хорошего тона, необходимо удалить, чтобы она более не мешалась в вашем коде. Но как это сделать?

><span style="color:grey">*Для локально расположенных веток существует команда:*</span>
>```
>$ git branch -d local_branch_name
>```
><span style="color:grey">*Где флажок -d являющийся опцией команды git branch - это сокращенная версия ключевого слова --delete, предназначенного для удаления ветки, а local_branch_name – название ненужной нам ветки.
Однако тут есть нюанс: удалить текущую ветку, в которую вы, в данный момент просматриваете - нельзя. Если же вы все-таки попытаетесь это сделать, система отругает вас и выдаст ошибку с таким содержанием:*</span>
>```
>Error: Cannot delete branch local_branch_name checked out at название_директории
>```
><span style="color:grey">*Так что при удалении ветвей, обязательно переключитесь на другой branch.*</span>

## <span style="color:red">Дополнительно</span>

### <span style="color:red">Отслеживание изменений, сделанных в коммитах</span>

><span style="color:grey">*У каждого коммита есть свой уникальный идентификатор в виде строки цифр и букв. Чтобы просмотреть список всех коммитов и их идентификаторов, можно использовать команду git log:*</span>
>```
>$ git log
>commit ba25c0ff30e1b2f0259157b42b9f8f5d174d80d7
>Author: Tutorialzine
>Date: Mon May 30 17:15:28 2016 +0300
>New feature complete
>commit b10cc1238e355c02a044ef9f9860811ff605c9b4
>Author: Tutorialzine
>Date: Mon May 30 16:30:04 2016 +0300
>Added content to hello.txt
>commit 09bd8cc171d7084e78e4d118a2346b7487dca059
>Author: Tutorialzine
>Date: Sat May 28 17:52:14 2016 +0300
>Initial commit
>```

><span style="color:grey">*Как вы можете заметить, идентификаторы довольно длинные, но для работы с ними не обязательно копировать их целиком — первых нескольких символов будет вполне достаточно. Чтобы посмотреть, что нового появилось в коммите, мы можем воспользоваться командой show [commit]*</span>
>```
>$ git show b10cc123
>commit b10cc1238e355c02a044ef9f9860811ff605c9b4
>Author: Tutorialzine
>Date: Mon May 30 16:30:04 2016 +0300
>Added content to hello.txt
>diff --git a/hello.txt b/hello.txt
>index e69de29..b546a21 100644
>--- a/hello.txt
>+++ b/hello.txt
>@@ -0,0 +1 @@
>+Nice weather today, isn't it?
>```

><span style="color:grey">*Чтобы увидеть разницу между двумя коммитами, используется команда diff (с указанием промежутка между коммитами):*</span>
>```
>$ git diff 09bd8cc..ba25c0ff
>diff --git a/feature.txt b/feature.txt
>new file mode 100644
>index 0000000..e69de29
>diff --git a/hello.txt b/hello.txt
>index e69de29..b546a21 100644
>--- a/hello.txt
>+++ b/hello.txt
>@@ -0,0 +1 @@
>+Nice weather today, isn't it?
>```
><span style="color:grey">*Мы сравнили первый коммит с последним, чтобы увидеть все изменения, которые были когда-либо сделаны. Обычно проще использовать git difftool, так как эта команда запускает графический клиент, в котором наглядно сопоставляет все изменения.*</span>

### <span style="color:red">Возвращение файла к предыдущему состоянию</span>

Гит позволяет вернуть выбранный файл к состоянию на момент определенного коммита. Это делается уже знакомой нам командой checkout, которую мы ранее использовали для переключения между ветками. Но она также может быть использована для переключения между коммитами (это довольно распространенная ситуация для Гита - использование одной команды для различных, на первый взгляд, слабо связанных задач).

><span style="color:grey">*В следующем примере мы возьмем файл hello.txt и откатим все изменения, совершенные над ним к первому коммиту. Чтобы сделать это, мы подставим в команду идентификатор нужного коммита, а также путь до файла:*</span>
>```
>$ git checkout 09bd8cc1 hello.txt
>```

### <span style="color:red">Разрешение конфликтов при слиянии</span>

Помимо сценария, описанного в предыдущем пункте, конфликты регулярно возникают при слиянии ветвей или при отправке чужого кода. Иногда конфликты исправляются автоматически, но обычно с этим приходится разбираться вручную — решать, какой код остается, а какой нужно удалить.

><span style="color:grey">*Давайте посмотрим на примеры, где мы попытаемся слить две ветки под названием john_branch и tim_branch. Где мы правим один и тот же файл в разных ветках. Теперь при попытки слить эти ветки, мы получаем код об ошибке:*</span> 
>```
>$ git merge tim_branch
>Auto-merging print_array.js
>CONFLICT (content): Merge conflict in print_array.js
>Automatic merge failed; fix conflicts and then commit the result.
>```
><span style="color:grey">*Система не смогла разрешить конфликт автоматически, значит, это придется сделать разработчикам. Приложение отметило строки, содержащие конфликт:*</span> 
>```
>><<<<<<< HEAD // Use a for loop to console.log contents. for(var i=0; i<arr.>length; i++) { console.log(arr[i]); } ======= // Use forEach to console.log >contents. arr.forEach(function(item) { console.log(item); }); >>>>>>> Tim's >commit.
>```
><span style="color:grey">*Над разделителем ======= мы видим последний (HEAD) коммит, а под ним - конфликтующий. Таким образом, мы можем увидеть, чем они отличаются и решать, какая версия лучше. Или вовсе написать новую. В этой ситуации мы так и поступим, перепишем все, удалив разделители, и дадим git понять, что закончили.*</span> 
>

><span style="color:grey">*Когда все готово, нужно закоммитить изменения, чтобы закончить процесс:*</span>
>```
>$ git add -A
>
>$ git commit -m "Array printing conflict resolved."
>```

## <span style="color:red">Настройка .gitignore</span>

В большинстве проектов есть файлы или целые директории, в которые мы не хотим (и, скорее всего, не захотим) коммитить. Мы можем удостовериться, что они случайно не попадут в git add -A при помощи файла .gitignore

* Создайте вручную файл под названием .gitignore и сохраните его в директорию проекта.
* Внутри файла перечислите названия файлов/папок, которые нужно игнорировать, каждый с новой строки.
* Файл .gitignore должен быть добавлен, закоммичен и отправлен на сервер, как любой другой файл в проекте.