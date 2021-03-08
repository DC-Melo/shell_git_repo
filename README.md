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

