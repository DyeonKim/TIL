# Jenkins + Docker를 활용한 CICD 구축

⭐ 목차 ⭐
1. [CICD란?](#cicd란)
2. [Docker란?](#docker란)
3. [Jenkins란?](#jenkins란)
4. [Docker로 Jenkins를 설치하고 설정](#docker로-jenkins를-설치하고-설정)
5. [GitLab과 Jenkins를 연동](#gitlab과-jenkins를-연동)
6. [웹서버(Nginx) 설치 후 설정을 하고 어플리케이션을 배포](#웹서버nginx-설치-후-설정을-하고-어플리케이션을-배포)

<br/><br/>

## CICD란?
![CICD](https://user-images.githubusercontent.com/45352173/152572489-36576f96-8ef6-420c-ae2b-3412fccf8c45.png)

CI
- ***Continuous Integration*** : 지속적인 통합.

CD
- ***Continuous Delivery*** : 지속적인 서비스제공
- ***Continuous Deploy*** : 지속적인 배포

<br/>

애플리케이션 개발 단계를 자동화하여 애플리케이션 개발을 보다 짧은 주기로 고객에게 제공하는 방법.

새로운 코드 통합으로 인해 개발 및 운영팀에서 발생하는 문제, 일명 통합지옥(*Integration hell*)을 해결하는 솔루션

CI/CD는 애플리케이션 통합, 테스트, 제공, 배포에 이르는 라이프사이클 전체에 걸쳐서 지속적인 자동화와 모니터링을 제공하며, 이러한 구축사례를 CI/CD 파이프라인이라 부른다.

![cicd pipeline](https://user-images.githubusercontent.com/45352173/152574215-e81c359c-3ca9-43fa-ad4c-e00d67d87b86.png)

<br/><br/>

## Docker란?

<br/>

## Jenkins란?
![Jenkins](https://user-images.githubusercontent.com/45352173/152574709-88401df8-cee0-4517-ba16-2bca4556e0e6.png)

- CI/CD를 도와주는 툴로 가장 널리 쓰인다.
- Jenkins는 기본적으로 java runtime 위에서 동작하는 자동화 서버이다. build, test, deployment의 모든 것을 자동화해준다.
- Jenkins에는 다양한 플러그인들이 존재하는데, 이미 만들어져있는 플러그인들을 사용하거나 아니면 직접 만들어서 각종 작업들을 자동화할 수 있다.
  - 대표적인 플러그인으로는 Credentials Plugin, Git Plugin, Pipleline 등이 있다

<br/>

## Docker로 Jenkins를 설치하고 설정

<br/>

## GitLab과 Jenkins를 연동

<br/>

## 웹서버(Nginx) 설치 후 설정을 하고 어플리케이션을 배포

<br/>
