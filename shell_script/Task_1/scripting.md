### 1. Shell script to print the HTTP error code
```bash
#!/bin/bash

status_code=$(curl -o /dev/null -s -w "%{http_code}" https://guvi.in)

echo "HTTP Status Code: $status_code"

if [[ $status_code -ge 200 && $status_code -lt 300 ]]; then
    echo "Success"
else
    echo "Failure"
fi
```
<img width="827" height="125" alt="image" src="https://github.com/user-attachments/assets/779c4f24-34cd-4114-9c4d-e88f9e3bf852" />

### 2. Replace all occurrence of the word "give" with "learning"
```bash
sed -i '5,$ {/welcome/ s/give/learning/g}' sample.txt
```
<img width="1032" height="487" alt="image" src="https://github.com/user-attachments/assets/3442ab24-5d70-49ad-8666-54c22e342e1c" />
