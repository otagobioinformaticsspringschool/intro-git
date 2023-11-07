# Creating a Repository

!!! clipboard-list "Objectives"

    - Create a local Git repository.
    - Describe the purpose of the `.git` directory.

Once Git is configured,
we can start using it.

We're going to use the Genomic Variant Calling workshop as the basis for our repository

First, let's navigate into the directory for the lesson `~/obss_2023/intro-git` and create a new directory `vc_project` there for our repository to live in:

!!! terminal-2

    ```bash
    $ cd ~/obss_2023/intro-git
    $ mkdir vc_project
    $ cd vc_project
    ```

Then we tell Git to make `vc_project` a repository
\-- a place where Git can store versions of our files:

!!! terminal-2

    ```bash
    $ git init
    ```

It is important to note that `git init` will create a repository that
can include subdirectories and their files---there is no need to create
separate repositories nested within the `vc_project` repository, whether
subdirectories are present from the beginning or added later. Also, note
that the creation of the `vc_project` directory and its initialization as a
repository are completely separate processes.

If we use `ls` to show the directory's contents,
it appears that nothing has changed:

!!! terminal-2

    ```bash
    $ ls
    ```

But if we add the `-a` flag to show everything,
we can see that Git has created a hidden directory within `vc_project` called `.git`:

!!! terminal-2

    ```bash
    $ ls -a
    ```

!!! terminal-2

    ```output
    .	..	.git
    ```

Git uses this special subdirectory to store all the information about the project,
including the tracked files and sub-directories located within the project's directory.
If we ever delete the `.git` subdirectory,
we will lose the project's history.

Next, we will change the default branch to be called `main`.
This might be the default branch depending on your settings and version
of git.
See the [setup episode](2_summary_setup.md#default-git-branch-naming) for more information on this change.

!!! terminal-2

    ```bash
    $ git checkout -b main
    ```

!!! terminal-2

    ```output
    Switched to a new branch 'main'
    ```

We can check that everything is set up correctly
by asking Git to tell us the status of our project:

!!! terminal-2

    ```bash
    $ git status
    ```

!!! terminal-2

    ```output
    On branch main

    No commits yet

    nothing to commit (create/copy files and use "git add" to track)
    ```

If you are using a different version of `git`, the exact
wording of the output might be slightly different.

!!! file-code "Places to Create Git Repositories"

    Along with tracking information about variant calling (the project we have already created),
    We would also like to track information about ecoli.
    Lets creates an `ecoli` project inside our `vc_project`
    project with the following sequence of commands:

    !!! terminal-2

        ```bash
        $ cd ~/obss_2023/intro-git   # return to Desktop directory
        $ cd vc_project     # go into vc_project directory, which is already a Git repository
        $ ls -a          # ensure the .git subdirectory is still present in the vc_project directory
        $ mkdir ecoli    # make a subdirectory vc_project/ecoli
        $ cd ecoli       # go into ecoli subdirectory
        $ git init       # make the ecoli subdirectory a Git repository
        $ ls -a          # ensure the .git subdirectory is present indicating we have created a new Git repository
        ```

    Is the `git init` command, run inside the `ecoli` subdirectory, required for
    tracking files stored in the `ecoli` subdirectory?

    ??? Solution

        No. we do not need to make the `ecoli` subdirectory a Git repository
        because the `vc_project` repository can track any files, sub-directories, and
        subdirectory files under the `vc_project` directory. Thus, in order to track
        all information about moons, we only needed to add the `ecoli` subdirectory
        to the `vc_project` directory.

        Additionally, Git repositories can interfere with each other if they are "nested":
        the outer repository will try to version-control
        the inner repository. Therefore, it's best to create each new Git
        repository in a separate directory. To be sure that there is no conflicting
        repository in the directory, check the output of `git status`. If it looks
        like the following, you are good to go to create a new repository as shown
        above:

        !!! terminal-2

            ```bash
            $ git status
            ```

        !!! terminal-2

            ```output
            fatal: Not a git repository (or any of the parent directories): .git
            ```

## Correcting `git init` Mistakes

A nested repository is redundant and may cause confusion
down the road. We would like to remove the nested repository. How can we undo
the last `git init` in the `ecoli` subdirectory?

!!! Solution -- USE WITH CAUTION!

    ### Background

    Removing files from a Git repository needs to be done with caution. But we have not learned
    yet how to tell Git to track a particular file; we will learn this in the next episode. Files
    that are not tracked by Git can easily be removed like any other "ordinary" files with

    !!! terminal-2

        ```bash
        $ rm filename
        ```

    Similarly a directory can be removed using `rm -r dirname` or `rm -rf dirname`.
    If the files or folder being removed in this fashion are tracked by Git, then their removal
    becomes another change that we will need to track, as we will see in the next episode.

    ??? Solution

        Git keeps all of its files in the `.git` directory.
        To recover from this little mistake, we can just remove the `.git`
        folder in the ecoli subdirectory by running the following command from inside the `vc_project` directory:

        !!! terminal-2

            ```bash
            $ rm -rf ecoli/.git
            ```

        But be careful! Running this command in the wrong directory will remove
        the entire Git history of a project you might want to keep.
        Therefore, always check your current directory using the command `pwd`.

!!! clipboard-list "keypoints"

    - `git init` initializes a repository.
    - Git stores all of its repository data in the `.git` directory.

```

```
