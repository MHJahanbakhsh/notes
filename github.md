# Github: 
* could be "global information tracker" 
* or "goddamn idiotic truckload of shit" (depends on your mood)
---
---
### some bash codes:
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

# Branching:
* ```git branch``` gives us list of all branches in our repo
* ```git branch -v``` similar to command above but gives little more info about each branch such as tip of hashcode and commit message
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

---
# Merging branches(oh boy!):
## overall we have 3 types of scenarios when it comes to merging:
* fast forward merges
* new merge commit(without conflict) 
* new merge commit(with conflict)

## 1-Fast Forward Merge:
this is the easiest merge. let say from the master branch you created a new branch called "bugfix" and made some commit in it.meanwhile master branch remained intact(no one commited any change into it).the situation is like this:
![Screenshot (77)](https://user-images.githubusercontent.com/50621975/151988464-d5e8b581-f2ed-413f-9662-87ecb6d85594.png)
what we gonna do is making master branch to catch up.and we do that by first going to master branch and then ```git merge bugfix``` .and what happens is picture below:
![Screenshot (78)](https://user-images.githubusercontent.com/50621975/151996209-e8af5db0-18e3-4437-9ace-d9b99823b91d.png)
you literally get the message says :"Fast Forward Merge"

## 2-New Merge Commit:
this type of merge happens when master branch is not remaining intact while working on other branches; but still there is no conflict among the files.
example of a conflict is :line 59 of the "hey.txt" in master branch is diffrent from "hey.txt" in bugfix branch
![Screenshot (82)](https://user-images.githubusercontent.com/50621975/152005706-8d14654e-f275-4815-b2cb-4c9e0a0b83e4.png)
in this case if we merge; git creates a new commit for us with 2 parents(beforehand we only have seen commits that we make them by ourselfs and there was only one parent for each commit)
a better example for this kind of merge is when you make a new file in the master branch and do some commits on it. this file has nothing to do with the one which editted in bugfix branch,hence there is no conflict)
__the workflow in this merge is exactly the same(switching to rspected branch and write ```git merge <branch name>```) . the only diffrence is what happens next:
a window will open to write your commit message
![Screenshot (84)](https://user-images.githubusercontent.com/50621975/152015235-394ae20a-8686-4785-8931-e23b5076604b.png)

## 2-Merge With Conflicts:
so essentially there is no magic involved. we have to manually resolve it
if we repeat the same process, we'll get the message below:
![Screenshot (85)](https://user-images.githubusercontent.com/50621975/152016382-8ac1c8a4-4bed-41d8-9450-67e170d2aab4.png)
so a commonplace scenario for this ,is when two branchs make diffrent changes in one file.
so after recieving message above,a new window opens in your default text edditor with some file like this:
![Screenshot (86)](https://user-images.githubusercontent.com/50621975/152023800-54ebd0a5-13d5-4234-82d5-f957ffdd1307.png)
at this point you have to make your choice upon how you are going to merge them.finally you have to delete all the " ==<<>>>" markers and deliver a legit file.
for example we can keep both changes(in coding is not always possible.here is just text file) 
```i have 2 cats
i have a chicken
i used to have a dog :(
```
and save this shit.
after this, a new file(s) gets created and when you type ```git status``` you see valla!! actually merge is done just not staged yet.and depends on the way you treated conflicts you see the messages:both files modified or 1 file modified or ...
now you have to commit your changes to finish the merge



