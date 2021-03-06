#Basic Authentication
```
curl -u $GITHUB_USER:$GITHUB_TOCKEN https://api.github.com/user

```
# create a github repo
```
github:
curl -u $GITHUB_USER:$GITHUB_TOCKEN https://api.github.com/user/repos -d '{ "name": "reponame","private":"false","description":"description" }'
gitee:
curl -X POST --header 'Content-Type: application/json;charset=UTF-8' 'https://gitee.com/api/v5/user/repos' -d '{"access_token":"ACCESS_TOKEN","name":"REPONAME","has_issues":"true","has_wiki":"true","can_comment":"true"}'
```
# delete repo
```
gitee:
curl -X DELETE --header 'Content-Type: application/json;charset=UTF-8' 'https://gitee.com/api/v5/repos/DC-Melo/REPONAME?access_token=ACCESS_TOKEN'

```
# clear repo
```
gitee:
curl -X PUT --header 'Content-Type: application/json;charset=UTF-8' 'https://gitee.com/api/v5/repos/DC-Melo/jj/clear' -d '{"access_token":"ACCESS_TOKEN"}'

```

一个项目push到多个远程Git仓库

我创建了一个项目，然后通过下面的命令 push 到了 GitHub 上。如何再将这个项目 push 到其他远程仓库呢？

git remote add github https://github.com/zxbetter/test.git
git push -u github master
方法一: 使用 git remote add 命令
1.1# 如下命令查看远程仓库的情况，可以看到只有一个叫 github 的远程仓库。

git remote
github

git remote -v
github  https://github.com/zxbetter/test.git (fetch)
github  https://github.com/zxbetter/test.git (push)
1.2# 使用如下命令再添加一个远程仓库（这里以码云为例）

git remote add oschina https://git.oschina.net/zxbetter/test.git
1.3# 再次查看远程仓库的情况，可以看到已经有两个远程仓库了。然后再使用相应的命令 push 到对应的仓库就行了。这种方法的缺点是每次要 push 两次。

git remote
github
oschina

git remote -v
github  https://github.com/zxbetter/test.git (fetch)
github  https://github.com/zxbetter/test.git (push)
oschina https://git.oschina.net/zxbetter/test.git (fetch)
oschina https://git.oschina.net/zxbetter/test.git (push)
方法二: 使用 git remote set-url 命令
2.1# 删除方法一的 oschina 远程仓库。

git remote rm oschina
2.2# 使用如下命令添加远程仓库。

git remote set-url --add github https://git.oschina.net/zxbetter/test.git
2.3# 查看远程仓库情况。可以看到 github 远程仓库有两个 push 地址。这种方法的好处是每次只需要 push 一次就行了。

git remote -v
github  https://github.com/zxbetter/test.git (fetch)
github  https://github.com/zxbetter/test.git (push)
github  https://git.oschina.net/zxbetter/test.git (push)
方法三: 修改配置文件
打开 .git/config 找到 [remote "github"]，添加对应的 url 即可，效果如下。这种方法其实和方法二是一样的。

[remote "github"]
    url = https://github.com/zxbetter/test.git
    fetch = +refs/heads/*:refs/remotes/github/*
    url = https://git.oschina.net/zxbetter/test.git
关于 git pull
方法二和三在 push 的时候比较方便。但是在 pull 的时候只能从方法三中的第一个 url 地址拉取代码。而方法一则不存在这种问题（可能要解决冲突）。
所以，如果只进行 push 操作，推荐方法二和三，如果也要进行 pull 操作，推荐方法一。
