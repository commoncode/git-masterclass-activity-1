# Git Master Class Activity 1

This is simple repository to practice some of the concepts taught in Common Code's Git Master Class training course.

Here we cover an example of interactive rebasing and using a merge strategy for rebasing.

The only file (apart from this one) is [manuscript.md](https://github.com/commoncode/git-masterclass-activity-1/blob/master/manuscript.md) which is a plain text passage of English.

There is a series of branches already created to set the scene for this activity.

_Try to perform the tasks using commands in your computer terminal - if you get stuck then click 'Show me how'_ 

## Setup

> First off, clone and/or fork this repository locally.

<details><summary>Show me how</summary>
    
    mkdir commoncode
    cd commoncode
    git clone git@github.com:commoncode/git-masterclass-activity-1.git
    cd git-masterclass-activity-1
    
</details>

To restart the exercise at any time just `rm -Rf git-masterclass-activity-1` and re-clone.

-------------------------

This repo has a couple of branches with a sequence of commits resulting in a tree like this:

```
                E --- F --- K --- L     feature_2
               /
        C --- D --- I --- J             feature_1
       /
A --- B --- G --- H                     master

```
## Task
>Inspect the git log for all branches and verify the above structure

<details><summary>Show me how</summary>

    # The --all flag specifies all branches
    git log --graph --oneline --all

</details>

## Task
> Interactively rebase `feature_1` branch onto `master` and squash the last two commits

The goal is to have a new master branch with commits as 
```
A --- B --- C' --- D' --- I+J --- H' 
```

Where `C'` and `D'` are the same change as `C` and `D` respectively and `I+J` is the combined changes of `I` and `J`.

Note that commits G and C conflict - they both change the same line.

<details><summary>Show me how</summary>

    # Rebase feature_1 into master
    git checkout master
    git rebase feature_1 
    ## Commits G and C' conflict - however we want C' as our latest change. Open up your idea and select C' change
    ## Open up your idea and select C.
    git rebase --skip
    ## Commit H conflicts with feature_1 current state. Select H' change over feature_1.
    git add .
    git rebase --contiue

    # Squash J into I
    git checkout feature_1
    git rebase -i HEAD~6
    # in the rebase file, change line three to: squash 0d45141 J - incredible
    # in the commmit message file make the commit text: I+J - understanding and incredible
    

</details>

## Discussion Points
- Did you arrive at the expected structure?
- What might be some other methods of acheiving the same resu
