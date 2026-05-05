# Flask dict CRUD 대비 콘솔 기반 문법 수업 자료

## 수업 목적

내일 진행할 콘솔 기반 문법 수업의 목적은 **Flask CRUD 코드를 마주했을 때 학생들이 당황하지 않게 만드는 것**이다.

Flask 실습에서 학생들이 가장 자주 마주치는 코드는 대략 다음 흐름이다.

```python
skill = request.form.get("skill", "").strip()
level = request.form.get("level", "").strip()
status = request.form.get("status", "").strip()

if skill == "":
    return redirect("/")

messages.append({
    "skill": skill,
    "level": level,
    "status": status
})
```

학생 입장에서는 이 코드에 여러 개념이 한꺼번에 들어 있다.

- 입력값 받기
- 공백 제거하기
- 빈 값 막기
- 딕셔너리 만들기
- 리스트에 딕셔너리 추가하기
- 조건에 따라 저장하거나 막기
- 리스트 안의 딕셔너리 읽기, 수정하기, 삭제하기

따라서 내일 수업은 Flask 화면을 띄우기 전에, 위 문법을 콘솔에서 먼저 다루는 것을 목표로 한다.

---

## 수업에서 제외하는 내용

아래 내용은 콘솔에서 억지로 설명하지 않는다.

- `def`
- `return`
- 함수의 인수
- `render_template()` 내부 구조
- 데코레이터 `@app.route()`의 원리
- `enumerate()`
- 딕셔너리 컴프리헨션
- 셋 컴프리헨션

이 내용은 실제 Flask 라우트를 작성하면서 화면 이동과 함께 설명하는 편이 더 직관적이다.

---

# 1부. 콘솔 입력 기초

---

## 문법 파트 1 — `input()`

### 📖 이론

`input()`은 사용자로부터 값을 입력받는 함수이다.
입력된 값은 항상 문자열로 저장된다.

Flask에서는 `request.form.get()`이 웹 화면의 입력값을 받는 역할을 한다.
콘솔에서는 그 역할을 `input()`으로 연습한다.

```python
name = input()
print(name)
```

---

### 💻 예제 코드

```python
name = input()
print(name)
```

---

### 📝 연습문제

#### 제목

입력값으로 인사 문장 만들기

#### 난이도

⭐⭐⭐

#### 발문

이름을 한 줄 입력받아 아래 형식으로 출력하시오.

```text
안녕하세요, 이름님
```

#### 정답 코드

```python
name = input()
print("안녕하세요, " + name + "님")
```

#### 테스트케이스

입력:

```text
민수
```

출력:

```text
안녕하세요, 민수님
```

입력:

```text
지현
```

출력:

```text
안녕하세요, 지현님
```

---

## 문법 파트 2 — `int(input())`

### 📖 이론

`input()`으로 받은 값은 문자열이다.
숫자 계산을 하려면 `int()`로 정수로 바꿔야 한다.

```python
num = int(input())
```

Flask에서도 폼으로 받은 값은 문자열이다.
나중에 번호, 인덱스, 점수 등을 사용할 때 정수 변환이 필요하다.

---

### 💻 예제 코드

```python
num = int(input())
print(num + 10)
```

---

### 📝 연습문제

#### 제목

입력받은 숫자의 두 배 출력하기

#### 난이도

⭐⭐⭐

#### 발문

숫자 하나를 입력받아 그 숫자의 두 배를 출력하시오.

#### 정답 코드

```python
num = int(input())
print(num * 2)
```

#### 테스트케이스

입력:

```text
5
```

출력:

```text
10
```

입력:

```text
12
```

출력:

```text
24
```

---

## 문법 파트 3 — `input().split()`

### 📖 이론

`input().split()`은 한 줄에 입력된 여러 문자열을 공백 기준으로 나눈다.

```python
a, b = input().split()
```

예를 들어 `Python Flask`를 입력하면 `a`에는 `Python`, `b`에는 `Flask`가 들어간다.

---

### 💻 예제 코드

```python
a, b = input().split()

print(a)
print(b)
```

---

### 📝 연습문제

#### 제목

두 단어 순서 바꿔 출력하기

#### 난이도

⭐⭐⭐

#### 발문

한 줄에 두 개의 문자열을 입력받아 순서를 바꿔 한 줄로 출력하시오.

예를 들어 `Python Flask`를 입력하면 `Flask Python`을 출력한다.

#### 정답 코드

```python
a, b = input().split()
print(b, a)
```

#### 테스트케이스

입력:

```text
Python Flask
```

출력:

```text
Flask Python
```

입력:

```text
HTML CSS
```

출력:

```text
CSS HTML
```

---

## 문법 파트 4 — `map(int, input().split())`

### 📖 이론

`map(int, input().split())`은 한 줄에 입력된 여러 값을 각각 정수로 바꾼다.

```python
a, b = map(int, input().split())
```

`input().split()`만 쓰면 문자열 두 개가 된다.
숫자로 계산하려면 `map(int, ...)`를 사용한다.

---

### 💻 예제 코드

```python
a, b = map(int, input().split())
print(a + b)
```

---

### 📝 연습문제

#### 제목

두 수 중 큰 수 출력하기

#### 난이도

⭐⭐⭐⭐

#### 발문

한 줄에 두 개의 숫자를 입력받아 둘 중 큰 수를 출력하시오.
두 수가 같으면 그 수를 출력하시오.

#### 정답 코드

```python
a, b = map(int, input().split())

if a >= b:
    print(a)
else:
    print(b)
```

#### 테스트케이스

입력:

```text
10 3
```

출력:

```text
10
```

입력:

```text
4 9
```

출력:

```text
9
```

입력:

```text
7 7
```

출력:

```text
7
```

---

# 2부. Flask CRUD 대비 기본 문법

---

## 문법 파트 5 — 문자열 결합

### 📖 이론

문자열은 `+` 연산자를 사용하여 이어 붙일 수 있다.

Flask에서는 사용자가 입력한 여러 값을 하나의 문자열로 만들어 저장하거나 출력할 때 사용한다.

---

### 💻 예제 코드

```python
skill = input()
level = input()

result = skill + " / " + level
print(result)
```

---

### 📝 연습문제

#### 제목

기술 정보 문자열 만들기

#### 난이도

⭐⭐⭐

#### 발문

세 줄에 걸쳐 `status`, `level`, `skill`을 입력받아 아래 형식으로 출력하시오.

```text
status / level / skill
```

#### 정답 코드

```python
status = input()
level = input()
skill = input()

result = status + " / " + level + " / " + skill
print(result)
```

#### 테스트케이스

입력:

```text
공부중
중
Python
```

출력:

```text
공부중 / 중 / Python
```

입력:

```text
미학습
하
SQL
```

출력:

```text
미학습 / 하 / SQL
```

---

## 문법 파트 6 — 비교 연산자 `==`

### 📖 이론

