# NiPy

![License MIT](https://img.shields.io/badge/license-MIT-green)
![Python 3.7](https://img.shields.io/badge/python-v3.7-blue)

대한민국 교육부의 교육행정정보시스템인 나이스와 관련한 파이썬 개발을 하실 때 보다 용이하게 하실 수 있도록 돕는 모듈입니다.  
자세한 내용은 아래를 참고하여 주십시오.

## 환영합니다 🎐

대한민국 교육부는 2003년 부터 교육행정정보시스템인 나이스를 제공하기 시작하였습니다. 교육당국의 온-나라 시스템이라 불릴 정도로 대부분의 교육정보는 나이스에 제공되어 있습니다. 그래서 많은 학생 개발자분들은 나이스로부터 정보를 받아오는 프로그램을 개발하고는 합니다. 본인의 개발 실력을 검증할 수 있으며, 실생활에서도 많이 사용되기 때문이죠.

하지만 실제 개발에서는 많은 시행착오가 발생하기 마련입니다. 나이스로부터 정보를 받아오기 위해선 나이스의 로직을 파악하여야 하며, 로직을 파악하여도 원하는 정보를 크롤링해오는 스크립트를 짜야하죠. 이러한 과정은 힘들고 어려울 수 있습니다.

그래서 NiPy 라는 통합 모듈을 개발하여 추후에 나이스와 연계하여 개발하고자 할 때 조금 더 빨리 그리고 더 안정적으로 개발할 수 있도록 돕기로 하였습니다. 본 NiPy는 MIT 라이선스로 제공되기에 출처만 기재하시면 자유롭게 사용하실 수 있습니다.

## 사용하는 방법 📖

```
~ 사용하기에 앞서 ~

본 NiPy는 1인 개발과 학업을 병행하는 학생이 제작한 모듈입니다.
따라서 문제가 발생할 경우 빠르게 대처가 어려울 수 있으며
기능이 제대로 작동하지 않을 수 있습니다.
이점 참고하여 개발하여 주시기 바랍니다.

본 NiPy를 이용하여 구현하실 수 있는 기능은 다음과 같습니다.

- 학교 고유 코드 불러오기
- 급식 정보 불러오기

이 외에도 시간표 불러오기, 학교 정보 불러오기 기능 등을 기획, 개발 중입니다.
```

| 목차                                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------- |
| [모듈 설치하기](#모듈-설치하기)<br/>[학교 고유 코드 api (Scode)](#학교-고유-코드-api)<br/>[학교 급식 정보 api (Smeal)](#학교-급식-정보-api) |

### 모듈 설치하기

아래 목록의 모듈을 정상 사용을 위해 반드시 필요한 모듈입니다.  
설치를 진행하여 주시기 바랍니다.

- requests
- json
- bs4 (Beautifulsoup)

아래 목록의 모듈은 필요시 설치하여야 하는 모듈입니다.
선택 설치하시기 바랍니다.

- openpyxl
- csv

### 학교 고유 코드 api

**1. 기본 정보 설정**

우선 코드를 조회할 학교의 기본 정보를 설정하여야 합니다. 예시는 다음과 같습니다.

```python
# 경기도내에 있는 김포이라는 이름을 가진 학교를 조회합니다.
l = nipy.Scode("김포", "경기")
```

| 매개변수(예시) | 이름     | 설명                                                                                                                        |
| -------------- | -------- | --------------------------------------------------------------------------------------------------------------------------- |
| 고창           | 학교이름 | 조회할 학교 이름을 입력합니다.<br/>문자열 자료형입니다.                                                                     |
| 경기           | 지역명   | 학교가 소재한 지역이름입니다.<br/>시, 도를 제외한 2자리 문자열 자료형입니다.<br/>설정을 원치 않을 경우 0으로 두어도 됩니다. |

위의 매개변수를 각 학교별 사정에 맞추어 바꿔서 작성하여 주십시오.  
기본 설정이 완료되면 다음 항목을 진행하실 수 있습니다.

**2. 학교 코드 불러오기**

`codefind()`를 사용하면 코드를 불러올 수 있습니다.

```python
# 기본 설정된 학교 중에서 중등 교육기관을 출력합니다.
print(l.codefind("2"))
```

| 매개변수(예시) | 이름 | 설명                                                                                               |
| -------------- | ---- | -------------------------------------------------------------------------------------------------- |
| 2              | 교급 | 조회할 학교의 교급을 의미합니다.<br/>1자리 문자열 자료형입니다.<br/>부록을 참고해 작성해 주십시오. |

위의 매개변수를 올바르게 입력하시면 다음과 같은 결과를 받으실 수 있습니다.

```python
[{'NAME': '김포신곡중학교', 'ADDRESS': '경기도 김포시 고촌읍 수기로 54-20', 'CODE': 'J100005681'},
{'NAME': '김포여자중학교', 'ADDRESS': '경기도 김포시 봉화로 37-15', 'CODE': 'J100001488'},
{'NAME': '김포중학교', 'ADDRESS': '경기도 김포시 봉화로 83', 'CODE': 'J100001490'},
{'NAME': '김포한가람중학교', 'ADDRESS': '경기도 김포시 김포한강9로 140', 'CODE': 'J100006783'}]
```

반환되는 결과는 리스트 형태이며 0번부터 접근하실 수 있습니다.  
학교 정보는 딕셔너리 형태로 반환되며 NAME으로 학교이름, ADDRESS로 주소, CODE로 학교코드를 불러오실 수 있습니다.

**에러코드**

학교 코드를 불러오던 중 문제가 생기면 다음과 같은 에러코드를 반환합니다.

| 에러코드            | 제목           | 설명                                                                                                |
| ------------------- | -------------- | --------------------------------------------------------------------------------------------------- |
| SERVER ERROR        | 서버 접속 실패 | 학교알리미에 접속하지 못하였습니다.<br/>점검중이거나 교육청 측에서 차단할 경우 발생하는 문제입니다. |
| CAN NOT FIND SCHOOL | 학교 검색 실패 | 입력하신 학교명을 가진 초·중·고·특수학교가 존재하지 않습니다.<br/>지역 설정 확인 후 진행해 주세요.  |

**부록**

- 학교 교급

  | 교급     | 코드 |
  | -------- | ---- |
  | 초등학교 | 1    |
  | 중학교   | 2    |
  | 고등학교 | 3    |
  | 특수학교 | 4    |
  | 모든학교 | 0    |

### 학교 급식 정보 api

**1. 기본 정보 설정**

우선 학교 기본 정보를 설정하여야 합니다. 기본 설정 예시는 다음과 같습니다.

```python
# 경기과학고등학교를 기본 조회 학교로 설정합니다.
m = nipy.Smeal("경기", "J100000447", "4")
```

| 매개변수(예시) | 이름         | 설명                                                                                                       |
| -------------- | ------------ | ---------------------------------------------------------------------------------------------------------- |
| 경기           | 교육청(지역) | 교육청 소재지를 입력합니다.<br/>시, 도를 제외한 두글자를 입력해 주세요.<br/>2자리의 문자열 자료형입니다.   |
| J100000447     | 학교 코드    | 학교별 고유 코드입니다.                                                                                    |
| 4              | 학교교급     | 학교교급 구분을 위한 매개변수입니다.<br/>1자리의 문자열 자료형입니다.<br/>부록을 참고하시어 작성해 주세요. |

위의 매개변수를 각 학교별 사정에 맞추어 바꿔서 작성하여 주십시오.  
기본 설정이 완료되면 다음 항목을 진행하실 수 있습니다.

**2. 하루치 급식 불러오기**

`day()` 함수를 사용하면 하루치 급식을 반환받을 수 있습니다.

```python
# 경기과고의 19년 10월 27일자 중식 급식을 출력합니다.
print(m.day("2019", "10", "27", "2"))
```

| 매개변수(예시) | 이름     | 설명                                                                                        |
| -------------- | -------- | ------------------------------------------------------------------------------------------- |
| 2019           | 조회년도 | 조회를 원하는 날짜의 년도입니다.<br/>4자리의 문자열 자료형 입니다.                          |
| 10             | 조회월   | 조회를 원하는 날짜의 월입니다.<br/>2자리의 문자열 자료형 입니다.                            |
| 27             | 조회일   | 조회를 원하는 날짜의 일입니다.<br/>2자리의 문자열 자료형 입니다.                            |
| 2              | 급식종류 | 조회를 원하는 급식의 종류입니다.<br/>1자리의 문자열 자료형입니다.<br/>부록을 참고해 주세요. |

위의 매개변수를 각 학교별 사정에 맞추어 바꿔서 작성하여 주십시오.
정상적으로 요청하신 경우 다음과 같은 형식의 급식정보를 반환합니다.

```
현미밥<br/>김치수제비5.6.9.13.18.<br/>부추겉절이5.6.13.<br/>순살바베큐볶음1.2.5.6.10.13.<br/>배추김치9.13.<br/>푸딩1.<br/>무쌈5.6.9.13.<br/>
```

**3. 한달치 급식 저장하기**

`month()` 함수를 사용하면 한달치 급식을 csv나 엑셀 형식으로 저장할 수 있습니다.  
길이가 너무 길어 단순 반환은 불가능합니다.

```python
# 경기과고의 19년 9월자 중식 급식을 csv 형식으로 출력합니다.
m.month("2019", "09", "2", "c")
```

| 매개변수(예시) | 이름     | 설명                                                                                        |
| -------------- | -------- | ------------------------------------------------------------------------------------------- |
| 2019           | 조회년도 | 조회를 원하는 날짜의 년도입니다.<br/>4자리의 문자열 자료형 입니다.                          |
| 09             | 조회월   | 조회를 원하는 날짜의 월입니다.<br/>2자리의 문자열 자료형 입니다.                            |
| 2              | 급식종류 | 조회를 원하는 급식의 종류입니다.<br/>1자리의 문자열 자료형입니다.<br/>부록을 참고해 주세요. |
| c              | 출력종류 | 급식 정보를 저장할 출력 파일의 형식입니다.<br/>엑셀의 경우 `e` CSV의 경우 `c`입니다.        |

위의 매개변수를 각 학교별 사정에 맞추어 바꿔서 작성하여 주십시오.
정상적으로 요청하신 경우 출력종류에 따른 형식으로 급식 정보를 출력합니다.  
또한 다음과 같은 값을 반환합니다.

```
SUCCEED
```

만일 출력에 실패할 경우 아래 에러코드를 반환합니다.  
또한 출력에 성공하여도 출력파일에 에러코드가 반환되는 경우도 있습니다.

**에러코드**

급식을 불러오던 중 문제가 생기면 다음과 같은 에러코드를 반환합니다.

| 에러코드     | 제목                 | 설명                                                                                                   |
| ------------ | -------------------- | ------------------------------------------------------------------------------------------------------ |
| SERVER ERROR | 서버 접속 실패       | 나이스 전산망에 접속하지 못하였습니다.<br/>점검중이거나 교육청 측에서 차단할 경우 발생하는 문제입니다. |
| SIZE ERROR   | 매개변수 길이 에러   | 매개변수로 받은 문자열의 길이가 올바르지 않습니다.<br/>매뉴얼에 따라 입력해 주십시오.                  |
| TYPE ERROR   | 매개변수 자료형 에러 | 매개변수로 받은 내용의 자료형이 올바르지 않습니다.<br/>매뉴얼에 따라 입력해 주십시오.                  |
| NO DATABASE  | 급식 정보 에러       | 조회 결과 급식이 없거나, 예정되지 않은 경우이거나, 조회에 실패한 경우입니다.                           |
| EXCEL ERROR  | 엑셀 변환 에러       | 한달치 급식을 엑셀에 저장하던 중 문제가 발생했습니다.<br/>모듈 상태등을 확인해 주십시오.               |
| CSV ERROR    | CSV 변환 에러        | 한달치 급식을 CSV에 저장하던 중 문제가 발생했습니다.<br/>모듈 상태등을 확인해 주십시오.                |
| OFFICE ERROR | 교육청 / 지역 에러   | 매개변수로 받은 지역이 올바르지 않습니다.<br/>매뉴얼에 따라 입력해 주십시오.                           |

**부록**

- 학교 교급

  | 교급     | 코드 |
  | -------- | ---- |
  | 유치원   | 1    |
  | 초등학교 | 2    |
  | 중학교   | 3    |
  | 고등학교 | 4    |

- 급식 종류

  | 종류 | 코드 |
  | ---- | ---- |
  | 조식 | 1    |
  | 중식 | 2    |
  | 석식 | 3    |

## 라이선스 📜

본 NiPy 모듈의 라이선스는 MIT 라이선스입니다.  
따라서 출처를 표기하시면 본 모듈의 복제, 배포, 활용을 포함한 모든 행위가 허가됩니다.  
자세한 내용은 License 파일을 참고하여 주십시오.

## 도움을 주신 분 🤝

본 NiPy 모듈 제작에 도움을 주신 분들의 목록입니다.  
도움을 주셔서 다시 한번 감사드립니다.

- 모듈 제공

  - [Requests](https://2.python-requests.org/en/master/user/intro/#apache2-license)
  - [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/)
  - [Openpyxl](https://openpyxl.readthedocs.io/en/stable/)

- 아이디어 제공
  - 친구들
  - [M4ndU (급식 조회 로직 아이디어)](https://github.com/M4ndU/school_meal_parser_python)
  - [moseoridve (학교알리미 로직 아이디어)](https://gist.github.com/moseoridev/2ead2abca1af27f489ef0dc6b95c3356)

## 연락처 📞

본 모듈과 관련하여 물어보고 싶으신 점은 다음 연락처로 문의주시기 바랍니다.

- joongi1978@naver.com
