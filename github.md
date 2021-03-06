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
*    tilda (`~`) represents users directory. for example to see ssh keys already exists or not: `ls -a -l ~.ssh`

---
### Git vs Github:
![Screenshot (71)](https://user-images.githubusercontent.com/50621975/149844296-f339a3fe-d476-45bb-8570-0fd8fd4cdb38.png)
---
* ```git log --oneline``` shows every contribute to project with diffrent contributers
* ```git config --list``` shows list of all configurations
* ```git config user.name``` shows  configured username
* ```git config --global user.name "Mohammad"``` config your username (and email accordingly,except that email dont goes in "")
* ```git add file1 file2``` or `git add .` to stage your changes

covention is to use present tense for commit messages.

-if you want to write very long commit message,then just write ```git commit``` (without -m flag) and then it will open a new window in default editor in git to eddit your commit message file
* ```git log``` shows history of commits. --oneline flag will summarize commit message
---
## Amending commits:
let say you added and commited some files and suddenly opps .. you realize that u forgot to add 1 file.what you can do is add that forgotten file just like you would have normally and then instead of commit with -m flag you'll write ```git commit --amend``` .this will open the previous commit message's file and you can eddit your message and this file will be added to previous commit(no new commit gets created) 
```bash
git commit -m 'some commit'
git add forgotten_file
git commit --amend 
```

__note:__ amending commit only works for previous commit.

---
there is a convention that hidden folders(and files?) start with dot?    

---
#### important note: Git tracks directory and all subdirectories(great great grandchild...) ;so dont initialize another git inside an already git subdirectory.its already gettin tracked

---
# in fact each commit is a check point! thats all. or diffrent save through a game so to speak
making commits should be conceptual. for example after adding or deleting an specific feature to your app. you should not commit after every little change in your script

the main benefit of having an staging area separate with commiting is when you made lots of change to your app but they are for diffrent featurs. for ex: file1 and file2 are created to shape navbar and file3 is eddited to enhance your app logic.you want to first ```add file1 file2``` and commit them with appropriate message and then do the same thing for file3 .so their workflow is separate

---
![image](https://user-images.githubusercontent.com/50621975/150650539-6141af9b-3cd7-42fe-8318-7cd8276c9dc7.png)

---
* there is nothing special about master branch.except its default premade for us.it's definitely not mandatory to do some special work in it. in fact you can rename or delete it 
* since 2020 github default branch in named ```main``` but Git remains ```master```
---
![Screenshot (73)](https://user-images.githubusercontent.com/50621975/150650850-202f87ed-82b4-48a9-ad6d-38f7482504d8.png)
Head is the state that your current project is at

---

# Branching:
* ```git branch``` gives us list of all branches in our repo
* ```git branch -v``` similar to command above but gives little more info about each branch such as tip of hashcode and commit message
* ```git branch branch1``` will create a branch1
* ``` git branch -M <new name>``` will rename the branch that you're currently in
__note:__ the default master branch is not created untill you commit somthing,hence if you try create a branch in a empty repo(right after initialization) it'll give you an error cause the default branch should be master and its not created yet
---
``` git commit -a -m "commit message"``` is the way to jump the staging area and directly commit changes. can not done for initial commit

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
```
i have 2 cats
i have a chicken
i used to have a dog :(
```
and save this shit.
after this, a new file(s) gets created and when you type ```git status``` you see valla!! actually merge is done just not staged yet.and depends on the way you treated conflicts you see the messages:both files modified or 1 file modified or ...
now you have to commit your changes to finish the merge

### important note about conflicts:
even if in one branhc the files is empty and in the other branch the respected file is not;they have conflicts! becuase in the same lines one branch is empty and the other is written some shit and this merge wont happen without first resolving it. when two files content appended to each other, was for when in a file a in branch "A" we have:
```
hello
you
wassap
```
and in branch "B":
```
hello
you 
wassap
some
other 
shits
...
```
as u can see first 3 lines is intact in file2
---
## Git Diff:
* ```git diff``` shows changes between working direcory(already commited) and current situation(not added to staging area yet).if you add changes to staging area, "git diff" shows nothing
* ```git diff HEAD``` show changes between working directory(already commited) and not yet commited(either it's staged or not). in other words:__```git diff HEAD``` will show all changes to tracked files.__
* ```git diff --staged or --cached``` will only show changes to files in the "staged" area.If you have all changes staged for commit, then both commands(```git diff HEAD``` and ```git diff --staged```) will output the same
* __note:__ if you make a new file and dont add it to staging area, ```git diff``` shows nothing!
* we can add a specific file to the commands above to narrow down our search for example:```git diff script.js``` or ```git diff HEAD main.css```
* ```git diff branch1..branch2``` comparing 2 branches(obviuosly only shows diffrences that are commited)
* ```git diff commit1..commit2``` similarly we can compare two commits;where commit1 & commit2 are shortened hashes you see on ```git log --oneline```
  * we can use "HEAD" if one of the branches we want to compare is on the HEAD

---

# Stashing:
stashing is like saving to temporary memory.for example: you are on branch x and working on somthing but not ready to commit;meanwhile you somthing happens and you have to go to branch y. you can add files to staging area and then type: ``` git stash``` or ``` git stash save``` and you'll see your files are not in staging area anymore,they are in the so called *stash* .now you can switch to desired branch and har gohi khasi bokhori and then come back to this branch and continuing your work by typing ``` git stash pop```;this command remove changes in *stash* and puts them back to staging area in branch x

note:it's not like always you have to choose over between commiting and stashing befor switching: if your changes are not conflicting to the other branche which you are moving,then your changes would come with you;however thats not optimal most of the times.

note:if your changes are confliciting and  you recieve ``` error: Your local changes to the following files would be overwritten by checkout:
        index.html
Please commit your changes or stash them before you switch branches.
Aborting ``` it does not matter if your changes are in staging area or working directory

__note:__ %95 of times we use just these two commands: ```git stash``` and ```git stash pop``` . but its good to know the rest

``` git stash apply``` is like``` git stash pop```,except it wont empty the stash and you can re apply changes somewhere else.

__we can have multiple stashes,stacking all over each other.when ```git stash pop``` git applies most recent stash first.__
we can see the list of multiple stashes by writing: ``` git stash list```
![Screenshot (87)](https://user-images.githubusercontent.com/50621975/152797452-0f73d4be-b90f-48c9-b681-36b7f0a311dc.png)

how to apply specific stash from a list:
![Screenshot (88)](https://user-images.githubusercontent.com/50621975/152797564-bcc99268-b809-4ab9-9043-0977cc143214.png)

### removing specific stash or the entire list:
![Screenshot (90)](https://user-images.githubusercontent.com/50621975/152819406-7f6cce38-2cae-4066-9faa-bc657ed5f9e0.png)
![Screenshot (91)](https://user-images.githubusercontent.com/50621975/152819431-94fa3b40-a22e-4583-9b75-7767809285a9.png)

---

# time traveling & git checkout:
so as u already know ``` git checkout``` is capable of all kinds of shit.that's why ``` git switch``` and ``` git restore``` are designed to reduce the load of it.
we can write ``` git checkout <some commit hash>``` to travel to specific commit.we can can use full hash or atleast first 7 digits of the hash(retrieved from ``` git log --oneline```.
by doing this we enter in "daetached HEAD" mode .in this mode HEAD is pointing to specific commit instead of the branch(when pointing to a branch , is pointing to the last commit of that branch).3 things can happen after entering deatached mode:
![Screenshot (92)](https://user-images.githubusercontent.com/50621975/152849637-1b999d09-dc55-4ded-ac43-1e0126374350.png)
![Screenshot (93)](https://user-images.githubusercontent.com/50621975/152850593-3ae01f9d-8deb-4056-84c7-356466c98e1a.png)
![Screenshot (94)](https://user-images.githubusercontent.com/50621975/152850618-5d4c4867-036c-44bf-9ad3-2a1b9304ee4e.png)
![Screenshot (96)](https://user-images.githubusercontent.com/50621975/152850635-52886899-aca8-4198-8595-cae7a0c559a1.png)

while in deatached HEAD mode you can type ```git switch -``` to go to the last commit of that branch(essentially back to attached HEAD mode). ``` git switch <branch name>``` also works

# undoing changes & git checkout:
let say you've made some changes and instead of ctrl+z you want to revert changes in giti way!(either added to stagig area or nah):
``` git checkout HEAD <filename(s)>``` or ``` git checkout -- <filename(s)>``` is the way to do it. the working directory becomes how last commit was
__note: important thing to know about undoing changes is :when we undo our changes and go to prior state; we actually stay do not time travel and HEAD stays on where it already is. this is important to know cuase next command ``` git restore``` can restore your current state to a specific commit__

``` git restore <filename>``` does exactly what ``` git checkout HEAD <filename(s)>``` and ```git checkout -- <filename(s)>``` do.(but better)
as we already discussed we can use git restore to restore to specific commit:  ```git restore --source HEAD~n <filename>``` . default source is HEAD,we changed it here to HEAD~1 or HEAD~2 or ...

## unstaging files with git restore:
![Screenshot (97)](https://user-images.githubusercontent.com/50621975/152859899-600eeea7-f44f-4467-9acd-68771cfb516b.png)

## git reset:
git reset will delete latest repository or repositories you've made and take you back to the hash you provided for it.

let say you have a repository like this:![Screenshot (98)](https://user-images.githubusercontent.com/50621975/152934073-ec6e96b3-913a-44cc-9799-ba46a62c360c.png)  
if you type ``` git reset bea1bf6``` or ```git reset HEAD~2``` you'll get:![Screenshot (99)](https://user-images.githubusercontent.com/50621975/152934826-216c7e40-425e-4958-8558-9f5276537437.png). as u see all commits after that hash are gone  
__BUT__ the thing is ,the last state of repo in "mistaken comes with you as unstaged changes. if you add ``--hard`` flag to those code this wont happen and you shall have a hard reset 

## Git Revert:
![Screenshot (100)](https://user-images.githubusercontent.com/50621975/152936090-336029ce-86a2-4c46-b257-731629bd93f9.png)
![image](https://user-images.githubusercontent.com/50621975/152936187-3fd5bce7-f822-4d6d-96b2-eac0967507b4.png)
![Screenshot (102)](https://user-images.githubusercontent.com/50621975/152936332-ecf71aec-db69-4538-8946-6899590ec232.png)

---
---
# Github:
![Screenshot (103)](https://user-images.githubusercontent.com/50621975/153028875-f1ae124b-9179-482e-b07a-19b18c484036.png)
url in gitclone does not necceserily have to be from github.it could be gitlab,bitbucket,.. basically any url that provides a git repo

__SSH = secure shell,it is a communication protocal just like http,https,ftp,... and it's encrypted.used mostly in terminal/command line__

## Remote:
ok so basically if we want to push our local code to github,there are two ways:
* create empty repo in github and define that repo in our local machine as a "remote"
   * if we have an already created local repo and worked on it, this is optimal solution
* or create empty repo in github and clone that to our machine.by cloning remoting process is already done behind the scene. 
   * if we are starting fresh , this could be little bit easier  

__wait wth is remote?__
![Screenshot (105)](https://user-images.githubusercontent.com/50621975/153225039-801dfd1b-2617-417b-8efe-e7b7943ae570.png)
and __origin__ is a conventional name that we pick for our remote
remotes are repository related.each repo can have multiple remotes.

before add any remote it's better to check if there is already any:![Screenshot (107)](https://user-images.githubusercontent.com/50621975/153226174-c213fbd5-5b29-4c99-b4b5-075199302151.png)
![Screenshot (108)](https://user-images.githubusercontent.com/50621975/153226351-b7ac5569-dc4d-4232-84cf-f5402f8ea2bf.png)
![Screenshot (109)](https://user-images.githubusercontent.com/50621975/153226373-6c7179ac-8243-4f8f-8d54-647ced2feb03.png)
![Screenshot (110)](https://user-images.githubusercontent.com/50621975/153226425-cb726811-7bb1-4171-8609-72a3d21646b5.png)
![Screenshot (111)](https://user-images.githubusercontent.com/50621975/153226440-2ff1c204-c0c3-4c7a-b94b-c8acdc507732.png)
by setting up a remote you just tell git the place of this particular local repo on cloud.
for connecting your work you have to push them
![Screenshot (112)](https://user-images.githubusercontent.com/50621975/153227979-7c030ce4-4d03-4940-ba0c-6e849123ec45.png)

not so commonly used commands for renaming and removing remotes:
``` git remote remove <remote name>```
``` git remote rename <old name> <new name>```

## push:
* we can push each branch at a time with ``` git push <remote repo name> <local repo name>``` (remote name is usually origin) ex:``` git push origin master```  
* or we can push whole repo at once: ```git push --all```

what is ```-u``` flag in push?
it is used to set "upstream" for a branch .which in next pushes we only have to type ```git push```:  
``` git push -u origin branch2``` ===> now while we are inside that branch we only have to type ```git push``` and vahlla ! does the same.
alternativly we can write ``` git push --set-upstream origin branch2```
![Screenshot (114)](https://user-images.githubusercontent.com/50621975/153236832-e3fd9c36-3f58-436a-81bd-65733698aaf4.png)  



---
# Fetching & Pulling:
![Screenshot (115)](https://user-images.githubusercontent.com/50621975/153236700-fc0917f9-f793-4368-a909-9c9f6e509408.png)

when we clone a remote repo or push something to remote, something gets created called "Remote Tracking Branch" it's like "HEAD" for your remote branch.it shows most recently known state,the last time you communicated with remote branch  
__note:__ unlike "HEAD", "remote tracking branch" is not unique for each repo. for each remote branch, we have one RTB
the syntax is like this : "<remote>/<branch>" for example: origin/master  
unlike HEAD you can't move it around yourself by switching branches or in deattached HEAD mode;it moves only when you communicate with remote
 ![Screenshot (116)](https://user-images.githubusercontent.com/50621975/153491805-bc6d76a9-1fed-4baa-b8ab-a754aa819921.png)
![Screenshot (117)](https://user-images.githubusercontent.com/50621975/153491862-0d9e8810-1c3c-4e7c-b450-bf54c58d124b.png)
 
 we can see list of RTBs by :``` git branch -r```
 
 ![Screenshot (118)](https://user-images.githubusercontent.com/50621975/153496248-7cd065ef-38fa-4382-be79-e7c3f7bd0f67.png)
![Screenshot (119)](https://user-images.githubusercontent.com/50621975/153496273-ee6f1921-4963-4ab8-bc82-4c4b78b059e7.png)
![Screenshot (120)](https://user-images.githubusercontent.com/50621975/153496301-b7f012ac-3443-4127-9899-23fff504a84f.png)

  we can checkout RTBs:
![Screenshot (121)](https://user-images.githubusercontent.com/50621975/153496328-e1b47f90-6b8d-4d2b-bf1c-4117241b5555.png)
![Screenshot (122)](https://user-images.githubusercontent.com/50621975/153496333-464fa5e2-4e80-4e21-8bf6-f8b828a574ed.png)

### wierd behavior after cloning:
as u might have already noticed, after you clone a repo if u type ```git branch``` ,you only see master or main!but if u type ``` git branch -r``` you'll see all remote branches .looks like other branches did not come with master or they are hidden.well typically after cloning by defualt my master branch is set to track origin/master .but this is not the case for other remote branches. which means you have to manually connect your local branch to those remote branches  
 and this can be easily done by ``` git switch <branch name>```
 ![Screenshot (123)](https://user-images.githubusercontent.com/50621975/153500416-2a991b8c-6ded-4d80-abb1-7540036089d9.png)
 ![Screenshot (124)](https://user-images.githubusercontent.com/50621975/153500436-bd5719ac-0f13-43a7-a8b0-da6d58bda32d.png)
![Screenshot (125)](https://user-images.githubusercontent.com/50621975/153500450-1d7d0e87-8317-4578-82cb-674d0d9521e9.png)
![Screenshot (126)](https://user-images.githubusercontent.com/50621975/153500463-85eeff1f-4cb0-4a9f-8368-a3b6b045b3f0.png)
![Screenshot (127)](https://user-images.githubusercontent.com/50621975/153500530-05e306c3-7438-472d-8b0b-babef27b6f09.png)
![Screenshot (128)](https://user-images.githubusercontent.com/50621975/153500546-a37c9dce-df22-4e18-bb63-30c07521f122.png)
what literally happens is after u switch git makes a local branch and connect to that already existed remote branch

## fetching:
 if we have multiple contributers and someone push some commits to let say branch master; by fetching those changes we update the RTB! not the actual local branches!
 i know the pic generally says local directory but actually the RTB in your local machine is the one who gets updated
![Screenshot (129)](https://user-images.githubusercontent.com/50621975/153505352-5e9293ed-eb0d-4b81-8f61-c84642ee75b6.png)
![Screenshot (131)](https://user-images.githubusercontent.com/50621975/153505384-b525d0ee-4b4d-48ac-9af8-4b66129175a0.png)
![Screenshot (132)](https://user-images.githubusercontent.com/50621975/153505396-01c52f11-a9db-4694-9dd3-ce1ae6d21508.png)
![Screenshot (133)](https://user-images.githubusercontent.com/50621975/153505406-7d519beb-0ef0-45c9-a142-c8b6ddc0c645.png)
![Screenshot (134)](https://user-images.githubusercontent.com/50621975/153505425-1ec398ea-8d09-4869-abfd-8c178c412b6f.png)
![Screenshot (135)](https://user-images.githubusercontent.com/50621975/153505434-22720a93-d1c5-4e93-9b0f-8c7752f02116.png)

the usual use case is like this: you type ```git status``` and it says "your branch_x is up to date with origin/branch_x"  __BUT__ that is just what git knows of github repo. the truth is branch_x has got updated multiple times by other collaborators in github(or even yourself from website). so what fetching does is letting git know "bitch you are far behind !"  and next time you type ``` git status ```, it says "you are n commits behind origin/branch_x"
 
 __Note: your local repo does not automatically checks github and update remote branches .you have to manually fetch the changes everytime you see them on github website __

 ## Pulling:
 pull implement those changes which made by others; in your repo in your actuall files and branches(not only remote branches)
![Screenshot (136)](https://user-images.githubusercontent.com/50621975/153554032-0ec9627d-a34f-4cd0-bf7f-eec9d6cfdd5d.png)
![Screenshot (137)](https://user-images.githubusercontent.com/50621975/153554055-de6fa358-3fbc-4b08-9628-9d59d549497d.png)
![Screenshot (138)](https://user-images.githubusercontent.com/50621975/153554067-3f611ef3-ce35-478a-87c0-faecc2cd5231.png)
 if you are on branch_x and run ``` git pull origin master``` while in there; it merges master remote branch to that branch_x. so its very important what branch you are currently on
![Screenshot (139)](https://user-images.githubusercontent.com/50621975/153554083-bf27d305-6cda-4f61-b4cc-557a27903e9a.png)
![Screenshot (140)](https://user-images.githubusercontent.com/50621975/153554095-92d1aa21-82ce-4c1e-8e36-51122113b504.png)
![Screenshot (141)](https://user-images.githubusercontent.com/50621975/153554113-7b0fa972-0a86-4149-b8f9-457a27978dd3.png)
![Screenshot (142)](https://user-images.githubusercontent.com/50621975/153554122-528694ad-35c2-411c-bb18-483817c7bd1a.png)
![Screenshot (143)](https://user-images.githubusercontent.com/50621975/153554132-445306c1-8326-4946-8d56-a60f7401757d.png)
![Screenshot (144)](https://user-images.githubusercontent.com/50621975/153554140-b019a8ca-df9b-4d67-aa98-114cdd86e224.png)
![Screenshot (145)](https://user-images.githubusercontent.com/50621975/153579275-8185012a-f51e-43a7-bc18-ea5015bfe175.png)
![Screenshot (146)](https://user-images.githubusercontent.com/50621975/153579282-daf84198-06f7-4036-ba19-7c72413e6cf1.png)
---
 # Github Pages:
 ![image](https://user-images.githubusercontent.com/50621975/153580059-5826bf30-5f0b-4e91-8c6b-957ec2eedde2.png)

---
 
 # Github Collaboration Workflows:
 aaand the worst github workflow award goes to __Centralized Workflow__.   
 the main problems of this are:
 * no one can work on anything without disturbing the main codebase
 * everytime someone wants to push some code,he or she probably have to pull the new commits first
 
 lets take a look at lots of slides to see how this works:
![Screenshot (148)](https://user-images.githubusercontent.com/50621975/153595790-3f9264ef-bab9-4340-ad7e-12bd07d93445.png)
![Screenshot (149)](https://user-images.githubusercontent.com/50621975/153595799-a255ca22-b3d9-463f-b1a7-f79fe54c3b97.png)
![Screenshot (151)](https://user-images.githubusercontent.com/50621975/153595835-088602f6-7cb3-4a5c-806f-074afb8f8bde.png)
![Screenshot (152)](https://user-images.githubusercontent.com/50621975/153595851-0cc2667f-17e4-48f6-a34f-79de79ba1e90.png)
![Screenshot (153)](https://user-images.githubusercontent.com/50621975/153595864-ec309d77-cc49-4074-afcb-d22a2fe3cb89.png)
![Screenshot (154)](https://user-images.githubusercontent.com/50621975/153595874-082bc5c6-8424-41a4-bc4f-507f0394b20d.png)
![Screenshot (155)](https://user-images.githubusercontent.com/50621975/153595880-5ccc2255-623c-4baa-b327-402a7bdc6e7f.png)
![Screenshot (156)](https://user-images.githubusercontent.com/50621975/153595893-500baaea-fcf5-4e6c-a298-03c0c153d8d8.png)
![Screenshot (157)](https://user-images.githubusercontent.com/50621975/153595907-d05c803e-86c9-4cf2-9bb1-089d082fd719.png)
![Screenshot (158)](https://user-images.githubusercontent.com/50621975/153595916-aad541b1-8f97-40de-aadd-e08b06a22249.png)
![Screenshot (159)](https://user-images.githubusercontent.com/50621975/153595933-cc1bc343-4ddf-43d1-9297-5113e1b364c3.png)
![Screenshot (160)](https://user-images.githubusercontent.com/50621975/153595945-cb66f567-818e-44fd-bf4c-7dff3395ab2b.png)
 ![Screenshot (161)](https://user-images.githubusercontent.com/50621975/153596143-f09d094e-c608-4b55-88f2-f765a26cce36.png)


 ## How to solve this?  .. feature branches workflow!
 all development should be done in diffrent branches. basically no one works on their experimental feature on master branch.only final results goes there.  
everyone can push their work without needing to first pulling remote repo,becuase they have their own seperate branch to work on 
![Screenshot (175)](https://user-images.githubusercontent.com/50621975/158075888-4bc95495-b829-4354-b6e5-a7e97d6dced2.png)
![Screenshot (176)](https://user-images.githubusercontent.com/50621975/158075890-41a20aa4-045f-4151-8045-95021d1bc605.jpg)
![Screenshot (179)](https://user-images.githubusercontent.com/50621975/158075894-eb57cc26-fa16-411b-9527-356c475ea4f1.png)
![Screenshot (180)](https://user-images.githubusercontent.com/50621975/158075898-efa52458-3405-460c-9246-24f960bf6db6.png)
![Screenshot (181)](https://user-images.githubusercontent.com/50621975/158075901-89fa5af1-3c93-4991-b039-b172925ab23c.png)
![Screenshot (182)](https://user-images.githubusercontent.com/50621975/158075904-3b37ba01-7adc-4c85-b812-a3cf4a477ee0.png)
![Screenshot (183)](https://user-images.githubusercontent.com/50621975/158075909-bf8f3670-c41f-46da-80ef-f44a45e3230a.png)
![Screenshot (184)](https://user-images.githubusercontent.com/50621975/158075913-aaf65222-53c0-44f8-ba63-73430ad3bbc8.png)
![Screenshot (185)](https://user-images.githubusercontent.com/50621975/158075918-024cb00b-2a44-4cdb-beb2-02c5a33091ef.png)
![Screenshot (186)](https://user-images.githubusercontent.com/50621975/158075919-22e9b34b-5ef0-4a8c-a15a-096ebb845b9a.png)
![Screenshot (187)](https://user-images.githubusercontent.com/50621975/158075922-eda13456-68e7-43f8-94b3-169ae2c08fd9.png)
![Screenshot (188)](https://user-images.githubusercontent.com/50621975/158075927-e2ed7504-2a28-48ef-86ae-6de7f29bc127.png)
![Screenshot (189)](https://user-images.githubusercontent.com/50621975/158075931-899f5784-d90a-41d1-9daa-8b874e036a08.png)
![Screenshot (190)](https://user-images.githubusercontent.com/50621975/158075934-e38014b0-089f-48a6-b579-169d13e8e4d9.png)
![Screenshot (191)](https://user-images.githubusercontent.com/50621975/158075939-cfe2fd9c-84e1-4de7-8a19-3434b75ec6b8.png)
![Screenshot (192)](https://user-images.githubusercontent.com/50621975/158075940-741f7469-8577-4eeb-a00b-a75cedeaa2af.png)

 
 

 