`==`는 두 값이 같은지 비교하는 연산자이다.

```python
skill == "Python"
```

같으면 `True`, 다르면 `False`가 된다.

---

### 💻 예제 코드

```python
skill = input()

if skill == "Python":
    print("백엔드")
else:
    print("기타")
```

---

### 📝 연습문제

#### 제목

SQL인지 확인하기

#### 난이도

⭐⭐⭐

#### 발문

문자열을 한 줄 입력받아 입력값이 `SQL`이면 `DB`를 출력하고, 아니면 `기타`를 출력하시오.

#### 정답 코드

```python
skill = input()

if skill == "SQL":
    print("DB")
else:
    print("기타")
```

#### 테스트케이스

입력:

```text
SQL
```

출력:

```text
DB
```

입력:

```text
Python
```

출력:

```text
기타
```

---

## 문법 파트 7 — 논리 연산자 `or`, `and`, `not`

### 📖 이론

논리 연산자는 여러 조건을 묶을 때 사용한다.

- `or`: 둘 중 하나라도 참이면 참
- `and`: 둘 다 참이어야 참
- `not`: 참과 거짓을 반대로 바꿈

---

### 💻 예제 코드

```python
skill = input()

if skill == "Python" or skill == "Java":
    print("백엔드 후보")
else:
    print("기타")
```

---

### 📝 연습문제

#### 제목

선택 가능한 기술 확인하기

#### 난이도

⭐⭐⭐⭐

#### 발문

두 줄에 걸쳐 `skill`과 `level`을 입력받는다.

아래 조건을 모두 만족하면 `선택 가능`을 출력하고, 아니면 `선택 불가`를 출력하시오.

조건:

- `skill`이 `Python` 또는 `Java`
- `level`이 `상`

#### 정답 코드

```python
skill = input()
level = input()

if (skill == "Python" or skill == "Java") and level == "상":
    print("선택 가능")
else:
    print("선택 불가")
```

#### 테스트케이스

입력:

```text
Python
상
```

출력:

```text
선택 가능
```

입력:

```text
Java
상
```

출력:

```text
선택 가능
```

입력:

```text
Python
중
```

출력:

```text
선택 불가
```

입력:

```text
HTML
상
```

출력:

```text
선택 불가
```

---

## 문법 파트 8 — `elif`

### 📖 이론

`elif`는 여러 조건을 순서대로 검사할 때 사용한다.

```python
if 조건1:
    실행문1
elif 조건2:
    실행문2
else:
    실행문3
```

Flask 화면에서 기술명에 따라 다른 배지 색상이나 분류를 지정할 때 연결된다.

---

### 💻 예제 코드

```python
skill = input()

if skill == "Python":
    print("백엔드")
elif skill == "SQL":
    print("DB")
else:
    print("기타")
```

---

### 📝 연습문제

#### 제목

기술명에 따라 분류 출력하기

#### 난이도

⭐⭐⭐⭐

#### 발문

문자열을 한 줄 입력받아 아래 조건에 따라 출력하시오.

- `Python` → `백엔드`
- `SQL` → `DB`
- `HTML` → `프론트`
- 그 외 → `기타`

#### 정답 코드

```python
skill = input()

if skill == "Python":
    print("백엔드")
elif skill == "SQL":
    print("DB")
elif skill == "HTML":
    print("프론트")
else:
    print("기타")
```

#### 테스트케이스

입력:

```text
Python
```

출력:

```text
백엔드
```

입력:

```text
SQL
```

출력:

```text
DB
```

입력:

```text
HTML
```

출력:

```text
프론트
```

입력:

```text
Java
```

출력:

```text
기타
```

---

## 문법 파트 9 — 빈 값 체크

### 📖 이론

파이썬에서는 빈 문자열 `""`이 거짓으로 판단된다.

```python
if skill:
    print("값 있음")
else:
    print("값 없음")
```

Flask에서는 사용자가 아무것도 입력하지 않고 제출했을 때 저장을 막는 데 사용한다.

---

### 💻 예제 코드

```python
skill = input()

if skill:
    print("입력됨")
else:
    print("비어 있음")
```

---

### 📝 연습문제

#### 제목

빈 입력 차단하기

#### 난이도

⭐⭐⭐⭐

#### 발문

문자열을 한 줄 입력받아 값이 비어 있지 않으면 `저장`을 출력하고, 비어 있으면 `취소`를 출력하시오.

#### 정답 코드

```python
skill = input()

if skill:
    print("저장")
else:
    print("취소")
```

#### 테스트케이스

입력:

```text
Python
```

출력:

```text
저장
```

입력:

```text

```

출력:

```text
취소
```

---

## 문법 파트 10 — `append()`

### 📖 이론

`append()`는 리스트 맨 뒤에 값을 추가하는 메소드이다.

Flask에서는 사용자가 입력한 데이터를 임시 리스트에 저장할 때 사용한다.

---

### 💻 예제 코드

```python
skills = ["Python", "HTML"]

new_skill = input()
skills.append(new_skill)

print(skills)
```

---

### 📝 연습문제

#### 제목

기존 기술 목록에 새 기술 추가하기

#### 난이도

⭐⭐⭐

#### 발문

기존 리스트가 있다.

```python
skills = ["Python", "HTML"]
```

문자열을 한 줄 입력받아 `skills` 리스트에 추가한 뒤 전체 리스트를 출력하시오.

#### 정답 코드

```python
skills = ["Python", "HTML"]

new_skill = input()
skills.append(new_skill)

print(skills)
```

#### 테스트케이스

입력:

```text
SQL
```

출력:

```text
['Python', 'HTML', 'SQL']
```

입력:

```text
CSS
```

출력:

```text
['Python', 'HTML', 'CSS']
```

---

## 문법 파트 11 — `remove()`

### 📖 이론

`remove()`는 리스트에서 특정 값을 삭제하는 메소드이다.

없는 값을 삭제하려고 하면 오류가 날 수 있으므로, 보통 `in`으로 먼저 확인한다.

---

### 💻 예제 코드

```python
skills = ["Python", "HTML", "SQL"]

target = input()

if target in skills:
    skills.remove(target)

print(skills)
```

---

### 📝 연습문제

#### 제목

기술 목록에서 입력값 삭제하기

#### 난이도

⭐⭐⭐⭐

#### 발문

기존 리스트가 있다.

```python
skills = ["Python", "HTML", "SQL"]
```

문자열을 한 줄 입력받아 해당 값이 리스트 안에 있으면 삭제하고, 없으면 그대로 둔다.
마지막에 전체 리스트를 출력하시오.

#### 정답 코드

```python
skills = ["Python", "HTML", "SQL"]

target = input()

if target in skills:
    skills.remove(target)

print(skills)
```

#### 테스트케이스

입력:

```text
HTML
```

출력:

```text
['Python', 'SQL']
```

입력:

```text
Java
```

출력:

```text
['Python', 'HTML', 'SQL']
```

---

