# chapter02 사용자 생성 및 계정관리

[TOC]

#### 2.1 사용자 관리

##### 2.1.1 사용자(User)의 개요

- 사용자(User)분류 

  - 정수형 숫자 형태의 UID(User Identity)로 관리  

  - root -  Super User or Privileged User : 모든 권한을 가짐 (UID 0)
  - 일반 - Normal user or Unprivileged user : 제한적 권한을 가짐 ( UID 1~ :: 레드헷 계열은 일반적으로 1000~) , 로그인 가능 계정, 시스템 계정

- 시스템 계정

  - 시스템의 필요에 의해 생성된 계정

##### 2.1.2 사용자 생성 명령어

- 사용자 계정 생성: useradd

  계정: 시스템에 ID PW 생성 사용권을 부여하는 것, 이때 사용자의 ID를 생성하는 명령이 useradd, root 권한자가 root 이외 사용자를 생성할때도 사용하는 명령어

  - 사용법 :  useradd [option] 사용자 계정이름
  - 전체 목록에서 user 목록 찾기 : cat /etc/passwd or cut -f1 -d: /etc/passwd
  - bash 목록에서 생성된 user  확인 명령어 :  grep /bin/bash /etc/passwd | cut -f1 -d:

##### 2.1.3 사용자 관련 파일

##### 2.1.4 사용자 계정 관리 및 삭제

##### 2.1.5 사용자 패스워드 관리

#### 2.2 그룹관리

##### 2.2.1 그룹의 개요

##### 2.2.2 그룹(Group)의 조회

##### 2.2.3 그룹 관리 명령어

#### 2.3 사용자 조회 및 기타 명령어

##### 2.3.1 사용자 조회 명령어

##### 2.3.2 사용자 간 메시지 전송 명령어

##### 2.3.3 기타명령어



