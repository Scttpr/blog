# Git emergency toolbox

> We always manage to fuck up git history, here are some tapes and tips

## For a better git log

It is always easier to understand or to parse git history with a nice display. Some GUI tools exist but if you prefer CLI like me you can rather :
```bash
# A straightforward one liner
git log --format='%Cred%h%Creset - %C(bold)%s%Creset %C(yellow)%D'

# Pretty two liner with useful informations
git log --format='%Cred%h%Creset - %C(bold green)%<(25,trunc)%ce%Creset %C(green)%cD%Creset%n%C(bold)%s%Creset %C(yellow)%d%Creset%n'

# Raw commit with some coloration
git log --format='%C(red)Commit %C(bold)%H%Creset%nTree %T%nParents %P%n%C(cyan)Author %C(bold)%an <%ae>%Creset %C(cyan)%aD%Creset%n%C(green)Committer %C(bold)%cn <%ce>%Creset %C(green)%cD%Creset%nTitle %C(bold)%s%Creset%C(yellow)%d%n%b%n%N%n'
```

Some people like to add graph vizualisation :
```bash
--graph
```

Or a line separation in between braches :
```bash
--show-linear-break
```

Both at the end of the command !

Then you can add those commands to aliases in `.zshrc` or `.bashrc`

I prefer to make a shell script to create a better UX for me, in terminal :

```bash
command="git log";
command_registered=0;
opts=();

increment_command()
{
  string=$1
  command="${command} ${string}"
  command_registered+=1
}

while [[ "$#" -gt 0 ]]; do
  if [[ $command_registered == 0 ]]; then
    case $1 in

      -s|--short)
        increment_command "--format='%Cred%h%Creset - %C(bold)%s%Creset %C(yellow)%D'"
        ;;
      -l|--long)
        increment_command "--format='%Cred%h%Creset - %C(bold green)%<(25,trunc)%ce%Creset %C(green)%cD%Creset%n%C(bold)%s%Creset %C(yellow)%d%Creset%n'"
        ;;
      -r|--raw)
        increment_command "--format='%C(red)Commit %C(bold)%H%Creset%nTree %T%nParents %P%n%C(cyan)Author %C(bold)%an <%ae>%Creset %C(cyan)%aD%Creset%n%C(green)Committer %C(bold)%cn <%ce>%Creset %C(green)%cD%Creset%nTitle %C(bold)%s%Creset%C(yellow)%d%n%b%n%N%n'"
        ;;
      *)
        opts+=("$1")
    esac
  else
    opts+=("$1")
  fi
  shift
done

len=${#opts[@]};
for (( i=0; i<len; i++ )); do increment_command "${opts[$i]}"; done

eval "$command";
```

Then juste paste the file into one of the $PATH folder and fix rights with `chmod`.