## 문법 파트 12 — 리스트 인덱스 수정

### 📖 이론

리스트는 번호를 이용해 특정 위치의 값을 수정할 수 있다.
첫 번째 값의 번호는 `0`이다.

```python
skills[1] = "CSS"
```

Flask 수정 기능에서 특정 데이터의 값을 바꿀 때 연결된다.

---

### 💻 예제 코드

```python
skills = ["Python", "HTML", "SQL"]

index = int(input())
value = input()

skills[index] = value

print(skills)
```

---

### 📝 연습문제

#### 제목

입력한 위치의 기술명 수정하기

#### 난이도

⭐⭐⭐⭐

#### 발문

기존 리스트가 있다.

```python
skills = ["Python", "HTML", "SQL"]
```

첫 줄에는 수정할 인덱스 번호를 입력받는다.
둘째 줄에는 새 값을 입력받는다.

해당 위치의 값을 수정한 뒤 전체 리스트를 출력하시오.
입력되는 인덱스는 항상 `0`, `1`, `2` 중 하나라고 가정한다.

#### 정답 코드

```python
skills = ["Python", "HTML", "SQL"]

index = int(input())
value = input()

skills[index] = value

print(skills)
```

#### 테스트케이스

입력:

```text
0
Java
```

출력:

```text
['Java', 'HTML', 'SQL']
```

입력:

```text
1
CSS
```

출력:

```text
['Python', 'CSS', 'SQL']
```

입력:

```text
2
PostgreSQL
```

출력:

```text
['Python', 'HTML', 'PostgreSQL']
```

---

# 3부. 딕셔너리 CRUD 문법

---

## 문법 파트 13 — 딕셔너리 만들기

### 📖 이론

딕셔너리는 여러 값을 `key: value` 형태로 저장하는 자료형이다.

```python
item = {
    "skill": "Python",
    "level": "중",
    "status": "공부중"
}
```

Flask에서는 입력받은 여러 값을 하나의 데이터로 묶을 때 사용한다.

---

### 💻 예제 코드

```python
skill = input()
level = input()

item = {
    "skill": skill,
    "level": level
}

print(item)
```

---

### 📝 연습문제

#### 제목

기술 정보 딕셔너리 만들기

#### 난이도

⭐⭐⭐

#### 발문

세 줄에 걸쳐 `skill`, `level`, `status`를 입력받아 딕셔너리로 만든다.
그 뒤 아래 형식으로 출력하시오.

```text
skill / level / status
```

#### 정답 코드

```python
skill = input()
level = input()
status = input()

item = {
    "skill": skill,
    "level": level,
    "status": status
}

print(item["skill"] + " / " + item["level"] + " / " + item["status"])
```

#### 테스트케이스

입력:

```text
Python
중
공부중
```

출력:

```text
Python / 중 / 공부중
```

입력:

```text
SQL
하
미학습
```

출력:

```text
SQL / 하 / 미학습
```

---

## 문법 파트 14 — 딕셔너리 값 읽기

### 📖 이론

딕셔너리 값은 key로 읽는다.

```python
item["skill"]
```

리스트가 번호로 접근한다면, 딕셔너리는 이름표로 접근한다.

---

### 💻 예제 코드

```python
item = {
    "skill": "Python",
    "level": "중",
    "status": "공부중"
}

key = input()
print(item[key])
```

---

### 📝 연습문제

#### 제목

입력한 key의 값 출력하기

#### 난이도

⭐⭐⭐

#### 발문

아래 딕셔너리가 있다.

```python
item = {
    "skill": "Python",
    "level": "중",
    "status": "공부중"
}
```

key를 한 줄 입력받아 해당 값을 출력하시오.
입력되는 key는 항상 `skill`, `level`, `status` 중 하나라고 가정한다.

#### 정답 코드

```python
item = {
    "skill": "Python",
    "level": "중",
    "status": "공부중"
}

key = input()
print(item[key])
```

#### 테스트케이스

입력:

```text
skill
```

출력:

```text
Python
```

입력:

```text
level
```

출력:

```text
중
```

입력:

```text
status
```

출력:

```text
공부중
```

---

## 문법 파트 15 — `get()`으로 안전하게 읽기

### 📖 이론

`get()`은 딕셔너리 값을 안전하게 꺼낼 때 사용한다.
없는 key를 조회해도 오류가 나지 않는다.

```python
item.get("memo", "정보 없음")
```

Flask에서는 이 코드와 직접 연결된다.

```python
request.form.get("skill", "")
```

---

### 💻 예제 코드

```python
item = {
    "skill": "Python",
    "level": "중"
}

key = input()
print(item.get(key, "정보 없음"))
```

---

### 📝 연습문제

#### 제목

없는 key 안전하게 처리하기

#### 난이도

⭐⭐⭐⭐

#### 발문

아래 딕셔너리가 있다.

```python
item = {
    "skill": "Python",
    "level": "중",
    "status": "공부중"
}
```

key를 입력받아 해당 값을 출력하시오.
없는 key가 입력되면 `정보 없음`을 출력하시오.

#### 정답 코드

```python
item = {
    "skill": "Python",
    "level": "중",
    "status": "공부중"
}

key = input()
print(item.get(key, "정보 없음"))
```

#### 테스트케이스

입력:

```text
skill
```

출력:

```text
Python
```

입력:

```text
status
```

출력:

```text
공부중
```

입력:

```text
memo
```

출력:

```text
정보 없음
```

---

## 문법 파트 16 — 딕셔너리 값 수정하기

### 📖 이론

딕셔너리 값은 key를 이용해 수정할 수 있다.

```python
item["status"] = "복습중"
```

Flask Update에서 기존 데이터를 새 값으로 바꿀 때 사용한다.

---

### 💻 예제 코드

```python
item = {
    "skill": "Python",
    "level": "중",
    "status": "공부중"
}

item["status"] = "복습중"
print(item)
```

---

### 📝 연습문제

#### 제목

입력한 key의 값 수정하기

#### 난이도

⭐⭐⭐⭐

#### 발문

아래 딕셔너리가 있다.

```python
item = {
    "skill": "Python",
    "level": "중",
    "status": "공부중"
}
```

첫 줄에는 수정할 key를 입력받는다.
둘째 줄에는 새 값을 입력받는다.

key가 존재하면 값을 수정하고 전체 정보를 아래 형식으로 출력하시오.
key가 존재하지 않으면 `수정 불가`를 출력하시오.

```text
skill / level / status
```

#### 정답 코드

```python
item = {
    "skill": "Python",
    "level": "중",
    "status": "공부중"
}

key = input()
value = input()

if key in item:
    item[key] = value
    print(item["skill"] + " / " + item["level"] + " / " + item["status"])
else:
    print("수정 불가")
```

#### 테스트케이스

입력:

```text
skill
Java
```

출력:

```text
Java / 중 / 공부중
```

입력:

```text
level
상
```

출력:

