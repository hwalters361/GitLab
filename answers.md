# Quiz questions

This is only a "quiz" in the loosest sense that it's asking questions whose
answers will be part of your grade. Please use *any resources you want*, as
long as you list those resources (e.g. peers, websites, etc.)

# Resources Used
I used this stack overflow post to understand how to checkout a remote branch locally:
https://stackoverflow.com/questions/1783405/how-do-i-check-out-a-remote-git-branch

I used this stack overflow post to understand how to make a .gitignore file:
https://github.com/DomBennett/Teaching-github/tree/master

## Navigating logs

1. What is the SHA for the last commit made by Prof. Xanda on the branch
xanda_0000_movie_processing?
(For this and future questions, the first 5 characters is plenty - neither
Git nor I need the whole SHA.)
9b257

2. What is the SHA for the last commit associated with line 9 of this file?
b2ed3

3. What did line 12 of this file say in commit d1d83?
"2. I should really finish writing this."

4. What changed between commit e474c and 82045?

-    gross_sort = lambda x : x["Gross"]
+    gross_sort = lambda x : int(x["Gross"])

-    top_five = rows[:-5:-1]
+    top_five = rows[:-6:-1]

## Predicting merges

Assume at the start of each of these three questions that your
branch for switching to a top-10 list was called `top_ten`
and your branch generalizing to any number of movies was called `top_N`.
Predict the behavior of these three possible operations - you don't
have to provide a full `diff` but you should describe at a high level
what changes would happen.

These questions are supposed to be separate paths, not cumulative;
for example, you should *not* assume that the operations of 5 were run
before 6. When testing outcomes later in the lab, you should make sure to
revert back to the state of the branch before you started these questions.

5. What do you think would happen if you ran the following commands?
What branches would change, and how?
```
git checkout test
git merge top_N
```
I think that it would merge successfully. top_N's commits would be merged into test, and the process_movie_dataset would be updated with the data in top_N.

Since the top_N branch was created based on the test branch, there shouldn't be any conflicts. Git should perform a fast-forward merge, which means it would simply move the test branch pointer to the same commit as the top_N branch. The branches would change by pointing to the same commit, and there would be no merge commit created.

6. What do you think would happen if you ran the following commands?
What branches would change, and how?
```
git checkout top_ten
git merge test
```
I think we would get a merge conflict because the content of process_movie_data.py is different in top_ten than in top_N. We would get a merge conflict error. 

Since both branches have different changes (the top_ten branch has modifications for the top ten movies, and the test branch has changes for questions and answers), there is a potential for merge conflicts. If Git cannot automatically resolve these conflicts, it will require manual intervention to resolve them. 

7. What do you think would happen if you ran the following commands?
What branches would change, and how?
```
git checkout test
git rebase top_ten
git rebase top_N
```

We will not get an error.
Since top_ten was based on test, and top_N was also based on test, the rebase operation should proceed smoothly without conflicts. The test branch would be updated to include the changes from both top_ten and top_N branches, and there would be no merge conflicts.