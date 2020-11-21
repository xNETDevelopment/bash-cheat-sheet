# Bash Cheat Sheet
Bash Cheat Sheet with the most needed stuff..



<br><br>


# delete

## remove files
```bash
git rm -f sample.txt
```

## remove folder
```bash
git rmdir -f sample.txt
```


<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />


# comment

## comment out multiple lines
```bash
: '
lorum ipsum
sample text..
'
```

<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />


## cd current directory
```bash
cd "$(dirname "$0")"; printf "\nCurrent working directory:"; pwd
```

<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />


# regex

## match something and return to variable
```bash
[[ $line =~ \/(.*).git ]]
printf "\n match: ${BASH_REMATCH[0]}";
```

<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />

# Replace

## Replace text and create new variable
```bash
PROJECTNAME=$(echo ${BASH_REMATCH[0]} | sed 's/.git//g')
```


<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />

## Open script in new window
```bash
# method 1 (you can basicly use any terminal emulator for this)
gnome-terminal -- yourscript.sh
```



<br />
<br />


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

<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />

# Iterate

## for loop array
```bash
for i in "${arrayName[@]}"
do
   # do whatever on $i
done
```

## parallel (async) for loop
```bash
for i in "${arrayName[@]}"
do
  git commit --allow-empty -a -m "Cron Job Mirror" &&
  git push &
done
wait # wait for all remaining workers
```



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



<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />


# Statements



## if else
``` bash
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
```

## check if folder exist (-d)
``` bash
if [ -d "$PROJECTNAME" ]
  then printf "\n Repo $PROJECTNAME folder already exist..\n"
  else printf "\n Repo $PROJECTNAME folder does not exist..\n"
fi
```

## check if file exist (-f)
``` bash
if [ -f "sample.txt" ]
  then printf "\n sample.txt already exist..\n"
  else printf "\n sample.txt does not exist..\n"
fi
```

## check if folder not exist
``` bash
if [ ! -d "$PROJECTNAME" ]
  then printf "\n Repo $PROJECTNAME folder does not exist..\n"
  else printf "\n Repo $PROJECTNAME folder already exist..\n"
fi
```

<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />

# Array


## Create array
```bash
# method 1
declare -a introAR=()

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
    SRC=/home/t33n/Downloads/vidz/*
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
