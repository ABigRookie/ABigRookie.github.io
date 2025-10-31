---
title: "Git使用"
date: 2022-11-19 17:01:35
tags:
  - "Git"
---

# Git

*   fork项目同步

    ```bash
    # 1.clone
    $ git clone git@github.com:XXXX/XXXX.git

    # 2.remote(source repo)
    $ git remote add upstream git@github.com:XXXX/XXXX.git
    # how to delete upstream
    $ git remote rm upstream

    # 3.change to master branch(check brance before checkout)
    $ git checkout master

    # 4.fetch upstream
    $ git fetch upstream

    # 5.merge branch
    $ git merge upstream/master

    # 6.push to fork repo
    $ git push origin master
    ```

*   项目上传

    ```bash
    # 生成ssh key
    ssh-keygen -t rsa -C "email@address"

    # github-setting-ssh-add new ssh key

    # install git if git not exists
    sudo apt-get install git

    # cd the project directory and init the git
    git init

    # add the files need to upload
    # if want upload all files under the directory
    git add ./

    # check the status of git
    git status

    # submit the modification to the local repository
    git commit -m "notes"

    # add user name and user email
    git config --global user.email "email address"
    git config --global user.name "user name"

    # create a remote repository named origin
    git remote add origin SSH_KEY_OF_REPO

    # add files into origin
    git remote set-url origin SSH_KEY_OF_REPO

    # push to upload
    git push origin master
    ```
