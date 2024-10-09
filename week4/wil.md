# What did I learn this week? - 4

**목표**: 관계형 데이터베이스 이해하고 Django에 적용해보자

---

## Glossary

### 관계형 데이터베이스

**DB**: 데이터베이스. 데이터들을 한 곳에 모아서 분류하고 관리하여 원하는 데이터를 쉽게 꺼낼 수 있도록 한 것

**DBMS**: 데이터베이스 관리 시스템. 데이터를 데이터베이스에 어떤 형식으로 저장할지 관리한다. MySQL, redis, MongoDB 등

**관계형 DB**: 행과 열로 이루어진 테이블로 되어있는 DB. 데이터 구조화가 쉽고 중복 데이터를 최소화하기 좋다.

- **PK**: Primary Key, 기본 키. 관계형 DB의 행이 고유하도록 하는 키.

  - 학번, 이메일, 전화번호 등이 적절함
  - PK로 적절한 값이 없으면 id를 만드는 방법이 있음

- **FK**: Foreign Key, 외래 키. 관계형 DB에서 다른 테이블의 행을 식별할 수 있는 키.

  - 유저 id라는 FK를 만들고 유저의 정보는 FK와 같이 저장된 다른 테이블에서 불러올 수 있다.

## Django의 `models.py`로 DB 관리

**`models.py`**: 데이터를 저장, 검색, 관리함.

- 장고에서 지원하는 `Model` 클래스를 상속해 관계형 DB 클래스를 생성하는 역할
- 데이터 입출력, 양식 변환의 역할
- DBMS에 비종속적임
- `models.???Field()` 메서드로 원하는 자료형을 지정해 열을 생성

```python
from django.db import models

class Students(models.Model):
    id = models.CharField(max_length=7)
    name = models.CharField(max_length=20)
    address = models.TextField()
    birth_date = models.DateField()
```

- 장고에서 파일을 찾을 떄 먼저 가상환경 안을 확인 후, 찾는 파일이 없다면 manage.py 위치를 기준으로 찾는다.
  - 위 코드에서 `django.db`는 `venv`안에 있다.

```powershell
python manage.py makemigrations
# `models.py`의 변경사항을 migrations 폴더 내 저장
python manage.py migrate
# 가장 최신 migration을 찾아 DB를 생성
```

- `config/settings.py`에서 DB 종류를 설정할 수 있음

- `views.py`에서 `models.py`에서 만든 DB 클래스를 임포트하여 DB를 가져옴

  ```python
  Students.object.all()
  # DB를 전부 담은 QuerySet 반환
  Students.object.get(key = 'value')
  # 조건을 만족하는 행이 하나일 경우 그 행을 반환
  # 없거나 여러개이면 Exception 반환
  Students.object.filter(key = 'value')
  # 조건을 만족하는 QuerySet 반환

  ```

## Django 데이터 흐름

1. url이 요청됨
2. `urls.py`에서 `path()`를 사용해 요청된 url 주소에 해당하는 `views.py`의 함수 호출
3. `views.py`의 함수에서 정보를 가공해 딕셔너리를 만들고 그것을 표시할 html 파일로 넘김

   4. html 파일에서 딕셔너리의 데이터를 이용, 동적으로 html이 생성됨
   5. `views.py`에서 DB가 필요할 경우 `models.py`의 원하는 DB 클래스를 임포트하여 사용

## 느낀점

- 프레임워크의 프로젝트 구조를 처음에 전반적으로 공부하는 것이 이해에 도움이 되는 것 같다. 다른 프레임워크를 배울 때에도 구조를 먼저 공부해야겠다.

## 더 알아야할 것

- DBMS를 한 번도 접해보지 않아서 뭐하는 녀석인지 궁금하다. Django처럼 IDE에서 편집하는 건가? CLI인가? GUI로 된 앱인가? 엑셀같은 건가? 한 번 찍먹해 봐야겠다.
- `settings.py`에서 DB의 종류를 설정하는게 무슨 의미인가?
- QuerySet이 무엇인가?
