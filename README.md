# Bash Cheat Sheet
Bash Cheat Sheet with the most needed stuff..



<br><br>


# functions

## Passing Arguments
```bash
CD(){
cd "$1"; printf "\nCD() - We will display now the current directory used:"; pwd
}

CD $PATH
```


















<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>

# read file
```bash
cat file | while read line
do
  echo "a line: $line"
done
```






















<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>

# shebang
- Put this on the first line of your script to tell in which way you want to execute the script.
```bash
#!/bin/sh — Execute the file using sh, the Bourne shell, or a compatible shell
#!/bin/csh — Execute the file using csh, the C shell, or a compatible shell
#!/usr/bin/perl -T — Execute using Perl with the option for taint checks
#!/usr/bin/php — Execute the file using the PHP command line interpreter
#!/usr/bin/python -O — Execute using Python with optimizations to code
#!/usr/bin/ruby — Execute using Ruby
#!/bin/ksh
#!/bin/awk
#!/bin/expect
```








































<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>

# delete

## remove files/folder
```bash
git rm -f sample.txt
git rm -rf folder
```


































<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>


# comment

<br><br>

## comment single line
```bash
# any comment here..
```

<br><br>


## comment multiple lines
```bash
: '
lorum ipsum
sample text..
'
```






























<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>


## cd current directory
```bash
cd "$(dirname "$0")"; printf "\nCurrent working directory:"; pwd
```

























<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>


# regex

<br><br>

## use in condition
```bash
#!/bin/bash

# Only continue for 'develop' or 'release/*' branches
BRANCH_REGEX="^(develop$|release//*)"

if [[ $BRANCH =~ $BRANCH_REGEX ]];
then
    echo "BRANCH '$BRANCH' matches BRANCH_REGEX '$BRANCH_REGEX'"
else
    echo "BRANCH '$BRANCH' DOES NOT MATCH BRANCH_REGEX '$BRANCH_REGEX'"
fi
```
<br><br>

## match something and return to variable
```bash
[[ $line =~ \/(.*).git ]]
printf "\n match: ${BASH_REMATCH[0]}";
```































<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>

# Replace

## Replace text and create new variable
```bash
PROJECTNAME=$(echo ${BASH_REMATCH[0]} | sed 's/.git//g')
```




























<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>

## Open script in new window
```bash
# method 1 (you can basicly use any terminal emulator for this)
gnome-terminal -- yourscript.sh
```




































<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>


# variables
```bash
INTRO=./intros/*
CPUCORES=1
```

<br><br>


# concate variables
```bash
tempDIR="$PROJECTNAME-$DATE"
```
<br><br>

  

## create variable of echo
```bash
a=$(echo '111 222 33' | awk '{print $3;}' )
```

<br><br>


## use home path in variable (**$HOME**)
```bash
EXPORT_PATH="$HOME/Documents"
cd "$EXPORT_PATH"
```































<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>

# Iterate

## for loop array
```bash
for i in "${arrayName[@]}"
do
   # do whatever on $i
done
```

<br><br>

## parallel (async) for loop

```bash
test(){
  sample="sample.."
  sample2="$1"
  # and other complex stuff..
}

for d in "${arrayName[@]}"
do
  test $d &
done
wait
```

<br><br>

## Select files from folder
```bash

SRC=/home/username/Downloads/vids/*

for FILE in $SRC
do

        filepath=$FILE
        echo "Current file path: $filepath"

        filename=$(basename -- "$FILE")
        echo "Current FULL file name: $filename"

        extension=${filename##*.}
        echo "Current file extension: $extension"


done
echo "font for loop was done.."
```





<br><br>

