# Bisectercise

`git bisect` is a powerful tool for quickly determining when a particular bug was introduced into your project. This sample project will show you the basics of using `git bisect` to identify what commit broke this toy project.

## Clone this repo

Clone this repository to your local machine like so:

```
git clone https://github.com/bradleyboy/bisectercise.git
cd bisectercise
```

## See the broken functionality

Load the `index.html` file in a browser. Click `+` or `-`. Notice how the number always goes down. Oops!

Resist the urge to dig into the code and find the issue. The code in this example is admittedly trivial. Instead, let's practice using `git bisect` to find the offending commit.

## Find a good and bad commit

Bisect requires a *good* and *bad* commit. We already know the bad commit – `HEAD` is broken. But when was the last time our project was working properly? In our case, we know the initial commit in the project was working. Give it a try:

```
git checkout 4d83cf
```

Now refresh `index.html` in your browser. The `+` and `-` buttons should now work properly. Great, we've found a good commit!

## Starting the bisect

Now that we have a reference to both a good and bad commit, we can use `git bisect` to quickly find the bad commit. First, let's get back to the main branch:

```
git checkout main
```

Now start the bisect:

```
git bisect start HEAD 4d83cf
```

Notice we provide our known bad and good commits (in that order) as additional arguments after `git bisect start`.

Bisect now checks out a commit halfway between the good and bad commit. It will keep doing this until it finds the commit that first caused this bug. Each time, we need to test for the bug in the browser and tell bisect if this is a good or bad commit.

So now that we have started, load `index.html` in the browser again and see if the functionality is working as expected. If it is, tell bisect this is a good commit:

```
git bisect good
```

Otherwise, mark this commit as bad:

```
git bisect bad
```

Bisect will now check out another commit. Test again and mark the commit as good or bad using the commands we just used above. Keep repeating this process until bisect dumps out the offending commit, which will look something like this:

```
a1b2c3 is the first bad commit
```

Hooray! We found the bad commit.


## Understanding the Bug

Once git bisect locates the buggy commit, you can utilize git show to examine the changes introduced in that commit. This breakdown provides a detailed overview of the modifications made, aiding in pinpointing the root cause of the bug. By understanding the exact alterations that led to the issue, developers can devise an effective solution with clarity and precision.

Execute the following command to inspect the changes:

```
git show
```

Amazing! With this information, you can effectively address and fix the problematic commit.
