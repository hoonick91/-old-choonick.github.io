---
layout: post
title:  github.io_the-plain jekyll theme 적용하기
---

- theme를 다운 

```https://github.com/heiswayi/the-plain```


- repository를 만든다.

reposigory name = githubID.github.io


- 원격저장소를 만든다.

```$ git remote add origin http://github.com/githu..~```

- _config.yml 파일에 들어가 base url을 지우고 자신의 정보를 입력한다.

지우기 전

```
# Site Settings
url:                https://heiswayi.nrird.com # main url
baseurl:            /the-plain # for gh-pages
```

지운 후

```
# Site Settings
url:                https://githubname.github.io # main url
baseurl:            # for gh-pages
```


- github에 다운 받은 테마를 push 한다.

```
$ git init
$ git add .
$ git commit -m 'commit message'
$ git push origin master
```

 