```text
Python / 상 / 공부중
```

입력:

```text
status
복습중
```

출력:

```text
Python / 중 / 복습중
```

입력:

```text
memo
중요
```

출력:

```text
수정 불가
```

---

## 문법 파트 17 — 딕셔너리 key 삭제하기

### 📖 이론

딕셔너리에서 key를 삭제할 때는 `del`을 사용한다.

```python
del item["status"]
```

없는 key를 삭제하면 오류가 나므로 먼저 `in`으로 확인하는 것이 좋다.

---

### 💻 예제 코드

```python
item = {
    "skill": "Python",
    "level": "중",
    "status": "공부중"
}

key = input()

if key in item:
    del item[key]
    print("삭제 완료")
else:
    print("삭제 불가")

print(item)
```

---

### 📝 연습문제

#### 제목

입력한 key 삭제하기

#### 난이도

⭐⭐⭐⭐

#### 발문

아래 딕셔너리가 있다.

```python
item = {
    "skill": "Python",
    "level": "중",
    "status": "공부중"
}
```

삭제할 key를 입력받는다.

key가 존재하면 삭제한 뒤 `삭제 완료`를 출력한다.
key가 존재하지 않으면 `삭제 불가`를 출력한다.
마지막 줄에는 남은 딕셔너리를 출력한다.

#### 정답 코드

```python
item = {
    "skill": "Python",
    "level": "중",
    "status": "공부중"
}

key = input()

if key in item:
    del item[key]
    print("삭제 완료")
else:
    print("삭제 불가")

print(item)
```

#### 테스트케이스

입력:

```text
skill
```

출력:

```text
삭제 완료
{'level': '중', 'status': '공부중'}
```

입력:

```text
status
```

출력:

```text
삭제 완료
{'skill': 'Python', 'level': '중'}
```

입력:

```text
memo
```

출력:

```text
삭제 불가
{'skill': 'Python', 'level': '중', 'status': '공부중'}
```

---

# 4부. 리스트 안의 딕셔너리 CRUD

---

## 문법 파트 18 — 리스트 안의 딕셔너리 읽기

### 📖 이론

Flask에서 자주 쓰는 구조는 딕셔너리 하나가 아니라, 리스트 안에 딕셔너리가 여러 개 들어 있는 구조이다.

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"}
]
```

값을 읽을 때는 두 단계를 거친다.

```python
data[0]["skill"]
```

뜻은 다음과 같다.

1. `data[0]`으로 첫 번째 딕셔너리를 꺼낸다.
2. 그 딕셔너리에서 `"skill"` 값을 꺼낸다.

---

### 💻 예제 코드

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"},
    {"skill": "HTML", "level": "상", "status": "복습중"}
]

index = int(input())
item = data[index]

print(item["skill"] + " / " + item["level"] + " / " + item["status"])
```

---

### 📝 연습문제

#### 제목

번호로 기술 정보 조회하기

#### 난이도

⭐⭐⭐⭐

#### 발문

아래 데이터가 있다.

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"},
    {"skill": "HTML", "level": "상", "status": "복습중"}
]
```

번호를 입력받아 해당 번호의 기술 정보를 아래 형식으로 출력하시오.
입력되는 번호는 항상 `0`, `1`, `2` 중 하나라고 가정한다.

```text
skill / level / status
```

#### 정답 코드

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"},
    {"skill": "HTML", "level": "상", "status": "복습중"}
]

index = int(input())
item = data[index]

print(item["skill"] + " / " + item["level"] + " / " + item["status"])
```

#### 테스트케이스

입력:

```text
0
```

출력:

```text
Python / 중 / 공부중
```

입력:

```text
1
```

출력:

```text
SQL / 하 / 미학습
```

입력:

```text
2
```

출력:

```text
HTML / 상 / 복습중
```

---

## 문법 파트 19 — 리스트에 딕셔너리 추가하기

### 📖 이론

새로운 딕셔너리를 만들어 리스트에 추가하면 Create가 된다.

```python
data.append({
    "skill": skill,
    "level": level,
    "status": status
})
```

Flask에서는 form에서 받은 값을 딕셔너리로 묶은 뒤 리스트에 넣는 구조와 같다.

---

### 💻 예제 코드

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"}
]

skill = input()
level = input()
status = input()

data.append({
    "skill": skill,
    "level": level,
    "status": status
})

for item in data:
    print(item["skill"] + " / " + item["level"] + " / " + item["status"])
```

---

### 📝 연습문제

#### 제목

새 기술 정보 추가하기

#### 난이도

⭐⭐⭐⭐

#### 발문

아래 데이터가 있다.

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"}
]
```

세 줄에 걸쳐 `skill`, `level`, `status`를 입력받아 새로운 딕셔너리로 만든다.
그 딕셔너리를 `data` 리스트에 추가한 뒤 전체 목록을 출력하시오.

#### 정답 코드

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"}
]

skill = input()
level = input()
status = input()

data.append({
    "skill": skill,
    "level": level,
    "status": status
})

for item in data:
    print(item["skill"] + " / " + item["level"] + " / " + item["status"])
```

#### 테스트케이스

입력:

```text
HTML
상
복습중
```

출력:

```text
Python / 중 / 공부중
SQL / 하 / 미학습
HTML / 상 / 복습중
```

입력:

```text
Java
중
공부중
```

출력:

```text
Python / 중 / 공부중
SQL / 하 / 미학습
Java / 중 / 공부중
```

---

## 문법 파트 20 — 리스트 안의 딕셔너리 수정하기

### 📖 이론

리스트 안의 딕셔너리 값을 수정하려면 번호와 key를 함께 사용한다.

```python
data[index][key] = value
```

예를 들어 1번 데이터의 상태를 수정하려면 이렇게 쓴다.

```python
data[1]["status"] = "공부중"
```

---

### 💻 예제 코드

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"}
]

index = int(input())
key = input()
value = input()

data[index][key] = value

item = data[index]
print(item["skill"] + " / " + item["level"] + " / " + item["status"])
```

---

### 📝 연습문제

#### 제목

번호와 key로 기술 정보 수정하기

#### 난이도

⭐⭐⭐⭐⭐

#### 발문

아래 데이터가 있다.

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"},
    {"skill": "HTML", "level": "상", "status": "복습중"}
]
```

첫 줄에는 수정할 번호를 입력받는다.
둘째 줄에는 수정할 key를 입력받는다.
셋째 줄에는 새 값을 입력받는다.

key가 존재하면 값을 수정하고 수정된 한 줄만 출력하시오.
key가 존재하지 않으면 `수정 불가`를 출력하시오.

입력되는 번호는 항상 `0`, `1`, `2` 중 하나라고 가정한다.

#### 정답 코드

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"},
    {"skill": "HTML", "level": "상", "status": "복습중"}
]

index = int(input())
key = input()
value = input()

if key in data[index]:
    data[index][key] = value
    item = data[index]
    print(item["skill"] + " / " + item["level"] + " / " + item["status"])
else:
    print("수정 불가")
```

