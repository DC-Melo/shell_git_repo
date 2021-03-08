#Basic Authentication
```
curl -u $GITHUB_USER:$GITHUB_TOCKEN https://api.github.com/user

```
# create a github repo
curl -u $GITHUB_USER:$GITHUB_TOCKEN https://api.github.com/user/repos -d '{ "name": "reponame","private":"false","description":"description" }'

