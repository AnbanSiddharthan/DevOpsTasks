### 1. Create a directory called ""my_folder"" and navigate into it
```bash
 mkdir my_folder
 cd my_folder
```
### 2. Create a file named ""my_file.txt"" 
```bash
echo "This is my first file." > my_file.txt
```
### 3. Create another file named ""another_file.txt"" 
```bash
echo "This is the second file." > another_file.txt
```
### 4. Concatenate the content of ""another_file.txt"" to ""my_file.txt""
```bash
cat another_file.txt >> my_file.txt
cat my_file.txt
```
### 5. List all files and directories in the current directory
```bash
ls
```
### 6. Create 20 files with .txt extensions
```bash
touch file{1..20}.txt
ls
```
### 7. Rename the first 5 files to .yml
```bash
for i in {1..5}; do mv file$i.txt file$i.yml; done
```
### 8. Print the latest created top 5 files
```bash
ls -lt | head -6
```
### 9. Screenshot Images
<img width="1432" height="626" alt="image" src="https://github.com/user-attachments/assets/92d304b4-8f00-4e01-b277-af573ff6ce39" />
