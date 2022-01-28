# Github: 
* could be "global information tracker" 
* or "goddamn idiotic truckload of shit" (depends on your mood)
---
---
### some bash odes:
* ``` start .``` in windows this will open file explorer on the directory that you are currently in(in mac is ``` code .```)
* ``` ls ``` by its own just shows directory files and folders.
*   ``` ls <folder name> ``` will show the ls of a folder currently exist in ls
*    ``` ls <folder1 name>/<folder2 name>``` and so on
*    ```pwd``` print working directory
*    ```cd ..``` backoff one level
*    ```touch newFile.js hello.txt read.pdf``` creating new file(s) or updating existing file
*    ``` mkdir folder1 folder2 folder3``` can create multiple folders with one mkdir command
*    ``` rm purple.txt yellow.xlsx``` delete file(s) perminantly(shift+delete)
*    ``` rm -rf folder1``` with -rf flag we can delete folders rf stands for recursive force?.(still shift delete)
*    ```cat <file name>``` reads the file in terminal

---
### Git vs Github:
![Screenshot (71)](https://user-images.githubusercontent.com/50621975/149844296-f339a3fe-d476-45bb-8570-0fd8fd4cdb38.png)
---
* ```git log --oneline``` shows every contribute to project with diffrent contributers
* ```git config --list``` shows list of all configurations
* ```git config user.name``` shows  configured username
* ```git config --global user.name "Mohammad"``` config your username (and email accordingly,except that email dont goes in "")
* ```git add file1 file2``` or ```git add .```` to stage your changes

covention is to use present tense for commit messages but its bullshit tbh.

-if you want to write very long commit message,then just write ```git commit``` (without -m flag) and then it will open a new window in default editor in git to eddit your commit message file
* ```git log``` shows history of commits. --oneline flag will summarize commit message
---
## Amending commits:
let say you added and commited some files and suddenly opps .. you realize that u forgot to add 1 file.what you can do is add that forgotten file just like you would have normally and then instead of commit with -m flag you'll write ```git commit --amend``` .this will open the previous commit message's file and you can eddit your message and this file will be added to previous commit(no new commit gets created) 
__note:__ amending commit only works for previous commit.
---
there is a convention that hidden folders(and files?) start with dot?
---
# important note: Git tracks directory and all subdirectories(great great grandchild...)
so dont initialize another git inside an already git subdirectory.its already gettin tracked
---
# in fact each commit is a check point! thats all. or diffrent save through a game so to speak
making commits should be conceptual. for example after adding or deleting an specific feature to your app. you should not commit after every little change in your script

the main benefit of having an staging area separate with commiting is when you made lots of change to your app bu they are for diffrent featurs. for ex: file1 and file2 are created to shape navbar and file3 is eddited to enhance your app logic.you want to first ```add file1 file2``` and commit them with appropriate message and then do the same thing for file3 .so their workflow is separate
---
![image](https://user-images.githubusercontent.com/50621975/150650539-6141af9b-3cd7-42fe-8318-7cd8276c9dc7.png)

---
* there is nothing special about master branch.except its default premade for us.it's deffenitly not mandatory to do some special work in it. in fact you can rename or delete it 
* since 2020 github default branch in named ```main``` but Git remains ```master```
---
![Screenshot (73)](https://user-images.githubusercontent.com/50621975/150650850-202f87ed-82b4-48a9-ad6d-38f7482504d8.png)
Head is the state that your current project is at
---

#Branching:
* ```git branch``` gives us list of all branches in our repo
* ```git branch branch1``` will create a branch1
__note:__ the default master branch is not created untill you commit somthing,hence if you try create a branch in a empty repo(right after initialization) it'll give you an error cause the default branch should be master and its not created yet
---
``` git commit -a -m "commit message"``` is the way to jump the staging area and directly commit changes
---

__note:__ when you commit some changes in a branch and then create a new branch, the Head will point to both branches and the new branch on its first node also has that state(visualize it). 
you can switch to that branch and start commiting new changes on it to seperate its way

---
![Screenshot (74)](https://user-images.githubusercontent.com/50621975/150656126-afb4d90a-38f9-4b03-ae0a-416e6ffab1d5.png)
```checkout``` is not recomended for switching between branches

![Screenshot (75)](https://user-images.githubusercontent.com/50621975/150656389-8ae2cf4e-367a-48de-8a51-743bceb996b8.png)
similar to this there is also ```git checkout -e``` but we dont do that here
----
if you're on a branch and with some uscommited changes in a file, try to switch your branch,you'll get an error saying that either commit your changes or stash
but the story would be diffrent if your uncommited chsnge is new empty file:without any error it'll follow you in your new branch

## Deleting and Renaming branch:
* in order to rename a branch you have to be on that branch(HEAD must point to that branch)
* in order to delete a branch you have to not be in that branch(HEAD must point to some other branch)

```git branch -d <branch name>``` how to delete a branch
however if you try to delete a branch without merged it before,you'll get a error.so you either have to merge it first or use "Force Delete"
force delete is done by using ```D``` instead of ```d``` .

```git branch -m <new name>``` for renaming a branch that you're currently in