## Select files from folder recursive
```bash
#!/bin/sh
PROJECTPATH=~/Projects/gitlab/example

recursiverm() {
  for d in *;
  do
    if [ -d "$d" ]; then
      (cd -- "$d" && recursiverm)
    fi
    echo "Current file path: "; pwd

    filename=$(basename -- "$d")
    echo "Current FULL file name: $filename"

    extension=${filename##*.}
    echo "Current file extension: $extension"
  done
}

(cd $PROJECTPATH; recursiverm)








# method #2
: '
-r or -R is recursive,
-n is line number, and
-w stands for match the whole word.
-l (lower-case L) can be added to just give the file name of matching files.
-e is the pattern used during the search
'

S3REGEX="s3[-]eu[-]central"
MATCHES="$(grep --exclude=\*.{jpg,png} -rnw $PROJECTPATH -e $S3REGEX)"

echo $MATCHES | while read line
do
    echo "Current line: $line"
    #echo "Current file path: "; pwd

    filename=$(basename -- "$1")
    #echo "Current FULL file name: $filename"

    extension=${filename##*.}
    #echo "Current file extension: $extension"

done
```













<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>

# Conditions





<br><br>

## if else
``` bash
# method 1
if [ $introname = "green" ]; then

                   AUDIOSRC=./audio/delay/green/*
                   echo "Current audio source folder: $AUDIOSRC"

elif [ $introname = "blue" ]; then

                   AUDIOSRC=./audio/delay/blue/*
                   echo "Current audio source folder: $AUDIOSRC"

else

                   AUDIOSRC=./audio/delay/red/*
                   echo "Current audio source folder: $AUDIOSRC"

fi

# method 2 - 1 liner if else
[ -d $REPONAME ] && repoExist || repoNotExist;
```

<br><br>

## if else multiple conditions
- You can use either [[ or (( keyword. When you use [[ keyword, you have to use string operators such as -eq, -lt. I think, (( is most preferred for arithmetic, because you can directly use operators such as ==, < and >.
``` bash
# Using [[ operator
a=$1
b=$2
if [[ a -eq 1 || b -eq 2 ]] || [[ a -eq 3 && b -eq 4 ]]
then
     echo "Error"
else
     echo "No Error"
fi


# Using (( operator
a=$1
b=$2
if (( a == 1 || b == 2 )) || (( a == 3 && b == 4 ))
then
     echo "Error"
else
     echo "No Error"
fi
```

<br><br>

## check if value is bla or not
``` bash
phone_missing=false
if [ "$phone_missing" != false ]; then
    echo "phone_missing is not 'false' (but may be non-true, too)"
fi
if [ "$phone_missing" == true ]; then
    echo "phone_missing is true."
fi
```


<br><br>

## check if folder exist (-d)
``` bash
# method 1
if [ -d "$PROJECTNAME" ]
  then printf "\n Repo $PROJECTNAME folder already exist..\n"
  else printf "\n Repo $PROJECTNAME folder does not exist..\n"
fi

# method 2
[ -d $PROJECTNAME/.git ] && rm -rf $PROJECTNAME/.git;
```

<br><br>

## check if file exist (-f)
``` bash
# method 1
if [ -f "sample.txt" ]
  then printf "\n sample.txt already exist..\n"
  else printf "\n sample.txt does not exist..\n"
fi

# method 2
[ -f $PROJECTNAME/.sample.txt ] && rm -f $PROJECTNAME/.sample.txt;
```

<br><br>

## check if folder not exist
``` bash
if [ ! -d "$PROJECTNAME" ]
  then printf "\n Repo $PROJECTNAME folder does not exist..\n"
  else printf "\n Repo $PROJECTNAME folder already exist..\n"
fi
```






























<br><br>
 _____________________________________________________
 _____________________________________________________
<br><br>

# Array


## Create array
```bash
# method 1
declare -a FontColor=()

#method 2
FontColor[0]='yellow'
FontColor[1]='white'
FontColor[2]='green'
FontColor[3]='red'
FontColor[4]='blue'
FontColor[5]='purple'
```


## Push items into array
```bash
    SRC=/home/usernamehere/Downloads/vidz/*
    for INTRO in $SRC
    do

              introAR+=( "$INTRO" )

    done
```


## get random item from array
```bash
rand=$[$RANDOM % ${#introAR[@]}]
intropath=${introAR[$rand]}
introname=$(basename -- "$intropath")
```
