# 6/9 금요일 수업

## 1. Django

### 1-1. 기본 리눅스 명령어

- `cd [경로]` : 해당 경로로 이동
- `pwd` : 현재 경로 보기
- `ls` : 현재 위치의 하위 폴더 리스트 보기
- `vi [편집할파일명]` : vi 편집기 열어서 파일 편집
  - `i` : insert 모드 (편집 시작할 수 있음)
  - `:wq!` : 저장 후 나가기
  - `:q!` : 저장하지 않고 나가기
- `cat [파일명]` : 파일 내용 출력
- `rm [fileName]` : 파일 제거
- `mv [fileName]` : 파일 이동
- `mkdir` : 디렉토리 생성
- `nohub [프로세스명]` : 세션이 끝나도 특정 프로세스가 계속 실행되도록 한다.

  - `nohub [프로세스명] &` : 백그라운드로 실행

- `ps ef|grep [프로세스명]` : 실행중인 프로세스와 관련된 명령어 검색

  - `kill -15 [pid]` : 프로세스 종료 (pid는 위 명령어로 확인 가능)
  - `kill -9 [pid]` : 강제 종료 (비권장)

- `ctrl + c ` : 현재 console (현재 사용자가 실행중인 프로그램) 종료

---

### 1-2. Django 기본

#### 📍 장고는 **Project**와 **App**으로 구성되어있음

- App : 하나의 독립적인 기능 (회원 앱, 상품 앱, 결제 앱 등등) 이며 다른 프로젝트에서 재사용이 가능
- Project : 복수의 앱들의 모임. manage.py가 위치한 곳

#### 📍 장고 서버 켜기

```
$ cd [projectName] //manage.py가 있는 프로젝트인지 경로 잘 보기!
$ python3 manage.py runserver 0.0.0.0:8000
```

후에 브라우저에서 **[공인ip]:8000** 접속

#### 📍 앱 생성하기

```
$ django-admin startapp [appName]
```

장고에서는 해당 app을 사용한다는 것에 대한 보고서 작성이 필요.
프로젝트의 하위에 프로젝트명과 동일한 이름의 앱이 있음. `settings.py` >
**_INSTALLED_APPS_** 항목 살펴보기

#### 📍 해당 **AppName/models.py**에서는 생성한 데이터베이스에 대한 model이 기술되어야 함. vi 편집기로 열어서 다음과 같이 입력.

```python
from django.db import models

# Create your models here.

class VipUser(models.Model):
        GENDERS = (('M','남성(Man)'),('W','여성(Woman)'))
        userid=models.CharField(max_length=64, verbose_name='id')
        username=models.CharField(max_length=5, verbose_name='username')
        password=models.CharField(max_length=64, verbose_name='password')
        gender=models.CharField(max_length=1, verbose_name='gender', choices=GENDERS)
        registered=models.DateTimeField(auto_now_add=True, verbose_name='register')
```

- option

  - **verbose_name** : 보는 사람을 위한 주석과 같은 것
  - **choices=GENDERS** : 정해진 값만 선택할 수 있게 제한 걸기
  - **auto_now_add** : 자동으로 기록할 것인지 선택 할 수 있음
- 이후 위에서 언급한 `settings.py` > **_INSTALLED_APPS_** 항목에 appName을 추가해주기

#### 📍 makemigrations (=local commit, 모델을 변경했다는 사실을 장고에게 알려주는 것)

`$ python3 manage.py makemigrations [appName]`

- 만약 실행시 다음과 같은 Traceback Error 발생한다면

```
  File "/root/newproject/vip_user/models.py", line 9
    userid=models.CharField(max_length=64, verbose_name='아이디')
                                                              ^
TabError: inconsistent use of tabs and spaces in indentation
```

models.py에서 tab과 space를 혼용해서 사용했을 때 뜨는 에러이므로
다른 편집기를 이용해서 수정하기!

- makemigrations 후

```
$ root@firstserver:~/newproject/vip_user/migrations# ls
0001_initial.py  __init__.py  __pycache__
```

`0001_initial.py` 파일 생성된 것 확인하기!

#### 📍 migrate (=server push)

`$ python3 manage.py migrate`

이 명령어 이후로 실서버에 반영, DB에 올라간 상태

#### 📍 Django admin 사용하기

`$ python3 manage.py createsuperuser` 로 admin id, pw 생성

- 장고는 DB 관리자 기능을 기본으로 제공함
- 웹에서 `[공인ip]:8000/admin` 으로 접속 후 해당 명령어로 생성한 id와 pw 입력
___

🤔🤔🤔 더 자세히 알고싶다면 : [Django App tutorial](https://docs.djangoproject.com/ko/3.2/intro/tutorial02/)
