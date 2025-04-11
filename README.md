# EazyCLI
## Introduction
EazyCLI is a single file module for console app development.

## Example
1. Create a child class that inherit `CommandLineArguments` and maps command line arguments to its properties:
```
from eazycli import add_argument, CommandLineArguments, CommandRunner

class CLIArguments((CommandLineArguments)):
    '''Bind command line arguments with property.
    '''
    @add_argument('-c', '--configuration-path')
    def configuration_path(self):
        '''Get configuration path from command line.
        '''
```
> For now, you can use value of `-c` or `--configuration-path` by accessing `configuration_path` property of `CLIArguments` instance. Note, all code in definiton of `configuration_path` will be ignored.

2. Create a child class that inherit `CLIArguments`(child class of `CommandLineArguments`) and `CommandRunner` then implement `execute(arg: CLIArguments)` method:
```
class Runner(CommandRunner, CLIArguments):
    '''Implement CommandRunner.
    '''
    def execute(self, command_line_arguments: CLIArguments) -> None:
        '''Implement execute method.

        :param command_line_arguments: a CLIArguments instance
        '''
        print('hello world')
```
> Put business logic in `execute` method. Note that `execute` return `None`.

3. Create `ConsoleApp` instance and bind subcommand with `Runner`. 
```
# main.py
from eazycli import ConsoleApp

if __name__ == '__main__':
    app = ConsoleApp()
    app.add_command('helloworld', Runner)
    app.run()
```

4. Start the app. In our example, simply run `python main.py helloworld -c <config file path>`.
