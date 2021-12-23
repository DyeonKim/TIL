# 테스트 케이스의 기본
- 테스트 케이스는 컨디션을 체크하기 위함임

### 테스트 케이스 vs 체크리스트
|       | 체크리스트 | 테스트 케이스 |
| :----: | :------------ | :--------------- |
| 개념 | 단순한 현상을 체크<br/>조건이 없음 | Condition = ~ 면(if)... |
| 예시 | 로그인하면 좌측 상단에<br/> 해당 로고가 표시된다.  | 일반회원으로 로그인하면 메인 하단부에 아무것도 안보이지만<br/>프리미어 회원으로 로그인하면 하단부에 프리미어 배지가 보인다. |

<br/><br/>

### 테스트 케이스 종류
 - 단위 테스트
 - 통합 테스트
 - 시스템 테스트

<br/><br/>

## 테스트 베이시스(Test Basis)
 :  테스트 케이스를 만들기 위한 재료/근거(데이터)

### 명세 기반 베이시스
 - 문장(text)로 이루어진 내용
 - Ex) 기능 설명서, 사용자 스토리

### 구조기반 베이시스
 - 코드, 제어 흐름도 등의 구조적 데이터로 이루어진 내용
 - Ex) 단위 코드, 제어 흐름도

<br/><br/>

## 베이시스에 따른 케이스 분석법
### 제어 흐름도
프로그램에서 실행되는 각 구문, 명령어나 함수가 호출되는 순서를 의미<br/>
제어문 : 주어진 조건의 결과값에 따라서 프로그램의 수행 순서를 제어하거나 문장들의 수행 횟수를 조정하는 문장

<img width="50%" src="https://user-images.githubusercontent.com/45352173/147180414-31200e73-88fd-414b-b3a9-a68e55acffcd.png" />

<br/><br/>

**일반적 기호**[(위키백과)](https://ko.wikipedia.org/w/index.php?title=%EC%88%9C%EC%84%9C%EB%8F%84&action=edit&section=2)

<img width="80%" src="https://user-images.githubusercontent.com/45352173/147196919-d1ed99f7-ee66-4597-b72e-aaf2cd68fc15.jpg"/>
<br />

**기타 기호**[(위키백과)](https://ko.wikipedia.org/w/index.php?title=%EC%88%9C%EC%84%9C%EB%8F%84&action=edit&section=2)

<img width="80%" src="https://user-images.githubusercontent.com/45352173/147197196-bba5d74c-9412-4912-a871-d4994634945c.jpg"/>
<br/><br/>

### (의사)결정테이블
논리적인 조건이나 상황(Conditions)을 구현하는 시스템 요구사항을 도출하거나 내부시스템 디자인을 문서화하는 매우 유용한 도구

<img width="50%" src="https://user-images.githubusercontent.com/45352173/147177394-2a3106ce-24de-4e9b-8f33-d0baf0797426.png" />
<br/><br/>

# 실제 최종 케이스

<img width="50%" src="https://user-images.githubusercontent.com/45352173/147178835-e4aae693-aec9-4f43-98c5-b97ee2a92167.png" />
