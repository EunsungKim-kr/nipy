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

### 학교 고유 코드 api (Scode)

아직 지원하지 않는 기능입니다.

### 학교 급식 정보 api (Smeal)

**1. 기본 정보 설정**

우선 학교 기본 정보를 설정하여야 합니다. 기본 설정 예시는 다음과 같습니다.

```python
# 경기과고의 19년 9월 27일자 중식 급식으로 기본 설정합니다.
import nipy
m = nipy.Smeal("goe", "J100000447", "2019", "09", "27", "4", "2")
```

| 매개변수(예시) | 이름        | 설명                                                                                                       |
| -------------- | ----------- | ---------------------------------------------------------------------------------------------------------- |
| goe            | 교육청 코드 | 교육청별 고유 코드입니다.<br/>부록을 참고하시어 작성해 주세요.                                             |
| J100000447     | 학교 코드   | 학교별 고유 코드입니다.                                                                                    |
| 2019           | 조회년도    | 조회를 원하는 년도입니다.<br/>4자리의 문자열 자료형입니다.                                                 |
| 09             | 조회월      | 조회를 원하는 달입니다.<br/>2자리의 문자열 자료형입니다.                                                   |
| 27             | 조회일      | 조회를 원하는 일입니다.<br/>2자리의 문자열 자료형입니다.                                                   |
| 4              | 학교교급    | 학교교급 구분을 위한 매개변수입니다.<br/>1자리의 문자열 자료형입니다.<br/>부록을 참고하시어 작성해 주세요. |
| 2              | 급식 종류   | 조회를 원하는 급식의 종류입니다.<br/>1자리의 문자열 자료형입니다.<br/>부록을 참고하시어 작성해 주세요.     |

위의 매개변수를 각 학교별 사정에 맞추어 바꿔서 작성하여 주십시오.

**2. 하루치 급식 불러오기**

기본 설정이 완료되면 하루치 급식을 불러올 수 있습니다.

```python
# 경기과고의 19년 9월 27일자 중식 급식을 출력합니다.
print(m.day())
```

`day()` 함수를 사용하면 하루치 급식을 반환받을 수 있습니다. 반환되는 데이터는 문자열 자료형이며 예시는 다음과 같습니다.

```
소고기쌀국수5.6.9.13.16.<br/>쌀밥(자율)<br/>열무김치<br/>사과<br/>왕만두찜1.2.5.6.10.13.14.16.18.<br/>양파초절이5.13.<br/>
```

**에러코드**

급식을 불러오던 중 문제가 생기면 다음과 같은 에러코드를 반환합니다.

| 에러코드     | 제목                 | 설명                                                                                                   |
| ------------ | -------------------- | ------------------------------------------------------------------------------------------------------ |
| SERVER ERROR | 서버 접속 실패       | 나이스 전산망에 접속하지 못하였습니다.<br/>점검중이거나 교육청 측에서 차단할 경우 발생하는 문제입니다. |
| SIZE ERROR   | 매개변수 길이 에러   | 매개변수로 받은 문자열의 길이가 올바르지 않습니다.<br/>매뉴얼에 따라 입력해 주십시오.                  |
| TYPE ERROR   | 매개변수 자료형 에러 | 매개변수로 받은 내용의 자료형이 올바르지 않습니다.<br/>매뉴얼에 따라 입력해 주십시오.                  |
| NO DATABASE  | 급식 정보 에러       | 조회 결과 급식이 없거나, 예정되지 않은 경우이거나, 조회에 실패한 경우입니다.                           |

**부록**

- 교육청 코드  
  | 지역명 | 코드 |
  | --- | --- |
  | 서울 | sen |
  | 부산 | pen |
  | 대구 | dge |
  | 인천 | ice |
  | 광주 | gen |
  | 대전 | dje |
  | 울산 | use |
  | 세종 | sje |
  | 경기 | goe |
  | 강원 | kwe |
  | 충북 | cbe |
  | 충남 | cne |
  | 전북 | jbe |
  | 전남 | jne |
  | 경북 | gbe |
  | 경남 | gne |
  | 제주 | jje |

* 학교 교급  
  | 교급 | 코드 |
  | --- | --- |
  | 유치원 | 1 |
  | 초등학교 | 2 |
  | 중학교 | 3 |
  | 고등학교 | 4 |

* 급식 종류  
  | 종류 | 코드 |
  | --- | --- |
  | 조식 | 1 |
  | 중식 | 2 |
  | 석식 | 3 |

## 라이선스 📜

본 NiPy 모듈의 라이선스는 MIT 라이선스입니다.  
따라서 출처를 표기하시면 본 모듈의 복제, 배포, 활용을 포함한 모든 행위가 허가됩니다.  
자세한 내용은 License 파일을 참고하여 주십시오.

## 연락처 📞

본 모듈과 관련하여 물어보고 싶으신 점은 다음 연락처로 문의주시기 바랍니다.

- joongi1978@naver.com
