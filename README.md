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

