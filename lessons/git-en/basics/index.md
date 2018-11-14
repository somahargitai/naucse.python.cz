At a certain point, keeping track of all these versions becomes unfeasible.
These tools allow you to share your files easily, or to restore their content
A relatively large project wouldn't be manageable with this approach.
Currently, the most popular one is Git, and we'll learn more about it in this lesson.
> If you are not confident working with it yet, look at the
If you have skipped the lesson before, you might want to get back to it now.
Create a new directory now and navigate inside (use the command `cd`).
You can see the file using `ls -a` (Linux) or `dir /a` (Windows).
`.git` is a hidden directory because it is managed only by Git
about the state of the repository:
*“On branch master”* refers to so-called branches, we'll get back to that later.
*“Initial commit”* means that there is no revision stored yet.
And *“nothing to commit”* says that there are no files to be saved and versioned in the directory.
## First revision
Try adding something to Git now!
Create a new file `poem.txt` and write a short poem inside.
It should span at least five lines so that we have enough to work with.
Then, try executing `git status` again: Git reports that there is a new
file in the directory and that it isn't managed by Git yet.
        ␛[31mpoem.txt␛[m
We need to make Git track each new file explicitely.
Let's do that for the file with your poem:
␛[36m$␛[0m git add poem.txt
Then check the state of the repository again:
        ␛[32mnew file:   poem.txt␛[m
The lines in green (“changes to be committed”)
will be included in the next batch of changes (a *commit*) that you will create.
Let's create our first commit:
[master (root-commit) 1a009f4] First revision
 create mode 100644 poem.txt
After entering this command, an editor opens where you can write a short description 
of this commit, briefly summarizing what changes have been made.
This is referred to as a *commit message*. For now, a simple `First revision` will do.
You can ignore the existing lines starting with `#`, these are just for your information.
Git will ignore them as well. Finally, save the file and close the editor.
> [note] Working with editors
> In Windows, if you have
> [set up your Git correctly]({{ lesson_url('git/install') }}),
> Notepad will be used as the editor; simply write something, save (<kbd>Ctrl</kbd>+<kbd>S</kbd>)
> and close (<kbd>Alt</kbd>+<kbd>F4</kbd>).
> In Linux or macOS, an editor called Nano appears directly in the command line window.
> You can recognize it by the keyboard shortcut help on the bottom two lines.
> Write something, save using <kbd>Ctrl</kbd>+<kbd>O</kbd>,
> confirm the name of the file (<kbd>Enter</kbd>)
> and exit the editor using <kbd>Ctrl</kbd>+<kbd>X</kbd>.
> If you haven't set up Git accordingly, Vim is invoked directly in the command line window
> and will be used as the default editor.
> It is a relatively complicated editor and learning to use it is beyond the scope
> of this lesson. You can recognize it by one or two lines at the bottom that show a path
> to a temporary file that you are currently editing.
> In that case, first press
> <kbd>Esc</kbd>, then type `:q!` (colon, lower letter Q, exclamation mark)
> and confirm by pressing <kbd>Enter</kbd>.
> Then set up Git corrently and try `git commit` again.
Try reporting on the repository again:
This short report means that nothing has changed since the last commit.
That is expected since we've just commited all our changes!
Now let's have a look at what has changed in the last commit.
Execute `git show`:
    First revision
␛[1mdiff --git a/poem.txt b/poem.txt␛[m
␛[1m+++ b/poem.txt␛[m
Notice the unique 
<span class="yellow">Git commit ID</span>
that allows you to return to this state of your project at any point in the future.
The author's name, the date of this commit's creation and the commit message
are also listed, along with the summary of changes: a new file <tt class="strong">poem.txt</tt>
containing the <span class="green">text in green</span> has been added.
> When the output of a command is too long, you can browse it using the keys
> (<kbd>↓</kbd>, <kbd>↑</kbd>, <kbd>PgUp</kbd>, <kbd>PgDn</kbd>).
> In such case, exit the browsing mode by pressing <kbd>q</kbd> for *Quit*.
> [note] Text encoding in Windows
> If you have trouble with displaying special characters like letters with diacritics,
> enter the following command before `git show`:
> This command will only configure the current command line window.
> It will have to be entered for any new window that you open.
## Second revision
Make a small change in your poem; replace one word,
change punctuation, or add a new verse.
Then check the status of the Git repository again.
        ␛[31mmodified:   poem.txt␛[m
The file is shown in red again. Something has changed inside!
To see the details, execute the command <code>git diff</code>.
␛[1mdiff --git a/poem.txt b/poem.txt␛[m
␛[1m--- a/poem.txt␛[m
␛[1m+++ b/poem.txt␛[m
The changes are shown on a per-line basis.
The lines in <tt class="red">red</tt> beginning with <tt class="red">-</tt> indicate
the original lines that have been removed;
the lines in <tt class="green">green</tt> starting with <tt class="green">+</tt>
show the newly added lines.
> Even if just a single word or a letter has changed on any given line,
> the whole line will be listed as removed and added (including the small change).
> This interpretation can be customized if needed,
> but it's a good idea to get used to the default behavior.
It is easy to see what exactly has changed since the last commit.
If your program stops working, but the last commited version still worked,
use <code>git diff</code> –
one of the changes listed must have introduced the error!
> The line beginning with <tt class="blue">@@</tt> indicates the location in the file
> where the changes occur. In the example above, the excerpt of the original file
> starts at line number 1 and it is 6 lines long; the matching block in the changed varsion
> starts at line 1 as well, but it is 9 lines long.
If you are satisfied with the changes, stage them for the next commit:
␛[36m$␛[0m git add poem.txt
As usual, check the `status` of the repository; the file in green will be included
within the next commit.
        ␛[32mmodified:   poem.txt␛[m
Before we finalize the next commit, let's talk about the best practices
in formulating the commit messages.
There are common conventions that most programmers follow:
the first line summarizes the changes, the second line is left blank,
and the following lines list the reasons for the change or describe
the changes themselves in more detail.
Each line should have under 70 characters in length;
the lenth of the comments (lines starting with `#`) can serve as a guide here.
It is not worth going into detail for changes that are trivial or obvious;
rather, focus on the broader context and reasons for the changes.
Anything that can help whomever will try to understand the changes in the commit;
this might include you few months later.

My commit message will be the following:
Split long lines
Typically, each verse of a poem goes on its own line. I think
that it's easier to read like this. (Although, the real reason was 
to demonstrate git diff.)
> If you ever have trouble summarizing your changes using
> just 70 characters, you might be taking too many steps at once.
> E.g. "change string X and add loop Y"
> might be better to commit as two separate revisions.
Finally, use `git commit` to create your second revision,
and then check it using `git show`:
    Split long lines
    Typically, each verse of a poem goes on its own line. I think
    that it's easier to read like this. (Although, the real reason was 
    to demonstrate git diff.)
␛[1mdiff --git a/poem.txt b/poem.txt␛[m
␛[1m--- a/poem.txt␛[m
␛[1m+++ b/poem.txt␛[m
The diagram below visualizes what each command demonstrated thus far does exactly,
and how the changes move from “not staged” to “commited”.
    alt="Diagram showing the process of committing changes"
Now that we have created our first few revisions in the repository,
let's demonstrate more commands that will help us understand
the whole history of our Git repository.
The first command is <code>git log</code>.
    Split long lines
    Typically, each verse of a poem goes on its own line. I think
    that it's easier to read like this. (Although, the real reason was 
    to demonstrate git diff.)
    First revision
<code>git log</code> prints all commits starting from the newest one and going
all the way back to the initial commit at the origin of the repository.
When there are so many commits that they don't fit on a single screen
of your command line window, you can browse back and forth using
Finally, exit by pressing <kbd>q</kbd>.
> There are many options that customize the output of `git log`.
> They are all described (at great length)
> in the built-in documentation (command `git help log`).
> If the help is displayed in the command line window, press <kbd>q</kbd>
> to exit.
> My personal favorite combination is `git log --oneline --graph --decorate --cherry-mark --boundary`.
To see all details about any commit,
execute `git show 5ff0b`, replacing `5ff0b`
with the first few characters of the <span class="yellow">Git commit ID</span>.
The command line can convey all sorts of information,
but not always in a clear way.
A graphical application called *gitk* offers a more intuitive look
at the history of your repository;
you can start it using the command `gitk --all`:
    alt="Graphical application Gitk",
The application doesn't look very appealing (almost as if
it has been designed by programmers who emphasise substance over form),
but it will suit our needs.
Get familiar with it first, then close it, commit a few more sets of changes
and finally explore them using `git log` and `gitk --all`.

## Conclusion

These are the Git basics that we'll need in the following lessons.
Whenever you perform <code>git add <var>file</var></code> and `git commit`,
the current version of the file is saved and will be accessible even if you delete the file later.
You can always view any past version of any file in your repository,
and review all changes made since the last time the project was saved.

Maybe all this sounded unnecessarily too complicated for a beginner.
Indeed, our projects will be relatively simple and easy to manage
even without the use of Git.
But it's a good idea to learn using it from the very beginning;
when you get to participate in bigger projects, already being used to Git
will come very handy.

So, from now on, whenever you make even a small but meaningful change to your program,
as long as the program works at least as well as it did before,
use `git add` and `git commit` to save the change in Git.