#### 테스트케이스

입력:

```text
0
level
상
```

출력:

```text
Python / 상 / 공부중
```

입력:

```text
1
status
공부중
```

출력:

```text
SQL / 하 / 공부중
```

입력:

```text
2
skill
CSS
```

출력:

```text
CSS / 상 / 복습중
```

입력:

```text
1
memo
중요
```

출력:

```text
수정 불가
```

---

## 문법 파트 21 — 리스트 안의 딕셔너리 삭제하기

### 📖 이론

리스트 안의 딕셔너리를 삭제할 때는 번호로 접근한 뒤 삭제할 수 있다.

```python
del data[index]
```

이 구조는 Flask에서 `/delete/0`, `/delete/1` 같은 주소로 삭제할 때 연결된다.

---

### 💻 예제 코드

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"},
    {"skill": "HTML", "level": "상", "status": "복습중"}
]

index = int(input())

del data[index]

for item in data:
    print(item["skill"] + " / " + item["level"] + " / " + item["status"])
```

---

### 📝 연습문제

#### 제목

번호로 기술 정보 삭제하기

#### 난이도

⭐⭐⭐⭐

#### 발문

아래 데이터가 있다.

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"},
    {"skill": "HTML", "level": "상", "status": "복습중"}
]
```

삭제할 번호를 입력받아 해당 딕셔너리를 삭제한 뒤 남은 전체 목록을 출력하시오.
입력되는 번호는 항상 `0`, `1`, `2` 중 하나라고 가정한다.

#### 정답 코드

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"},
    {"skill": "HTML", "level": "상", "status": "복습중"}
]

index = int(input())

del data[index]

for item in data:
    print(item["skill"] + " / " + item["level"] + " / " + item["status"])
```

#### 테스트케이스

입력:

```text
0
```

출력:

```text
SQL / 하 / 미학습
HTML / 상 / 복습중
```

입력:

```text
1
```

출력:

```text
Python / 중 / 공부중
HTML / 상 / 복습중
```

입력:

```text
2
```

출력:

```text
Python / 중 / 공부중
SQL / 하 / 미학습
```

---

# 5부. 리스트 컴프리헨션 반복 학습

---

## 문법 파트 22 — 리스트 컴프리헨션

### 📖 이론

리스트 컴프리헨션은 `for`문으로 리스트를 만드는 코드를 한 줄로 줄이는 문법이다.

기본 형태는 다음과 같다.

```python
[값 for 변수 in 반복대상]
```

조건을 붙일 수도 있다.

```python
[x for x in range(10) if x < 5]
```

조건을 2개 붙이면 두 조건을 모두 만족하는 값만 남는다.

```python
[x for x in range(10) if x < 5 if x % 2 == 0]
```

출력:

```text
[0, 2, 4]
```

위 코드는 아래 코드와 같은 뜻이다.

```python
result = []

for x in range(10):
    if x < 5:
        if x % 2 == 0:
            result.append(x)

print(result)
```

Flask 수업에서는 리스트 안의 딕셔너리에서 조건에 맞는 데이터만 골라낼 때 연결된다.

```python
study_items = [item for item in data if item["status"] == "공부중"]
```

---

### 💻 예제 코드 1 — 숫자 조건

```python
result = [x for x in range(10) if x < 5]
print(result)
```

출력:

```text
[0, 1, 2, 3, 4]
```

---

### 💻 예제 코드 2 — 조건 2개

```python
result = [x for x in range(10) if x < 5 if x % 2 == 0]
print(result)
```

출력:

```text
[0, 2, 4]
```

---

### 💻 예제 코드 3 — 리스트 안의 딕셔너리에서 기술명만 뽑기

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"},
    {"skill": "HTML", "level": "상", "status": "복습중"},
    {"skill": "Java", "level": "상", "status": "공부중"}
]

result = [item["skill"] for item in data if item["status"] == "공부중"]

print(result)
```

출력:

```text
['Python', 'Java']
```

---

### 📝 연습문제

#### 제목

조건 2개로 기술명만 뽑기

#### 난이도

⭐⭐⭐⭐⭐

#### 발문

아래 데이터가 있다.

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"},
    {"skill": "HTML", "level": "상", "status": "복습중"},
    {"skill": "Java", "level": "상", "status": "공부중"},
    {"skill": "CSS", "level": "하", "status": "복습중"}
]
```

리스트 컴프리헨션을 사용하여 다음 조건을 모두 만족하는 기술명만 리스트로 만들어 출력하시오.

조건:

- `level`이 `상`
- `status`가 `공부중`

#### 정답 코드

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"},
    {"skill": "HTML", "level": "상", "status": "복습중"},
    {"skill": "Java", "level": "상", "status": "공부중"},
    {"skill": "CSS", "level": "하", "status": "복습중"}
]

result = [
    item["skill"]
    for item in data
    if item["level"] == "상"
    if item["status"] == "공부중"
]

print(result)
```

#### 출력

```text
['Java']
```

---

# 6부. Flask CRUD 대비 데이터 유효성 검사 3대장

---

## 문법 파트 23 — `.strip()`과 빈 문자열 검사

### 📖 이론

Flask에서 폼을 통해 데이터를 받을 때 사용자가 스페이스바만 누르고 제출하는 경우가 있다.
이때 그냥 `if skill:`만 쓰면 공백도 값이 있는 것으로 처리될 수 있다.

그래서 문자열 양끝의 공백을 제거하는 `.strip()`을 사용한다.

```python
skill = skill.strip()
```

Flask에서는 나중에 이렇게 쓴다.

```python
skill = request.form.get("skill", "").strip()

if skill == "":
    return redirect("/")
```

---

### 💻 예제 코드

```python
skill = input()
skill = skill.strip()

if skill == "":
    print("입력값이 없습니다.")
else:
    print("입력된 기술:", skill)
```

---

### 📝 연습문제

#### 제목

공백 제거 후 빈 값 차단하기

#### 난이도

⭐⭐⭐

#### 발문

기술명을 입력받는다.
입력받은 값의 양옆 공백을 제거하시오.

공백 제거 후 값이 비어 있다면 `추가 불가`를 출력하고, 값이 있다면 `{'skill': 입력값}` 형태의 딕셔너리를 만들어 출력하시오.

#### 정답 코드

```python
skill = input()
skill = skill.strip()

if skill == "":
    print("추가 불가")
else:
    item = {"skill": skill}
    print(item)
```

#### 테스트케이스

입력:

```text
  Python  
```

출력:

```text
{'skill': 'Python'}
```

입력: 스페이스바 3번

```text
   
```

출력:

```text
추가 불가
```

입력:

```text
SQL
```

출력:

```text
{'skill': 'SQL'}
```

---

## 문법 파트 24 — `get()`의 기본값 빈 문자열 `""`

### 📖 이론

