---
title: AWS EC2 -> Jupyter 셋팅
tags: [aws, jupyter]
categories: [jupyter]
published: true
comments : true
---

# 1.설치 명령어 

```console
sudo yum update
python --version
sudo yum install python3
python --version
python3 --version
sudo yum install python3-pip
pip3 --version
history

pip3 install jupyter

```

# 2.쥬피터 노트북 config 생성명령어

```console

jupyter notebook --generate-config

```

생성하는 경로에서 .jupyter 디렉토리가 생성됨 


# 3.python3 접속해서 해쉬 암호 생성

```
$> python3

>>> from notebook.auth import passwd
>>> passwd()


```
![](/assets/imgs/2020/05/19/1.png)


# 4.jupyter_notebook_config.py 셋팅

```
ls

cd .jupyter/
ls
jupyter_notebook_config.py -> 생성되었는지 확인 
vi jupyter_notebook_config.py
```

jupyter_notebook_config.py 파일 마지막줄에 

```sbtshell
c = get_config()
c.NotebookApp.password = u'해쉬암호'
c.NotebookApp.ip = '내부아이피'
c.NotebookApp.port = 내부포트
c.NotebookApp.notebook_dir = '/home/ec2-user/jupyter'

```


# 5.쥬피터 노트북 실행 명령어

```sbtshell

jupyter notebook --allow-root

```

# 6.기타 설치 명령어

쥬피터 노트북 이것저것 할때 은근히 설치 해야할 거 
자바는 한글 분석용 konlpy? 이거 쓸때 필요함 

- 폰트 셋팅
```sbtshell

yum install mkfontscale

yum install fontconfig

```

- 자바셋팅

```sbtshell

sudo yum install -y java-1.8.0-openjdk-devel.x86_64

```

# 7.쥬피터 노트북 백그라운드 실행모드

```

$> nohup jupyter notebook --allow-root > error.log &

$> ps -ef | grep jupyter 

$> kill -9 #{쥬피터 노트북 프로세스 아이디}

$> nohup jupyter notebook --allow-root > error.log & echo $!> pid.txt

$> kill -9 $(cat pid.txt)

```

이제 데이터 분석을 열심히 하면됨..