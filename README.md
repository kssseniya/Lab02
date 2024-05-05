# Lab02
## Part I
01. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).

02. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдущем шаге.

Создаю локальный репозиторий:
```sh
$ mkdir Lab02
$ cd Lab02
$ git init
```

Добавляю удаленный репозиторий:
```sh
$ git remote add origin https://github.com/kssseniya/Lab02.git
```
Синхронизирую с удаленным репозиторием:
```sh
$ git pull origin main
```

``` sh
$ touch README.md
$ git add README.md
$ git commit -m "added README.md"
$ git push origin master
```

03. Создайте файл ```hello_world.cpp``` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку ```using namespace std;```.

``` sh
$ touch hello_world.cpp
```

Файл hello_world.cpp:
```sh
#include <iostream>
using namespace std;
int main()
{
  cout << "Hello world!" << endl;
  return 0;
}
```
``` sh
$ cat >> hello_world.cpp << EOF
```

04. Добавьте этот файл в локальную копию репозитория.
``` sh
$ git add hello_world.cpp
```

05. Закоммитьте изменения с *осмысленным сообщением*.
``` sh
$ git commit -m "added hello_world.cpp"
```

06. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение ```Hello world from @name```, где ```@name``` имя пользователя.

Измененный код:
```sh
#include <iostream>
#include string
using namespace std;
int main() {
  string name;
  cout << "Enter your name"; 
  cin >> name;
  cout << "Hello world from " << name << endl;
  return 0;
}
```

07. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно ```git add```?
``` sh
$ git commit -am "added name"
```

08. Запуште изменения в удалёный репозиторий.
``` sh
$ git push origin master
```

09. Проверьте, что история коммитов доступна в удалёный репозитории.

## Part II
**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания*.

01. В локальной копии репозитория создайте локальную ветку ```patch1```.
```sh
$ git checkout -b patch1
```

02. Внесите изменения в ветке ```patch1``` по исправлению кода и избавления от ```using namespace std;```.

Измененный код:
```sh
#include <iostream>
#include string

int main() {
  string name;
  cout << "Enter your name"; 
  cin >> name;
  cout << "Hello world from " << name << endl;
  return 0;
}
```

03. **commit**, **push** локальную ветку в удалённый репозиторий.
``` sh
$ git commit -am "deleted std"
$ git push -u origin HEAD
```

04. Проверьте, что ветка ```patch1``` доступна в удалёный репозитории.

05. Создайте pull-request ```patch1 -> master```.

06. В локальной копии в ветке ```patch1``` добавьте в исходный код комментарии.
``` sh
Измененный код:
#include <iostream>
#include string
//функция
int main() {
  string name;
  cout << "Enter your name"; 
  cin >> name; //ввод имени
  cout << "Hello world from " << name << endl;
  return 0;
}
```

07. **commit**, **push**.
```sh
$ git commit -am "with comments"
$ git push -u origin HEAD
```

08. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request

09. В удалённый репозитории выполните слияние PR ```patch1 -> master``` и удалите ветку ```patch1``` в удаленном репозитории.

10. Локально выполните **pull**.
``` sh
$ git pull
```

11. С помощью команды **git log** просмотрите историю в локальной версии ветки ```master```.

12. Удалите локальную ветку ```patch1```.
``` sh
$ git checkout master
$ git pull
$ git branch -d patch1
```

## Part III
**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания*.

01. Создайте новую локальную ветку ```patch2```.
``` sh
$ git checkout -b patch2
```

02. Измените *code style* с помощью утилиты clang-format. Например, используя опцию ```-style=Mozilla```.
``` sh
$ sudo apt install clang-format
$ clang-format -i -style=Mozilla hello_world.cpp
```

03. **commit**, **push**, создайте pull-request ```patch2 -> master```.
``` sh
$ git commit -am "changed code style"
$ git push -u origin HEAD
```

04. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.

05. Убедитесь, что в pull-request появились *конфликты*.

06. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
``` sh
$ git pull
$ git rebase master
```

07. Сделайте *force push* в ветку ```patch2```.
``` sh
$ git push origin patch2 --force
```

08. Убедитель, что в pull-request пропали конфликтны.

09. Вмержите pull-request ```patch2 -> master```.
