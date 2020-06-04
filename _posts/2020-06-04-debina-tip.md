---
title: "debian tip"
excerpt: "linux tip"
toc: true
toc_sticky: true
categories: linux

tags: linux, debian

last_modified_at: 2020-06-04
---
# 데비안(debian) gnome-desktop 팁

## 데비안 설치 전 알아야 할 사항
 * 한국에서는 우분투 사용률이 높아서 데비안에대한 정보가 부족
 * 최신 기술의 하드웨어 일수록 지원 안할 가능성이 높음
 * 우분투와는 비슷하지만 조금 다름
 프로그램을 새로 설치 전 데비안 스타일 설치 검색이 필요함. 의존성 관련 패키지를 통합관리 하는 데비안은 우분투처럼 최신 버전의 패키지를 유지하지 않아 패키지 의존성이 꼬일 가능성이 있음. 특히 정식버전인 stable의 경우 보수적 패키지라 없거나 오래된 버전의 패키지가 많음. 최신버전에 가까운 패키지를 쓰려면 sid 나 test 버전을 사용해야함.

## 설치 전 라이브 부팅
* 설치 시디 선택시 라이브 시디를 선택해서 라이브 모드로 부팅을 해보는 것이 좋음.
* 와이파이 그래픽카드 등 하드웨어적인 문제를 알아서 처리해줌. 
* 라이브 부팅으로 컴퓨터에 필요한 작업을 미리 확인해 볼 수 있음

## 데비안에서 한글 입력
* 설치 단계에서 기본으로 ibus가 설치되어있으나 한글 입력이 안됨
    - 설정 -> 지역 및 언어 -> 입력 소스 에서 한국어(hangul) 을 추가 첫번째 입력소스로 선택
    - 한글이 없으면 ibus-hangul 을 설치
    ```shell
     $ sudo apt install ibus-hangul
    ```
    - 화면 우측 상단 와이파이 아이콘 옆 en 클릭 후 "korea(hangul)" 선택
    - 단축키(shift + space)등으로 설정 후 한영 전환이 가능하다.

## 설치 후

### home 디렉토리들의 한글명을 영어로 전환 방법
```shell
    $lang=C
    $xdg-user-dirs-gdk-update
```

### 초기 상태 백업
* timeshift 설치 후 상태 저장하면 에러 및 꼬인 상태를 쉽게 되돌릴 수 있음.(강추)

### 멀티제스쳐 touchpad 설정
[fusuma 사이트](https://github.com/iberianpig/fusuma)
- xdotool은 wayland,x11,xorg 중 지원이 안될 수 있음
- 일부 설정은 플러그인을 설치해야 함

### 네이버 d2coding font 사용
```shell
 $ apt install fonts-naver-d2coding
```

### 윈도우 글꼴 사용하기
윈도우 폰트 폴더에서 필요한 폰트를 복사
```shell
sudo cp *.* /usr/share/fonts 
sudo fc-cache -fc  
```
super + a(모든프로그램보기) -> 기능개선(tweaks) -> 글꼴(font) -> 해당폰트 선택

### chrom 설치
chromium 이라는 크롬과 같은 프로그램을 제공함
```shell
 # apt install chromium
```
구글 계정 싱크를 하려면<br> chromium setting -> advanced - Privacy and security - Allow Chromium sign-in 변경

### vscode 설치
[vscode install 안내](https://linuxize.com/post/how-to-install-visual-studio-code-on-debian-10/)

### docker 설치
[docker install 안내](https://docs.docker.com/engine/install/debian/
)

#### residual config 삭제
- 필요없는 프로그램의 설정파일을 다 지움
```shell
apt purge $(dpkg -l | grep '^rc' | awk '{print $2}')
```

#### bash 단축키
ctrl + r : 히스토리 찾기

#### 파일 찾기
```shell
$ find / -name 파일명
```

#### grub 설정 변경
```shell
$ cat /usr/sbin/update-grub | grep grub-mkconfig
$ exec /usr/sbin/grub-mkconfig -o /boot/grub/grub.cfg "$@"
```

#### 터미널 환경에서 유용하게 쓰이는 mc
- ctrl + o : 평소 화면을 볼 수 있다. 한번 더 누르면 mc로 돌아온다.

#### godoc 사용위해 apt-get install golang-golang-x-tools
 
#### debian 패키지들은 파일 위치가 기본적으로 다른 리눅스와 다름 항상 확인 필요함