# Be not afraid of git


TODO install git

TODO configure git

---

## Exercise 1) First commit

Make a folder for the toy project and get in there.
```
mkdir git-learn
cd git-learn
```

Initialise this folder as a git repository.
```
git init
```

Make a file.
```
touch names.txt
```

Now we can add the new file to the `staging area`. This step is required before we can commit.
```
git add names.txt
```

And commit the change, with a message.
```
git commit -m "Make a name file"
```


Have a look at the log with this command.
```
git log --pretty=oneline
```

You should see something like this.
```git
737468d8b3a80e0fc3fdc832313d37e6a35085d3 (HEAD -> master) Make a names file
```

This one-line form of the log shows us the commit ID, some info about which `branch` we are on, and the commit message. The 40 character long ID, also known as a `hash`, is a label which uniquely identifies the commit we just made. For more gory detail about how the hashes are generated, see https://blog.thoughtram.io/git/2014/11/18/the-anatomy-of-a-git-commit.html

As well as using hashes, git has `tags` such as HEAD which are nicknames for particular commits. `HEAD` is a nickname for the most recent commit, so `HEAD -> master` in the log tells us that we are at HEAD on the master branch.

`Branches` are tracks of work that diverge from the main line of development. They are a way of isolating your work from what other people are doing (or other work you are doing) in the code. Every git project has a `master` branch by default. Other branches are added according to the project or developer's individual needs.

Exit the log view by pressing `q`

---

## Exercise 2) A second commit

Write something to the file.
```
echo "ben" > names.txt
```

Check what state the project is in.
```
git status
```

Git tells us that a file has been `modified`. We can commit our change now. Previously, we did a two-stage process of adding then committing. Let's combine those into a single step.
```
git commit -am "Write a name into the file"
```

Have another look at the log
```
git log --pretty=oneline
```

Now we see two commits: two hashes, two messages. Notice that the HEAD tag has moved to the most recent commit. Exit the log view with `q`.

---

## Exercise 3) Third commit

Make a change to the file, commit it and check the log.
```
 echo "benny" > names.txt
 git commit -am "Change file content"
 git log --pretty=oneline
 ```

## Exercise 4) Branching

Let's start working on a new branch. First, make a new branch.
```
git branch "dev"
```

And change to working on that branch. You should see a message that you have "Switched to branch dev".
```
git checkout "dev"
```

Make another change to the file contents, commit that change, and repeat so that you have a couple of  commits on the dev branch. View the log to confirm.

Now let's go back to the master branch, and look at the log.
```
git checkout master
git log --pretty=oneline
```

EEEEK! WHERE'S ALL MY LATEST WORK GONE?

Don't worry, it's still there on dev branch. Have a look.
```
git checkout dev
git log --pretty=oneline
```

So you can move around between branches. Let's go back to master and add a new file.

```
git checkout master
touch "location.txt"
echo "here" > location.txt
git add .
git commit -m "Make loc file"
```

Have a look at the log now in graph view. This should show us the master and dev branches, with respective commits on each.
```
git log --graph --oneline --decorate --all
```

## Exercise 5) Go back in time

You can go back through commits too. This will go to the previous commit (aka the commit parent).


```
git reset --hard HEAD~
git log --pretty=oneline
```

Go back two ancestors with `git reset --hard HEAD~2`.

- HEAD~1 is one step back in history (nth ancestor commit, always following the first parent)
- HEAD^2 is second parent, not parent parent.

For more detail about the notation, see http://www.paulboxley.com/blog/2011/06/git-caret-and-tilde

Note that `reset` will destroy changes that you haven't committed. Make sure you have committed your work before using it.




---

# Further Reading

See this article for more information about the staging area https://dev.to/sublimegeek/git-staging-area-explained-like-im-five-1anh
