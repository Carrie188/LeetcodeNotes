# What is Git ?

* Version control
* Time machine
* Check ponts ( commits )
* Multiverse ( branches )
* Sychronie ( merging )



```shell
// Git: https://git-scm.com/download/mac
// 1. reate 


// using homebrew
brew install git
// check if the version the latest
git --version
// 1. go to the directory of the project
// create a git foder and initialize a empty repository
git init

// staging files (add all the files of the project to the git)
git add --all
git add -A
git add .

// make comments while you commit
git commit -m "First Commit"

// go to log to verify if the actions above have done 
git log

// checke if there is anything changed in your project before doing the commit
git status

// restoring files that are staged in the last commit action  (recall the changes from the repository)
git restore --staged finleName.txt

// undo the changes in the local project
git restore .
git restore finleName.txt


// ignore files while commiting 
//1. add a file named: .gitignore in the local project
//2. add some ignore format in the file


// set a gloabl ignore file applying to all the project in your git 
git config --global core.excludesfile.[filename]

//clearing cache
git rm -r --cached

//delete a file, two way below: 
//1. delete a file manually and do the staging action (git add .)
//2. using command, this way can delete the file directly as well as make the action staged 
git rm filename.txt


// ... a lot actions can do 



//copying a branch 
git switch -c newbranchname

git switch branchname






```



## GitHub

```shell
// go to the directory of the project
git init
git add --all
git commit -m ""

//1. create a new repository on gitHub
guthub.new
//2. follow the instruction on the new repository
//…or push an existing repository from the command line
git remote add origin https://github.com/Carrie188/movie-booking-system-backend.git
// pushing all the local branchs to GitHub
git push --all

// remote
git remote add NAME URL
git remote remove NAME
git rename OLDNAME NEWNAME
git remote -v



// pull a branch to local folder
// go to the directory of the folder
git init
git pull <remote rpository> <branch>



//rE


// gitignore file
.DS_Store
.vscode/
authentication.js
node_modules
notes/
**/*-todo.md


// create a new repository on gitHub
https://github.new



```

