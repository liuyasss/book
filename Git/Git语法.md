##  Git语法

##### Create a new repository

```
git clone git@gitlab.com:TcCode/demo.git
cd demo
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
```

##### Existing folder

```
cd existing_folder
git init
git remote add origin git@gitlab.com:TcCode/demo.git
git add .
git commit -m "Initial commit"
git push -u origin master
```

##### Existing Git repository

```
cd existing_repo
git remote add origin git@gitlab.com:TcCode/demo.git
git push -u origin --all
git push -u origin --tags
```