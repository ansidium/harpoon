# Как писать плагины

## Определение библиотеки

В подкаталоге `/lib` находятся библиотеки, необходимые для работы вашего плагина. Если нужная библиотека уже существует, создавать новую не требуется — переходите к следующему пункту.

Сначала определите класс плагина, который будет принимать объект в качестве аргумента.

Пример:

```python
class Foo(object):
    """Документация по плагину и ссылки"""

    def __init__(self, key):
        self.key = key
        self.base_url = "http://foo.bar/api/v1"

    def _query(self, query):
        return requests.get(self.base_url + query)
```

Далее опишите функции, которые, по возможности, соответствуют командам интерфейса командной строки. Их набор зависит от API, которое вы интегрируете.

Пример:

```python
def burger(self, query):
    """Документация"""
    r = requests.get(self.base_url, query)
    if r.ok:
        print(r.json())
    else:
        print("error")
```

Когда функции готовы, можно приступать к описанию командной строки.

Полный пример кода:

```python
class Foo(object):
    """Документация по плагину и ссылки"""

    def __init__(self, key):
        self.key = key
        self.base_url = "http://foo.bar/api/v1"

    def _query(self, query):
        return requests.get(self.base_url + query)

    def burger(self, query):
        """Документация"""
        r = requests.get(self.base_url, query)
        if r.ok:
            print(r.json())
        else:
            print("error")
```

## Определение команд

В подкаталоге `/commands` располагаются команды, доступные пользователю. Создайте новый файл с названием сервиса, для которого пишете плагин.

* Создайте класс `CommandNAME_OF_YOUR_PLUGIN`, описывающий доступные команды пользователя:

Пример:

```python
from harpoon.commands.base import Command  # обязательно

class CommandFoo(Command):
    """
    # Foo

    * Foo your IoC: `harpoon foo options IoC`
    """

    name = "foo"
    description = "toto"
    config = {"Foo": ["key"]}
```

При необходимости (например, если сервис требует API‑ключ) запросите его у пользователя через параметры конфигурации.

* Опишите команды для вызова через CLI:

```python
def add_arguments(self, parser):
    subparsers = parser.add_subparsers(help="Subcommand")  # обязательно
    parser_a = subparsers.add_parser("burger", help="Use foo with a burger")
    parser_a.add_argument("IoC", help="put your IoC here")
    parser_a.set_defaults(subcommand="burger")

    # ...добавьте другие команды...

    self.parser = parser  # обязательно
```

* Опишите логику работы команды:

```python
def run(self, conf, args, plugins):
    yourPlugin = Foo(conf["Foo"]["key"])
    if "subcommand" in args:
        if args.subcommand == "burger":
            yourPlugin.burger(args.ioc)
        else:
            self.parser.print_help()
    else:
        self.parser.print_help()
```

Для проверки кода пересоберите пакет командой `pip install .`.

Полный пример команды:

```python
from harpoon.commands.base import Command
from harpoon.lib.foo import Foo

class CommandFoo(Command):
    """
    # Foo

    * Foo your IoC: `harpoon foo options IoC`
    """

    name = "foo"
    description = "toto"
    config = {"Foo": ["key"]}

    def add_arguments(self, parser):
        subparsers = parser.add_subparsers(help="Subcommand")
        parser_a = subparsers.add_parser("burger", help="Use foo with a burger")
        parser_a.add_argument("IoC", help="put your IoC here")
        parser_a.set_defaults(subcommand="burger")

        # ...добавьте другие команды...

        self.parser = parser

    def run(self, conf, args, plugins):
        yourPlugin = Foo(conf["Foo"]["key"])
        if "subcommand" in args:
            if args.subcommand == "burger":
                yourPlugin.burger(args.ioc)
            else:
                self.parser.print_help()
        else:
            self.parser.print_help()
```