`dict.get("key", "기본값")`은 key가 없을 때 기본값을 돌려준다.

Flask에서는 폼 데이터가 아예 넘어오지 않았을 때 오류를 막기 위해 기본값으로 빈 문자열 `""`을 많이 사용한다.

```python
request.form.get("skill", "")
```

이 패턴을 이해하려면 딕셔너리에서 먼저 연습하는 것이 좋다.

---

### 💻 예제 코드

```python
item = {"skill": "Python"}

level = item.get("level", "")

if level == "":
    print("레벨 정보가 누락되었습니다.")
else:
    print(level)
```

---

### 📝 연습문제

#### 제목

빈 문자열 기본값으로 안전하게 조회하기

#### 난이도

⭐⭐⭐

#### 발문

아래 딕셔너리가 있다.

```python
item = {"skill": "SQL", "status": "미학습"}
```

조회할 `key`를 입력받는다.
`get()`을 사용하여 딕셔너리에서 값을 꺼내되, key가 없다면 빈 문자열 `""`을 기본값으로 가져오시오.

가져온 값이 빈 문자열이라면 `정보 누락`을 출력하고, 값이 있다면 그 값을 출력하시오.

#### 정답 코드

```python
item = {"skill": "SQL", "status": "미학습"}
key = input()

value = item.get(key, "")

if value == "":
    print("정보 누락")
else:
    print(value)
```

#### 테스트케이스

입력:

```text
skill
```

출력:

```text
SQL
```

입력:

```text
status
```

출력:

```text
미학습
```

입력:

```text
level
```

출력:

```text
정보 누락
```

---

## 문법 파트 25 — `in` / `not in`으로 허용된 값만 받기

### 📖 이론

사용자가 아무 값이나 서버로 보내면 데이터가 지저분해질 수 있다.
예를 들어 학습 상태는 `공부중`, `미학습`, `복습중` 세 가지만 허용해야 한다.

이때 `in`, `not in`과 리스트를 함께 사용한다.

```python
allowed = ["공부중", "미학습", "복습중"]

if status not in allowed:
    print("잘못된 값")
```

이 구조는 Flask Create와 Update에서 잘못된 값이 저장되는 것을 막는다.

---

### 💻 예제 코드

```python
allowed_status = ["공부중", "미학습", "복습중"]
status = input()

if status not in allowed_status:
    print("허용되지 않은 상태입니다.")
else:
    print("상태가 정상적으로 입력되었습니다.")
```

---

### 📝 연습문제

#### 제목

허용된 상태 값만 업데이트하기

#### 난이도

⭐⭐⭐⭐

#### 발문

아래 데이터가 있다.

```python
item = {"skill": "Python", "status": "미학습"}
```

새로운 상태를 입력받는다.
허용되는 상태는 `공부중`, `미학습`, `복습중` 세 가지뿐이다.

입력받은 상태가 허용된 상태가 아니라면 `잘못된 상태 값`을 출력하시오.
허용된 상태라면 딕셔너리의 `status`를 수정한 뒤 딕셔너리 전체를 출력하시오.

#### 정답 코드

```python
item = {"skill": "Python", "status": "미학습"}
status = input()
allowed = ["공부중", "미학습", "복습중"]

if status not in allowed:
    print("잘못된 상태 값")
else:
    item["status"] = status
    print(item)
```

#### 테스트케이스

입력:

```text
공부중
```

출력:

```text
{'skill': 'Python', 'status': '공부중'}
```

입력:

```text
미학습
```

출력:

```text
{'skill': 'Python', 'status': '미학습'}
```

입력:

```text
복습중
```

출력:

```text
{'skill': 'Python', 'status': '복습중'}
```

입력:

```text
마스터함
```

출력:

```text
잘못된 상태 값
```

---

# 7부. 형성평가

형성평가는 실전 레벨로 구성한다.
단순 암기가 아니라, Flask CRUD에서 실제로 마주칠 데이터 흐름을 콘솔 문제로 바꾼 형태이다.

---

## 형성평가 1 — 단순 딕셔너리 생성과 출력

### 난이도

⭐⭐⭐⭐⭐

### 발문

세 줄에 걸쳐 기술명, 수준, 학습 상태를 입력받는다.
입력받은 값을 딕셔너리에 저장한 뒤 아래 형식으로 출력하시오.

```text
기술명 / 수준 / 학습상태
```

### 정답 코드

```python
skill = input()
level = input()
status = input()

item = {
    "skill": skill,
    "level": level,
    "status": status
}

print(item["skill"] + " / " + item["level"] + " / " + item["status"])
```

### 테스트케이스

입력:

```text
Python
중
공부중
```

출력:

```text
Python / 중 / 공부중
```

입력:

```text
SQL
하
미학습
```

출력:

```text
SQL / 하 / 미학습
```

입력:

```text
HTML
상
복습중
```

출력:

```text
HTML / 상 / 복습중
```

---

## 형성평가 2 — `get()`을 사용한 안전한 값 조회

### 난이도

⭐⭐⭐⭐⭐

### 발문

아래 딕셔너리가 있다.

```python
item = {
    "skill": "Python",
    "level": "중",
    "status": "공부중"
}
```

key를 한 줄 입력받아 해당 값을 출력하시오.
없는 key가 입력되면 `정보 없음`을 출력하시오.

### 정답 코드

```python
item = {
    "skill": "Python",
    "level": "중",
    "status": "공부중"
}

key = input()
print(item.get(key, "정보 없음"))
```

### 테스트케이스

입력:

```text
skill
```

출력:

```text
Python
```

입력:

```text
level
```

출력:

```text
중
```

입력:

```text
status
```

출력:

```text
공부중
```

입력:

```text
memo
```

출력:

```text
정보 없음
```

---

## 형성평가 3 — 단순 딕셔너리 값 수정

### 난이도

⭐⭐⭐⭐⭐

### 발문

아래 딕셔너리가 있다.

```python
item = {
    "skill": "Python",
    "level": "중",
    "status": "공부중"
}
```

첫 줄에는 수정할 key를 입력받는다.
둘째 줄에는 새 값을 입력받는다.

key가 존재하면 값을 수정한 뒤 전체 정보를 아래 형식으로 출력하시오.
key가 존재하지 않으면 `수정 불가`를 출력하시오.

```text
skill / level / status
```

### 정답 코드

```python
item = {
    "skill": "Python",
    "level": "중",
    "status": "공부중"
}

key = input()
value = input()

if key in item:
    item[key] = value
    print(item["skill"] + " / " + item["level"] + " / " + item["status"])
else:
    print("수정 불가")
```

### 테스트케이스

입력:

```text
skill
Java
```

출력:

```text
Java / 중 / 공부중
```

입력:

```text
level
상
```

출력:

```text
Python / 상 / 공부중
```

입력:

```text
status
복습중
```

출력:

```text
Python / 중 / 복습중
```

입력:

```text
memo
중요
```

