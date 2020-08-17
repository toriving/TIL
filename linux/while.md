# while loop


```bash
#!/bin/bash

FILE=data_out
while [ ! -d $FILE ]; do
       echo "File $FILE does not exist."
       echo "Sleep 1min"
       sleep 60
done

echo "File $FILE exist."
sleep 60
bash sh/multi_run.sh
```
