# Docker를 Windows10에 설치하기

Docker를 Windows10에 설치해보자.

<br/>

## 0. 들어가기 전에

### 0-1. WSL2 란?
[2020년 5월 Windows 10 May 202 Update(20H1) 업데이트](https://blogs.windows.com/windowsexperience/2020/05/27/whats-new-in-the-windows-10-may-2020-update/)

윈도우에서 리눅스를 사용할 수 있게 해주는 WSL2 버전이 정식으로 릴리스 되었다.
> WSL2 : Windows Subsystem for Linux 2

단순히 가상머신으로 리눅스를 사용할 수 있는 것이 아니라, 윈도우 시스템과 통합되어 마치 하나의 머신처럼 자연스럽게 리눅스를 활용하는 것이 가능하다.

<br/>
 
#### 📌 Windows 10에 WSL2의 리눅스 커널 설치 가능한 지 확인
`Windows + S` 클릭하고 PC 정보(설정)을 검색하여 실행.

<img width="80%" alt="PC 정보 설정 검색" src="https://user-images.githubusercontent.com/45352173/152536048-c4a36ba0-757f-4e64-8637-c8931cc5f538.png" />
<br/>

버전이 20H1, 20H2, 21H1 혹은 그보다 높은 버전인지 확인
> 이보다 낮은 버전이면 Windows Update 설정을 열어 최신 버전으로 업데이트

<img width="80%" alt="Windows 사양에서 현재 버전 확인" src="https://user-images.githubusercontent.com/45352173/152536753-f3d4ac1f-78c3-455f-baf5-38af9c4c78c0.png" />

<br/>

### 📌 WSL2를 설치하고 활성화하는 방법
`Windows + S` 클릭하고 "Windows PowerShell" 검색하여 '관리자 권한'으로 실행.
> Windows PowerShell은 윈도우 환경에서 리눅스 명령어를 사용할 수 있다.

DISM(배포 이미지 서비스 및 관리) 명령어로 Microsoft-Windows-Subsystem-Linux 기능을 활성화
- Linux용 Windows 하위 시스템 사용
``` Bash
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```
- Virtual Machine 기능 사용
```Bash
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```
두 명령어 모두 ‘작업을 완료했습니다’ 출력으로 종료되었는지 확인

<details>
  <summary>GUI 방식으로 해결하는 방법</summary>
  
  <img width="80%" src="https://user-images.githubusercontent.com/45352173/152560357-826da6f3-59ee-47ff-a7c1-193b067769bd.png" />
  <img width="80%" src="https://user-images.githubusercontent.com/45352173/152560633-a92d7e49-71fa-4157-94cb-5382105380cf.png" />
  
</details>

윈도우를 재부팅

[x64 머신용 최신 WSL2 Linux 커널 업데이트 패키지](https://aka.ms/wsl2kernel)를 다운로드 받아 안내에 따라 설치

Windows PowerShell을 열고 다음 명령어를 실행
``` Bash
wsl --set-default-version 2
```


<br/><br/>

### 0-2. Hyper-V 가상화 기능 활성화
Hyver-V : Windows 10에서 가상 컴퓨터를 만들 수 있도록 해준다.
> Hyper-V는 Windows에서 선택적 기능으로 기본 제공되므로 Hyper-V를 다운로드할 필요가 없다.
> Hyper-V는 Windows 10 Home에는 설치할 수 없습니다.

<br/>

**요구사항**
- Windows 10 Enterprise, Pro 또는 Education
- 두 번째 수준 주소 변환(SLAT)을 사용하는 64비트 프로세서.
- VM 모니터 모드 확장(Intel CPU의 VT-c)에 대한 CPU 지원.
- 최소 4GB의 메모리.

> 자세한 사항 확인은 [여기서➡](https://docs.microsoft.com/ko-kr/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)

<br/><br/>

Docker Desktop은 기본적으로 Hyper-V 기능을 사용하기 때문에 Windows 10 Enterprise, Pro 또는 Education 에디션에서만 사용할 수 있었다.<br/>
Home 에디션에서는 Docker Toolbox(boot2docker)가 대안으로 이야기되곤 했었다만, 현재는 공식적으로 지원이 종료된 상태이다.<br/>
그러나 Docker Desktop의 발빠른 지원으로 현재는 WSL2를 기반으로 Docker Desktop을 사용하는 것이 가능하다.

<br/>

📌 정리
- Windows 10 Enterprise, Pro 또는 Education 에디션
  - WSL2 기반 Docker Engine 사용 가능
  - Hyper-V 기반 Docker Engine 사용 가능
- Windows 10 Home 에디션
  - WSL2 기반 Docker Engine 사용 가능

<br/>

<details>
  <summary>Windows 10 Enterprise, Pro 또는 Education 에서 Hyper-V 활성화</summary>
  
  `작업관리자` > `성능` 에서 가상화가 `사용`인지 체크
  
  <img width="50%" alt="작업관리자에서 가상화 체크" src="https://user-images.githubusercontent.com/45352173/152539334-c70a9d4e-e9e5-4505-90f6-fee944479210.png" />
  <br/>
  
  `제어판` > `프로그램` > `프로그램 및 기능` 에서 왼쪽의 `🛡️Windows 기능 켜기/끄기` 클릭<br/>
  Hyper-V가 체크✅되어 있는 지 확인!<br/>
  만약 체크되어 있지 않다면 체크 후 확인을 눌러준다.<br/>
  
  <img width="50%" alt="Hyper-V 활성화" src="https://user-images.githubusercontent.com/45352173/152544149-ccd66ce7-bdb6-4336-a85c-99d2e7aebf69.png" />
  
  위의 설정 확인 후 재설치 후 재부팅
</details>


## 1. [hub.docker.com](https://hub.docker.com) 계정 등록
Windows 환경에서는 hub.docker.com의 계정이 없이는 Docker Hub의 컨테이너를 사용할 수 없다.<br/>
따라서 계정 생성을 먼저 해주자.

<br/>

## 2. Windows Docker 설치
[Docker Desktop for Windows](https://docs.docker.com/desktop/windows/install/) 에서 응용 프로그램 다운로드⬇

`Docker Desktop Installer` 실행

<img width="50%" alt="설치 환경설정" src="https://user-images.githubusercontent.com/45352173/152546058-35f847b1-30fb-46f8-a690-886181f0011e.png" />

> Windows 10 Enterprise, Pro 또는 Education에서는 목록에 `Enable Hyper-V Windows Feature`이 추가됨.

설치 후 `Close and Restart` 클릭하여 재부팅

<br/><br/>

## 3. 리부팅, 그리고 WSL2 설치
만약 x64 머신용 WSL2 Linux 커널이 최신으로 업데이트 되어 있지 않다면 리부팅 후에 다이알로그 창이 뜬다.
<img width="80%" src="https://user-images.githubusercontent.com/45352173/152554803-dbb1c4bb-90de-4690-af37-712ad40768c0.png" />
> Kernel update를 먼저 해야하기 때문에 WSL2가 불완전하게 설치되었다는 안내.


이 경우 [x64 머신용 최신 WSL2 Linux 커널 업데이트 패키지](https://aka.ms/wsl2kernel)를 다운로드 받아 안내에 따라 설치해주면 된다.

## 4. 실행
<img width="80%" alt="Docker Desktop" src="https://user-images.githubusercontent.com/45352173/152578934-4becc623-e8a1-48e3-a68c-0fbf60e3c92a.png" />

``` Bash
PS C:\Users\[user폴더]> docker --version
PS C:\Users\[user폴더]> Docker version 20.10.12, build e91ed57
```
무사히 실행되는 걸 확인할 수 있다.

Windows 환경에서는 hub.docker.com의 계정 로그인을 해줘야 한다.

``` Bash
PS C:\Users\[user폴더]> docker login
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: [유저명]
Password: [비밀번호]
Login Succeeded

Logging in with your password grants your terminal complete access to your account.
For better security, log in with a limited-privilege personal access token. Learn more at https://docs.docker.com/go/access-tokens/
```

이제 image를 pull 받거나 컨테이너를 run할 수 있다.