출력:

```text
수정 불가
```

---

## 형성평가 4 — 딕셔너리 key 삭제

### 난이도

⭐⭐⭐⭐⭐

### 발문

아래 딕셔너리가 있다.

```python
item = {
    "skill": "Python",
    "level": "중",
    "status": "공부중"
}
```

삭제할 key를 입력받는다.

key가 존재하면 해당 key를 삭제하고 `삭제 완료`를 출력한다.
key가 존재하지 않으면 `삭제 불가`를 출력한다.
그다음 남은 딕셔너리를 출력하시오.

### 정답 코드

```python
item = {
    "skill": "Python",
    "level": "중",
    "status": "공부중"
}

key = input()

if key in item:
    del item[key]
    print("삭제 완료")
else:
    print("삭제 불가")

print(item)
```

### 테스트케이스

입력:

```text
skill
```

출력:

```text
삭제 완료
{'level': '중', 'status': '공부중'}
```

입력:

```text
level
```

출력:

```text
삭제 완료
{'skill': 'Python', 'status': '공부중'}
```

입력:

```text
status
```

출력:

```text
삭제 완료
{'skill': 'Python', 'level': '중'}
```

입력:

```text
memo
```

출력:

```text
삭제 불가
{'skill': 'Python', 'level': '중', 'status': '공부중'}
```

---

## 형성평가 5 — 리스트 안의 딕셔너리 조회

### 난이도

⭐⭐⭐⭐⭐

### 발문

아래 데이터가 있다.

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"},
    {"skill": "HTML", "level": "상", "status": "복습중"}
]
```

번호를 입력받아 해당 번호의 기술 정보를 아래 형식으로 출력하시오.
입력되는 번호는 항상 `0`, `1`, `2` 중 하나이다.

```text
skill / level / status
```

### 정답 코드

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"},
    {"skill": "HTML", "level": "상", "status": "복습중"}
]

index = int(input())
item = data[index]

print(item["skill"] + " / " + item["level"] + " / " + item["status"])
```

### 테스트케이스

입력:

```text
0
```

출력:

```text
Python / 중 / 공부중
```

입력:

```text
1
```

출력:

```text
SQL / 하 / 미학습
```

입력:

```text
2
```

출력:

```text
HTML / 상 / 복습중
```

---

## 형성평가 6 — 리스트에 딕셔너리 추가와 빈 값 차단

### 난이도

⭐⭐⭐⭐⭐

### 발문

아래 데이터가 있다.

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"}
]
```

세 줄에 걸쳐 `skill`, `level`, `status`를 입력받는다.

조건:

- `skill`의 양옆 공백을 제거한다.
- 공백 제거 후 `skill`이 비어 있으면 `추가 불가`를 출력한다.
- `skill`이 비어 있지 않으면 새 딕셔너리를 만들어 `data`에 추가한다.
- 추가 성공 시 전체 목록을 아래 형식으로 출력한다.

```text
skill / level / status
```

### 정답 코드

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"}
]

skill = input().strip()
level = input().strip()
status = input().strip()

if skill == "":
    print("추가 불가")
else:
    data.append({
        "skill": skill,
        "level": level,
        "status": status
    })

    for item in data:
        print(item["skill"] + " / " + item["level"] + " / " + item["status"])
```

### 테스트케이스

입력:

```text
HTML
상
복습중
```

출력:

```text
Python / 중 / 공부중
SQL / 하 / 미학습
HTML / 상 / 복습중
```

입력:

```text
  Java  
중
공부중
```

출력:

```text
Python / 중 / 공부중
SQL / 하 / 미학습
Java / 중 / 공부중
```

입력: 첫 줄에 스페이스바 3번

```text
   
상
복습중
```

출력:

```text
추가 불가
```

---

## 형성평가 7 — 리스트 안의 딕셔너리 수정과 허용값 검사

### 난이도

⭐⭐⭐⭐⭐

### 발문

아래 데이터가 있다.

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"},
    {"skill": "HTML", "level": "상", "status": "복습중"}
]
```

첫 줄에는 수정할 번호를 입력받는다.
둘째 줄에는 새로운 `status` 값을 입력받는다.

허용되는 `status`는 `공부중`, `미학습`, `복습중` 세 가지이다.

조건:

- 입력되는 번호는 항상 `0`, `1`, `2` 중 하나이다.
- 입력받은 status의 양옆 공백을 제거한다.
- 허용되지 않은 status가 입력되면 `잘못된 상태 값`을 출력한다.
- 허용된 status라면 해당 번호의 `status`를 수정한 뒤 수정된 한 줄만 출력한다.

### 정답 코드

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"},
    {"skill": "HTML", "level": "상", "status": "복습중"}
]

index = int(input())
status = input().strip()
allowed = ["공부중", "미학습", "복습중"]

if status not in allowed:
    print("잘못된 상태 값")
else:
    data[index]["status"] = status
    item = data[index]
    print(item["skill"] + " / " + item["level"] + " / " + item["status"])
```

### 테스트케이스

입력:

```text
0
복습중
```

출력:

```text
Python / 중 / 복습중
```

입력:

```text
1
공부중
```

출력:

```text
SQL / 하 / 공부중
```

입력:

```text
2
  미학습  
```

출력:

```text
HTML / 상 / 미학습
```

입력:

```text
1
마스터함
```

출력:

```text
잘못된 상태 값
```

---

## 형성평가 8 — 리스트 안의 딕셔너리 삭제

### 난이도

⭐⭐⭐⭐⭐

### 발문

아래 데이터가 있다.

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"},
    {"skill": "HTML", "level": "상", "status": "복습중"}
]
```

삭제할 번호를 입력받아 해당 딕셔너리를 삭제한 뒤 남은 전체 목록을 출력하시오.
입력되는 번호는 항상 `0`, `1`, `2` 중 하나이다.

### 정답 코드

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"},
    {"skill": "HTML", "level": "상", "status": "복습중"}
]

index = int(input())

del data[index]

for item in data:
    print(item["skill"] + " / " + item["level"] + " / " + item["status"])
```

### 테스트케이스

입력:

```text
0
```

출력:

```text
SQL / 하 / 미학습
HTML / 상 / 복습중
```

입력:

```text
1
```

출력:

```text
Python / 중 / 공부중
HTML / 상 / 복습중
```

입력:

```text
2
```

출력:

```text
Python / 중 / 공부중
SQL / 하 / 미학습
```

---

## 형성평가 9 — 리스트 컴프리헨션으로 조건 검색

### 난이도

⭐⭐⭐⭐⭐

### 발문

