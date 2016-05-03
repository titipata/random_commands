[back to home](../README.md)

# Git Pull Request

I just collaborated with few repository and first don't know how to deal with
forking. Here is a memo of, hopefully, good practice of how to make pull-request
to project that we want to contribute to.

As we know, when we want to contribute to outside project, we have to
fork that repository to our account. For example, if I want to contribute
to repo `john_doe/awesome_project`. Here is good practice to contribute to
the project

- First, I have to fork to `titipata/awesome_project`
- Clone `titipata/awesome_project` to my local computer
- Here, we will keep `master` branch up-to-date with `john_doe/awesome_project` and
we can `git pull https://github.com/john_doe/awesome_project.git` each time he
update the project.
- Now, we can create branch for developing feature branch name `feature`
i.e. `git checkout -b feature` and pull request to original repo from this branch.
- In case original repo has update, we can pull those changes to our `master`
branch in fork repo. Then we can merge it with current `feature` branch before
we create pull-request i.e. `git checkout feature` then `git rebase master`.
Afterward, you manage all the conflict and then do `git rebase --skip`
