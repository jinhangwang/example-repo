#Stashing

When you find a bug that is obvious but small enough, like```cout<<"nama="<<endl;```, you may become crazy if you don't fix it before continuing your former work. You can use ```git stash``` to save the current work status,  fix that bug and go on with your work.

Imagine this situation: you just made a commit for a.cpp and are half way developing b.cpp, but you suddenly realize that there is a small mistake in a.cpp.
If you want to keep your work in b.cpp, you have to make a commit for b.cpp with half-way work and then back to a.cpp and fix the bug. If you back to fix the bug in a.cpp without making the commit for b.cpp, you'll lose all the work in b.cpp since the last commit. 

Stashing is a way to solve this kind of problem -- fix the bug in previous commit without losing your recent work.

Now let's try the stash command:
Create a.cpp and b.cpp, make a commit for a.cpp and make some development in b.cpp after the commit.
```
$ touch a.cpp
$ toch b.cpp
$ vim a.cpp
$ cat a.cpp
// hello world
$ git add a.cpp
$ git commit -m "helloworld a.cpp"
[master cd3e990] helloworld a.cpp
 1 file changed, 1 insertions(+)
$ git add b.cpp # suppose b.cpp has already been in the stage in the real situation
$ echo int main() >> b.cpp
$ echo { >> b.cpp
$ echo } >> b.cpp
$ cat b.cpp
int main()
{
}
```
Now use git stash to interupt the current work and back to the last commit cd3e990:
```
$ git stash
Saved working directory and index state WIP on master: df93074 helloworld a.cpp
HEAD is now at df93074 helloworld a.cpp
```
make some change(fix the bug in a.cpp) and commit it:
```
$ echo // a new line in a.cpp to test stash >> a.cpp
$ cat a.cpp
// hellow world
// a new line in a.cpp to test stash
$ git add a.cpp
$ git commit -m "add a line in a.cpp"
[master e495093] add a line in a.cpp
 1 file changed, 1 insertion(+)
```
Using ```git stash list``` to check your stash status:
```
$ git stash list
stash@{0}: WIP on master: cd3e990 helloworld a.cpp
```
Back to the status which updates the develop in a.cpp and keeps the work in b.cpp by ```git stash apply```
```
$git stash apply
$ cat b.cpp
int main()
{
}
$ cat a.cpp
// hellow world
// a new line in a.cpp
```
just a reminder: it seems that SVN doesn't have that function.