아래 데이터가 있다.

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"},
    {"skill": "HTML", "level": "상", "status": "복습중"},
    {"skill": "Java", "level": "상", "status": "공부중"},
    {"skill": "CSS", "level": "하", "status": "복습중"}
]
```

첫 줄에는 `level`을 입력받는다.
둘째 줄에는 `status`를 입력받는다.

리스트 컴프리헨션을 사용하여 두 조건을 모두 만족하는 기술명만 리스트로 출력하시오.

입력되는 `level`은 `상`, `중`, `하` 중 하나이다.
입력되는 `status`는 `공부중`, `미학습`, `복습중` 중 하나이다.

### 정답 코드

```python
data = [
    {"skill": "Python", "level": "중", "status": "공부중"},
    {"skill": "SQL", "level": "하", "status": "미학습"},
    {"skill": "HTML", "level": "상", "status": "복습중"},
    {"skill": "Java", "level": "상", "status": "공부중"},
    {"skill": "CSS", "level": "하", "status": "복습중"}
]

level = input()
status = input()

result = [
    item["skill"]
    for item in data
    if item["level"] == level
    if item["status"] == status
]

print(result)
```

### 테스트케이스

입력:

```text
상
공부중
```

출력:

```text
['Java']
```

입력:

```text
상
미학습
```

출력:

```text
[]
```

입력:

```text
상
복습중
```

출력:

```text
['HTML']
```

입력:

```text
중
공부중
```

출력:

```text
['Python']
```

입력:

```text
중
미학습
```

출력:

```text
[]
```

입력:

```text
중
복습중
```

출력:

```text
[]
```

입력:

```text
하
공부중
```

출력:

```text
[]
```

입력:

```text
하
미학습
```

출력:

```text
['SQL']
```

입력:

```text
하
복습중
```

출력:

```text
['CSS']
```

---

## 형성평가 10 — `strip()`과 `get()` 기본값을 사용한 안전한 입력 처리

### 난이도

⭐⭐⭐⭐⭐

### 발문

아래와 같은 `form` 딕셔너리가 있다고 가정한다.

```python
form = {
    "skill": "  Python  ",
    "status": "공부중"
}
```

실제 제출 코드는 첫 줄에 `skill`, 둘째 줄에 `status`를 입력받아 `form` 딕셔너리를 만들어 사용한다.

조건:

- `form.get("skill", "")`로 skill을 가져온다.
- `form.get("status", "")`로 status를 가져온다.
- 두 값 모두 `.strip()`으로 양옆 공백을 제거한다.
- skill이 비어 있으면 `입력 오류`를 출력한다.
- skill이 있으면 `skill / status` 형식으로 출력한다.

### 정답 코드

```python
skill_input = input()
status_input = input()

form = {
    "skill": skill_input,
    "status": status_input
}

skill = form.get("skill", "").strip()
status = form.get("status", "").strip()

if skill == "":
    print("입력 오류")
else:
    print(skill + " / " + status)
```

### 테스트케이스

입력:

```text
  Python  
공부중
```

출력:

```text
Python / 공부중
```

입력:

```text
SQL
  미학습  
```

출력:

```text
SQL / 미학습
```

입력: 첫 줄에 스페이스바 3번

```text
   
복습중
```

출력:

```text
입력 오류
```

---

## 형성평가 11 — 허용된 상태값만 저장하는 실전 Create 로직

### 난이도

⭐⭐⭐⭐⭐

### 발문

아래 데이터가 있다.

```python
data = []
```

세 줄에 걸쳐 `skill`, `level`, `status`를 입력받는다.

조건:

- 세 입력값은 모두 `.strip()`으로 양옆 공백을 제거한다.
- `skill`이 비어 있으면 `추가 불가`를 출력한다.
- `status`는 `공부중`, `미학습`, `복습중`만 허용한다.
- 허용되지 않은 status가 입력되면 `잘못된 상태 값`을 출력한다.
- 모든 조건을 통과하면 딕셔너리를 만들어 `data`에 추가하고 `data`를 출력한다.

### 정답 코드

```python
data = []

skill = input().strip()
level = input().strip()
status = input().strip()

allowed_status = ["공부중", "미학습", "복습중"]

if skill == "":
    print("추가 불가")
elif status not in allowed_status:
    print("잘못된 상태 값")
else:
    data.append({
        "skill": skill,
        "level": level,
        "status": status
    })
    print(data)
```

### 테스트케이스

입력:

```text
Python
중
공부중
```

출력:

```text
[{'skill': 'Python', 'level': '중', 'status': '공부중'}]
```

입력:

```text
  SQL  
하
미학습
```

출력:

```text
[{'skill': 'SQL', 'level': '하', 'status': '미학습'}]
```

입력: 첫 줄에 스페이스바 3번

```text
   
상
복습중
```

출력:

```text
추가 불가
```

입력:

```text
HTML
상
완료
```

출력:

```text
잘못된 상태 값
```

---

# 8부. 다음 Flask 수업과 연결

내일 콘솔 수업이 끝나면 다음 Flask 수업에서 아래 코드를 만났을 때 학생들이 덜 당황해야 한다.

```python
skill = request.form.get("skill", "").strip()
level = request.form.get("level", "").strip()
status = request.form.get("status", "").strip()

allowed_status = ["공부중", "미학습", "복습중"]

if skill == "":
    return redirect("/")

if status not in allowed_status:
    return redirect("/")

messages.append({
    "skill": skill,
    "level": level,
    "status": status
})

return redirect("/")
```

학생들이 이 코드를 완전히 설명할 필요는 없다.
다만 아래 정도를 말할 수 있으면 성공이다.

- `get("skill", "")`은 값이 없을 때 빈 문자열을 사용한다.
- `.strip()`은 양옆 공백을 제거한다.
- `if skill == "":`는 빈 입력을 막는다.
- `status not in allowed_status`는 허용되지 않은 값을 막는다.
- `{ "skill": skill, ... }`은 입력값을 딕셔너리로 묶는 것이다.
- `messages.append(...)`는 딕셔너리를 리스트에 추가하는 것이다.

---

# 수업 운영 메모

## 오늘 반드시 잡아야 하는 것

- `input()`으로 입력값 받기
- `int(input())`로 번호 받기
- 문자열 결합
- 조건 분기
- 리스트 추가, 삭제, 수정
- 딕셔너리 만들기, 읽기, 수정, 삭제
- 리스트 안의 딕셔너리 읽기, 추가, 수정, 삭제
- `.strip()`으로 공백 제거
- `get(key, "")`의 의미
- `in` / `not in`으로 허용값 검사

## 오늘 무리해서 넣지 말 것

- 함수 정의
- `return`의 정확한 의미
- Flask 데코레이터 원리
- `render_template()` 분해
- `enumerate()`
- DB
- 딕셔너리 컴프리헨션
- 셋 컴프리헨션

## 최종 판단

내일 수업은 문법을 많이 배우는 날이 아니라, **Flask CRUD에서 나오는 코드를 해석할 수 있게 만드는 날**이다.

따라서 문법의 깊이보다 중요한 것은 다음 흐름이다.

```text
입력 → 공백 제거 → 유효성 검사 → 딕셔너리 생성 → 리스트 저장 → 조회/수정/삭제
```
