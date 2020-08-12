# Bash Cheat Sheet
Bash Cheat Sheet with the most needed stuff..



## variables
```bash
INTRO=./intros/*
CPUCORES=1
```


## cd current directory
```bash
cd "$(dirname "$0")"
pwd
printf "\nCurrent working directory:"
echo "$(dirname "$0")"
printf "\n"
```



<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />

# Loops


## Select files from folder
```bash

SRC=/home/t33n/Downloads/vidz/*

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


## Statements

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
