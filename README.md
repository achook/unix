# Systemy uniksowe

## Zestaw 4

### Zadanie 1
```bash
find -maxdepth 1 -type f -mtime 1
```

### Zadanie 2
```bash
PS1="\w \j\n $"
```

### Zadanie 3
```bash
#!/bin/bash

if [ -z $1 ]
then
        for filename in ./*.JPG
        do
                mv $filename `basename -s .JPG $filename`.jpg
        done
elif [ $1 == "-h" ]
then
        echo "This is help"
else
        cd $1
        for filename in ./*.JPG
        do
                mv $filename `basename -s .JPG $filename`.jpg
        done
fi
```

### Zadanie 4
```bash
#!/bin/bash

for filename in ./*.JPG
do
    mv $filename `basename -s .JPG $filename`.jpg
done
```

### Zadanie 5
```bash
#!/bin/bash

for filename in ~/lab5/*
do
        if [[ -z `file -b 1 $filename | grep JPEG` ]]
        then
                rm $filename
        fi
done
```

### Zadanie 6
```bash
#!/bin/bash

while read f; do
        if [[ `date +%Y-%m-%d` == `echo "$f" | cut -d ' ' -f -1 -` ]]
        then
                echo "$f" | cut -d " " -f 2- -
        fi
done < ~/reminder
```

### Zadanie 7
```bash
#!/bin/bash

LOG_PATH=~/myps.log

trap '' SIGTERM
trap "rm $LOG_PATH && echo 'File $LOG_PATH cleaned' >&2" SIGUSR1

while [ true ]
do
    echo "`date +'%Y-%m-%d %H:%M'`,`ps -e --no-headers | wc -l`,`cut -d " " -f -3 /proc/loadavg | tr " " ,`" >> $LOG_PATH
    sleep 3
done
```