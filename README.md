# super-worktree

Demonstration to show how git worktree works. Here's what I have done

Firstly, I created a new directory for my project and initialize a it repository
  
    mkdir  test-worktree
    cd  test-worktree
    git  init
    
 
Then, I make changes, stages it and commit to the  `main`  branch
    
    echo  "This is the initial commit, at main branch"  >  main.txt
    git  add  .
    git  commit  -m  "Initial commit"
    
Then, I need to work on a new feature so I created a  `features1`  branch
    
    git checkout -b features1
    
   Then, I add a worktree for the  `features1`  branch. This command creates a new directory (`f1-worktree`) next to my current project directory and is linked to the  `features1`  branch.
    
    git  worktree  add  ../f1-worktree  features1
    
By creating this directory, I can work on the new feature in branch `features1`  without disrupting my main workspace.   

Then I go inside the ```f1-worktree``` directory, make changes, stages it and commit. Changes made here are directly on the  `features1`  branch. By doing my work here, it's just like I had switched to  `features1`  in main project directory, but with the benefit of a separate workspace.
    
    cd  ../f1-worktree
    echo "Feature 1 in progress" > feature1.txt
    git  add  .
    git  commit  -m  "This is feature1"
    
   Then let say I need to fix a bug that just happened, I can just change the directory to main project directory, create a new branch and switch to that particular branch to fix the bug
    
    cd ../test-worktreee   # Assuming you're in the f1-worktree directory which just next to test-worktreee 
    git checkout -b fix-bug 
  
   
Then I fix the bug, stages it and commit it to the ```fix-bug``` branch without having to first commit my progress in branch ```features1```
    
    echo  "Critical bug fix"  >  hotfix.txt
    git  add  .
    git  commit  -m  "Fix critical bug"
    

Then I merge the ```fix-bug``` branch into main and delete the branch
    
    git  checkout  main
    git  merge  fix-bug
    git  branch  -d  fix-bug


Then, once the feature that I have been working on just now is complete, I merge it into  `main` branch.
    
    cd  ../test-worktreee
    git  merge  features1
    
 Finally, I remove the worktree for  `features1`  
    
    git  worktree  remove  ../features1-worktree
    
Before pushing this to the remote repository, I need to esnure that I have integrate the changes from the remote `main` branch into my  local `main` branch. So I fetch and merger the latest changes from remote repository using  `git pull`. If you're working in a team or on a public repository where others might be pushing changes, it's a good practice to frequently pull changes from the remote repository to avoid such conflicts.
 ```
git pull origin main
```
 
Finally, I push the changes to the remote repository 
```
   git push --set-upstream origin main
   ```

