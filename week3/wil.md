# What did I learn this week? - 3

**목표**: Django 프로젝트 파일 구조를 이해하자

---

## 장고 프로젝트 구조

> 다음부터 `|foo|` 형식은 이름이 `foo`인 디렉토리를 의미한다.

|**Project**|

- |**config**|

  - |\_\_pycache\_\_|
  - \_\_init\_\_.py
  - asgi.py
  - **settings.py**
  - **urls.py**
  - wsgi.py

- |**App**1|

  - |\_\_pycache\_\_|
  - |migrations|
  - \_\_init\_\_.py
  - admin.py
  - apps.py
  - **models.py**
  - test.py
  - **views.py**

- |**App**2|
  - |\_\_pycache\_\_|
  - |migrations|
  - \_\_init\_\_.py
  - admin.py
  - apps.py
  - **models.py**
  - test.py
  - **views.py**
- db.sqlite3
- **manage.py**

### 설명

- Django 프로젝트는 `|config|`와 여러 개의 어플리케이션 폴더들, `manage.py`로 이루어진다.

  - `|config|`와 `manage.py`를 생성하는 명령
    ```
    django-admin startproject config
    ```
    - 어플리케이션 폴더를 생성하는 명령
    ```
    django-admin startapp 어플리케이션이름
    ```

- `|config|`

  - `settings.py`는 데이터베이스 설정, 언어, 시간 설정 등을 담고 있다.
  - `asgi.py`와 `wasgi.py`는 데이터베이스를 관리하고 동적으로 html파일을 만든다고 한다.
    > ❓ `view.py`와 역할이 비슷한 것 같은데 어디에 사용하는 건지 잘 모르겠다.
    > 왜 `|config|`에 있는지도 모르겠다.
  - `urls.py`는 URL의 path를 보고 알맞은 어플리케이션의 알맞은 뷰로 연결시켜준다.

- 어플리케이션 폴더

  - `views.py`는 전체적인 흐름을 제어하고, 정보를 가공해서 템플릿으로 넘겨준다. 데이터베이스를 호출하기도 한다.
  - `|templates|`폴더를 어플리케이션 폴더 안에 만들고 html을 담아 템플릿을 만든다. 각 파일은 `views.py`에서 정보를 넘겨받아서 동적인 html을 생성한다.

- `manage.py`는 터미널로 미리 작성된 명령을 실행할 수 있게 해준다.

## 장고 프로젝트 만드는 법

0. 프로젝트를 만들고 싶은 폴더로 이동
1. venv(가상환경) 세팅
2. startproject
3. 프로젝트 폴더 안으로 이동
4. startapp
5. `settings.py`에서 필요한 설정 하기
6. 개발!
