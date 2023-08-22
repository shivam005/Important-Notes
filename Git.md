
# Merge multiple commit into one

git rebase -i HEAD~3
Here, 3 denotes the last afew commits which has to be merged into one. We can change this number as per our use case.

Step.1: you will get this into the editor -->
pick 03fd69e5 commit1
pick 6877ebea commit2
pick 3dd792e2 commit3

Step.2: Change this as below -->
pick 03fd69e5 commit1
squash 6877ebea commit2
squash 3dd792e2  commit3

Note: here, commit2 and commit3 will get merged into  commit1 

Step.3: Now, another editor will come wherein you will have to mention the commit message for the final commit -->
Final commit
// This is a combination of 3 commits.
// This is the 1st commit message:

Step.4: Now push the changes -->
 git push -f -u  origin [Name of the branch]

# 



 
git init  
git add README.md  
git commit -m "first commit"  
git branch -M main  
git remote add origin https://github.com/shivam005/Important-Notes.git  
git push -u origin main  



git remote add origin https://github.com/shivam005/Important-Notes.git  
git branch -M main  
git push -u origin main  
