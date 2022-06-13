# airflow
## Configuring tasks
The 2 ways I have found for injecting configuration values into DAG tasks are 
1. trigger the DAG with a configuration object
2. use Variables
### Trigger the DAG with a configuration object
```
airflow dags trigger --conf '{"conf1": "value1"}' example_parameterized_dag
```
This can also be done using the UI.

In the code:
```
parameterized_task = BashOperator(
    task_id="parameterized_task",
    bash_command="echo value: {{ dag_run.conf['conf1'] }}",
    dag=dag,
)
```
Note: The parameters from dag_run.conf can only be used in a template field of an operator.

### Use Variables
Airflow provides an API which the task writer can use to retrieve a variable value.
The variables can be defined using the Airflow UI.
This is similar to the way that named connections (e.g. to databases) can be created using the UI.
```
from airflow.models import Variable

foo = Variable.get("foo")
```

# docker
## Bring services down and removal all trace of them
```
docker-compose down --volumes --remove-orphans
```
## Get the IP address of a container
```
docker inspect mynginx | grep IPAddress
```
## Stop all containers
```
docker stop $(docker ps -q)
```
## Remove stopped containers
```
docker rm --volumes $(docker ps --filter status=exited -q)
```
Use `--volumes` to remove associated anonymous volumes.

Alternatively
```
docker system prune
```

# git
## Delete a local branch
```
git branch -d name-of-branch
```
## Delete remote branch
```
git push origin --delete new-branch
```
## Diff before commit
if the file has not yet been added...
```
git diff PATH_TO_FILE
```
if the file is already staged
```
git diff --cached PATH_TO_FILE
```
## Push a (new) local branch to the remote
The following command creates a remote branch and creates an association between the local and the remote branch. This means that one can subsequently simply run 'git push' or 'git pull' without having to care about specifying branch)
```
git push -u origin new-branch
```
# ISO dates
1BC is `+0000` and 2BC is `-0001`

# netstat
netstat example on Windows:
```
netstat -aon | find /i ":25"
```

# Poetry
To make a poetry project out of an existing project
```
poetry init
```

# Python
## Run pydoc
```
python -m pydoc -b
```
## [Embedding an interactive shell](https://stackoverflow.com/questions/5597836/embed-create-an-interactive-python-shell-inside-a-python-program)
```
import code
variables = globals().copy()
variables.update(locals())
shell = code.InteractiveConsole(variables)
shell.interact()
```

## reload a module
```
from importlib import reload
reload(math)
```

# tcpdump
## Use -A for ascii output
``` 
tcpdump -A -i any  port 8080
```
## Another example
```
tcpdump -i any -nntX port 80
```
Refer to [Daniel Miessler's tutorial](https://danielmiessler.com/study/tcpdump/).

# tmux
- `Ctrl-B %` for a vertical split (one shell on the left, one shell on the right)
- `Ctrl-B"` for a horizontal split (one shell at the top, one shell at the bottom)
- `Ctrl-B o` to make the **o**ther shell active
- `Ctrl-B ?` for help
- `Ctrl-B d` detach from Tmux, leaving it running in the background (use tmux attach to reenter)
- `Ctrl-B x` to close the current pane
- `Ctrl-B {` to rotate panes

# vi
## apply edit on multiple lines
1. Select the lines: `Ctl-v` to enter selection mode, then the usual keys eg `j` or `G` to select 
a block of lines.
2. Perform the edit eg `I` to insert at the beginning of the line. Note that, at this point, the UI may not show the 
effects of the edit for the whole block.
3. `Esc` when done
## auto-indent off when pasting
```
:set paste
```
and, when done:
```
:set nopaste
```
## copy characters
With the cursor on the first character, `v` then move to select text. `y` to yank.
## turn off highlighting from last search
```
:noh
```
Also, the following might help to stop vim from highlighting every occurrence
of a match after doing a substitution:
```
:set nohlsearch
```
## List colors
```
ls -l /usr/share/vim/vim*/colors
```
To apply:
```
:color elflord
```
## Tabs
```
set tabstop=4 shiftwidth=4 expandtab
```

