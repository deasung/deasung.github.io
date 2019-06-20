---

title: Hugo & Github 블로그 연동
layout: post 
category: devops
tags: 
  - hugo
  - github
  - blog
---

Hugo & Github 블로그 연동
---------------------------------------------


휴고를 이용해서 사이트 디렉토리 생성한다.
```
hugo new site dskim
```

디렉토리로 이동
```
cd dskim/
ls
```


git init설정해준다.
```
git init
```


git remote 저장소를 추가한다
```
git remote add origin https://github.com/deasung/deasung.github.io.git
```


gitignore에 public 디렉토리 안들어가도록 추가해준다 
```
echo 'public' >> .gitignore
```


gitignore 및 config.toml  <-알아서 추가가되어있을 것이다 
```
git add -A
```


git status상태 본다
```
git status
```


변경내용을 되돌린다. branch source에 push해준다
```
git checkout -b source
git add -A
git commit -m ‘Init commit'
git remote add origin https://github.com/deasung/deasung.github.io.git
git push origin source
```


hugo 테마를 담을 디렉토리 themes를 생성한다음 git clone으로 원하는 테마를 가져온다
```
/Users/dskim/Desktop/dskim/themes
mkdir themes
cd themes/
git clone https://github.com/zyro/hyde-x
```


테마를 가져온후에 git지워준다
```
rm -rf .git
```


nano config.toml 파일에 theme 테마명을 추가해준다.
![theme](/assets/imgs/2016/02/03/2016-02-03.png)

테마를 실행하면 경로에 public폴더가 자동생성됨
```
hugo -t hyde-x

cd public/
```


public 디렉토리안에 git 저장소를 추가한다음 master로 푸쉬해준다.

```
git init
git push origin master
git remote add origin https://github.com/deasung/deasung.github.io.git
git add -A
ls
git status
git commit -m 'test'
git push origin master
```


그다음부터는 반복적으로 
환경설정 및 post추가시에는 post를 추가한다음 source브랜치에 commit push 
 
테마를 돌린후에는 public 디렉토리를 master에 커밋한다음 푸쉬를 하면된다

참고 사이트

[https://gohugo.io/](https://gohugo.io/)

[https://gist.github.com/cobyism/4730490](https://gist.github.com/cobyism/4730490)

