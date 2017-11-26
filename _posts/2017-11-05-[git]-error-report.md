## error: failed to push some refs to 'https://github.com 

> '-'로 시작하는 url은 push가 안되는 것같다.


```
bagjonghun-ui-MacBook-Pro:language jhoon$ git remote -v
origin	https://github.com/jhoon07/-study-language.git (fetch)
origin	https://github.com/jhoon07/-study-language.git (push)
bagjonghun-ui-MacBook-Pro:language jhoon$ git push -f origin  master
error: src refspec master does not match any.
error: failed to push some refs to 'https://github.com/jhoon07/-study-language.git'
```

```
bagjonghun-ui-MacBook-Pro:language jhoon$ git remote add origin2 https://github.com/jhoon07/study-language.git
bagjonghun-ui-MacBook-Pro:language jhoon$ git remote
origin
origin2
bagjonghun-ui-MacBook-Pro:language jhoon$ git push origin2 master
Counting objects: 3, done.
Writing objects: 100% (3/3), 211 bytes | 211.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/jhoon07/study-language.git
 * [new branch]      master -> master
bagjonghun-ui-MacBook-Pro:language jhoon$ 

```


