# chapter02 리눅스 설치

[TOC]

#### 2.1리눅스 설치

##### 2.1.1 리눅스 설치의 개요

운영체제의 사용환경이 텍스트 기반에서 gui 환경으로 전환되고 당양한 용도의 리눅스가 등장하면서 고사양을 요구하는 리눅스도 등장 사용하는 목적에 따라 선택하고 배포되는 리눅스마다 지원되는 아키텍처가 다르기 때문에 시스템에서 사용하는 CPU를 지원하는 리눅스를 선택한다.

##### 2.1.2 리눅스 설치를 위한 하드웨어 정보 파악

cpu, 메모리 ,하드 디스크 등에 대한 정확한 정보는 리눅스 설치와 운영 및 관리에 꼭 필요한 정보이다.

- CPU 
  - 인텔사 :x86, x86_64(Xeon),IA-64(Itanium)
  - 32비트 64비트 cpu 여부에 따라 기본적으로 지원되는 메모리의 양이 다름
  - i7-7500U CPU@ 2.70GHz 2.90GHz / x64 기반 프로세서
- 메모리(RAM) : 하드 디스크 일부 공간을 램처럼 사용하는 스왑파티션 설정과 관련있기때문에 확인 필요
  - 설치된  메모리 : 8.00GB
- 하드 디스크 드라이브
  - 하드디스크 인터페이스에 따라 파일 명이 달라짐.
    - ide :/dev/hda ,/dev/hdb등
    - SCSI,USB메모리,SSD등:/dev/sda,/dev/sdb 등
  - 내장형 SSD :samsung mzvlw256hehp-000
- 모니터와 비디오 어댑터
- 네트워크 인터페이스
  - 네트워크 환경 기반으로 네트워크 인터페이스 설정은 필수
  - 주로 이더넷 사용: 제조사 상관없이 지원
  - 네트워크 설정을 위해서는 IP주소, 넷마스크,게이트웨이 주소, DNS 서버의 IP주소 등을 알아야한다
- 키보드 및 마우스
- CD-ROM 및 DVD-ROM
- 기타 하드웨어

##### 2.1.3 리눅스 설치하기

- VirtualBox 설치 : 리눅스 가상환경 만들기
  - https://www.virtualbox.org/
  - Downloads / Windows hosts
  - 이름에 CentOS-7 로 지정하면 자동으로  종류와버전이 세팅된다. Linux /Red Hat (64-bit)
  - 4096MB (2GB)로 메모리 할당
  - 하드디스크 - '지금 새 가상 하드디스크 만들기' 선택
  - 하드디스크 파일 종류 -VDL선택
  - 물리적 하드드라이브에 저장 - 동적할당
  - 파일 위치및 크기- 30.92GB
  - 설정 / 저장소 / 광학 드라이브 /파일 선택 : CentOS-7-x86_64-DVD-1810.iso
  - 파티션 설정 :마운트지점 '/'= 25GIB(25GB) 마운트지점'swap'=4096MIB(4GB)

#### 2.2 파티션

##### 2.2.1 파티션의 개요

파티션 분할: 하드디스크의 영역 설정, 하나의 물리적 디스크를 여러개의 논리적인 디스크로 분할 하는 것, 분할 된 파티션은 하나의 독립적인 디스크로 간주되어 블록과 파일 시스템 구성 등을 독자적으로 할 수 있으며 , 다양한 정책들도 독립적으로 설정 할 수 있다

- 파티션 분할의 장점
  - 여러개의 운영체제 사용 가능
  - 파티션 단위의 다양한 정책설정 가능(사용자및 그룹쿼터 설정, 보안설정,백업설정, 파일 시스템 점검 설정 )
  - 디스크 효율성 극대화 - 사용자가 원하는 파일 시스템 구성 가능, 블록크기 설정 가능
  - 안정성을 높일수 있음 - 파티션 단위 데이터 복구
  - 자료 이전및 관리,백업 용이
  - 부팅이 빨라짐, 파일 시스템 점검 시간 단축
  - 특정 영역 데이터 증가에 따른 시스템 및 프로세스 중단 방지

##### 2.2.2 디스크와 장치명

|     연결위치     |  파일명  |
| :--------------: | :------: |
|  Primary Master  | /dev/hda |
|  Primary Slave   | /dev/hdb |
| Secondary Master | /dev/hdc |
| Secondary Slave  | /dev/hdd |

별도 : SCSI/SAT-A/SSD/USB메모리등 -  /dev/sd ***x***

##### 2.2.3 파티션의 종류

|    파티션 송류    | 특징                                                         |
| :---------------: | :----------------------------------------------------------- |
| Primary Partition | - 부팅 가능 파티션,디스크에 하나 이상 존재해야함<br />-  하나의 물리적 디스크에 총 4개까지 생성, 파티션 번호로 1~4번이 할당<br />- Extend Partition을 사용할 경우 실질적으로 사용 가능한 Primary Partition은 3개가 됨 |
| Extend Partition  | - 하나의 물리적 디스크에 1개만 생성 가능<br />-  Primary 영역 내에 대체해서 사용하는 것임, 파티션 번호도 1~4로 할당<br />- 자료를 저장하기 위한 파티션 x, Logical Partition을 사용하기위해 선언되는 파티션 |
| Logical Partition | - Extend Partition 안에 선언됨<br />- 생성되는 갯수 제한 x ,12개 이상 생성은 권장하지 않음<br />- Logical Partition은 5번 이후에 번호가 붙여짐 |

##### 2.2.4 파티션과 장치명

- 분할된 파티션은 디스크 장치 파일명 뒤에 숫자가 붙여져 관리된다.
- 일반 IDE 파티션 생성 -  /dev/hda1의 형식 
- SCSI,S-ATA,SSD,USB메모리등 파티션 생성 - /dev/sda1,/dev/sdb1의 형식
- /dev/sda1
  - sd: [디스크 방식] 즉 S-ATA,SCSI방식 디스크,SSD,USB메모리를 뜻함(hd면 IDE or ATA)
  - a: [디스크의 우선순위] 알파벳 a부터 시작하여 표기(a~d)
  - 1: [파티션 번호] 1~4 는 Primary or Extend Partition , 5~ 은 Logical Partition

##### 2.2.5 파티션 분할 

- 리눅스에서는 최소한 /와 swao 파티션을 분할 해야한다.
- root 권한으로 fdisk /dev/[장치명:sda,hda ... ] 
- 파티션 분할이 필요한 영역과 디렉터리
  - / : 설치의 기본이 되는 영역 , 파티션 미분할 시 모든 디렉터리와 프로그램들이 이곳에 설치된다.[최소 파티션 크기 : 250MB]
  - swap : 시스템 자료를 처리할 때 RAM이 부족할 경우 사용되는 스왑 영역,  보통 RAM용량의 2배를 스왑 영역으로 지정
  - /boot : 부팅과 연결된 파일, 부트  로더인 GRUB관련파일, 시스템의 커널 등이 들어있는 디렉터리, /boot를 하드디스크의 앞부분에 할당하면 약간 부팅 속도가 빨라지는 장점이 있으나 체감 속도가 빠르지않아 미설정인 경우가 많다[최소 파티션 크기 : 250MB]
  - /usr : X-Window 를 비롯 리눅스 으용프로그램의 대부분이 이영역에 설치, 최근 레드햇에서는 iSCSI에서 동작 이상과 부트 프로세스의 복잡성등으로 별도 파티션으로 분할 하지 않도록 권장 [최소 파티션 크기 : 250MB]
  - /var : 시스템의 로그파일, 프린터 spool, 메일등이 저장되는 디렉터리, 최근 yum을 사용하는 경우 다운로드한 업데이트 패키지들이 임시로 저장되는 용도로 사용, 충분한 크기로 여유있게 설정해야함[최소 파티션 크기 : 384MB]
  - /home : 계정 사용자의 자료가 저장되는 디렉터리, 다수의 사용자 기반의 서버로 운영되는 경우 할당 필요[최소 파티션 크기 : 100MB]
  - /tmp : 각종 프로그램이나 소켓 파일, 프로세스 작업을 할 때 임시로 생성되는 파일을 저장하는 공간, 모든 접근자가 권한을 가지므로 보안상의 취약점이 있고 보한 강화를 위해 파티션 분할이 요구된다. [최소 파티션 크기 : 50MB]

##### 2.2.6 파티션 확인

- 명령어 : root 권한으로 fdisk -l
- fdisk로 파티션 추가후 재부팅 필요
- 실제 리눅스 상에서 반영되는 파티션 정보 : /proc/partitions 에서 확인

#### 2.3 시스템의 시작과 종료

##### 2.3.1 부트매니저와 GRUB

- 부트매니저 :부팅을 도와주는 역할(부트로더)
- 대표적인 부트 매니저 프로그램 : LILO(Linux Loader)dhk GRUB(Grand Unified BootLoader)
- 특정 파일 시스템에 구애받지 않고 플로피 디스크와 하드 디스크를 이용한 부팅을 지원
-  GRUB
  - GNU 프로젝트에서 만든 부트로더 
  - 다양한 파일 시스템 지원
  - 부팅시 커널 인자를 조정 동적인 부팅 지원
  - 메뉴인터페이스 ,Bash 명령행 인터페이스 제공
  - 그래픽 메뉴 ,배경 그림 삽입 가능
  - GRUB부팅 모드
    - 편집 모드 : 
      - GRUB 목록에서 [e]키 :설정창 오픈
      - 커서로 선택 
      - [ctrl]+[x] : 부팅 시작 
      - [ctrl]+[c] : 관련 설정 직접 입력
      - [ESC] : 초기 GRUB 메뉴로 돌아감
    - 명령 프롬프트 모드 : 
      - GRUB 목록에서 [c]키 : 모드 진입
      - Bash Shell과 유사
      - [TAB] : 명령행 자동완성
      - [ESC] : 취소
      - 부팅 : 순차적 입력후 boot 입력
    - GRUB 환경 설정 파일
      - /boot/grub2/grub.cfg
      - 셀 스크립트 형태
      - 환경 설정파일 변경 후 grub2-mkconfig 명령 실행 필요
      - GRUB 운영과 관련된 주요설정들은 /etc/default/grub파일이다(명령어: cat /etc/default/grub) 
        - GRUB_TIMEOUT=5 - GRUB 부트 화면에서 대기하는 시간(부팅대기시간)
        - GRUB_DISTRIBUTOR =... - GRUB부트 화면에서 각 엔트리 앞에 보여질 리눅스 배포판 이름을 추출할때 사용
        - GRUB_DEFAULT=saved - 부트화면에 제시된 목록 중에 기본적으로 부팅할 모드 선택(정수값) 'saved'는 기본 메뉴 목록에 'GRUB_SAFEDEFAULT' or 'grub-set-defualt'에 의해 저장된다.
        - GRUB_DISABLE_SUBMENU=true - grub-mkconfig 에서 버전 번호가 가장 높은 커널에 대해 최상위 메뉴 항목으로 생성 그외 다른 커널 및 복구모드는 하위 메뉴로 생성됨 true로 설정하면 하위 메뉴를 생성하지 않도록 설정하는 것
        - GRUB_TERMINAL_OUTPUT='console' - GRUB이 출력되는 터미널 장치를 설정하는 항목, 기본이 'console'
        - GRUB_CMDLINE_LINUX ='crashkernel= auto rhgb quiet' -  커널 인자값 지정 항목
        - GRUB_DISABLE_RECOVERTY='true' - 부트 메뉴 엔트리에 복구 모드를 표시할것인지 지정,'true' 일경우 표시 x
      - GRUB의 활용
        - root 패스워드를 잃어버렸을 경우 - 응급 복구 모드로 접근
          - [e] 
          - 커널 인자값으로 커서 이동 
          - 'ro rhgb quite LANG=ko_KR.UTF-8' 을 지우고 'rw init=/bin/sh' 입력
          - [ctrl]+[x] : 부팅
          - 패스워드 변경
        - GRUB 패스워드 설정
          - vi /etc.grub.d/00_header : 파일 오픈
          - 파일수정 마지막 줄에 i나 a로 insert
            - cast <<EOF
            - set superusers='posein'
            - password posein 1234
            - EOF
          - [esc] -> : ->wq ->[enter] - 저장
          - tail -4 /etc/grub.d/00_header :변경 사항 확인
          - grub2-mkconfig -o /boot/grub2/grub.ctg : 명령실행
          - 재부팅 후 편집 모드 [e] 

##### 2.3.2 부팅

- 하드디스크에 설치된 운영체제의 부팅과정

  - 컴퓨터의 전원을 켜면 바이오스(BIOS)는 컴퓨터에 장착된 하드웨어 점검
  - CMOS에 설정된 첫번째 부팅 하드 디스크를 확인
  - 첫번째 하드디스크의 MBR 영역에 있는 부트 매니저 프로그램 실행
  - 부트매니저 프로그램은 관련 설정 파일을 참고해 부팅 시작

- 리눅스 부트 프로세스 변화

  - 리눅스는 SyS V 및 BSD계열 유닉스에서 사용하던 init 프로세스를 사용, 위임하는 방식
  - 전원 -> BIOS(basic input output system)->커널 로드->루트 파일 시스템(/)을 읽기 전용 형태로 마운트,검사 ->쓰기 가능 형태로 마운트->init 프로세스 발생->init 프로세스(리눅스시스템내부의 최초의 프로세스)는 PID-process identity 가 1번이 할당되고 그후 생성되는 프로세스는 모두 fork 방식으로 생성
  - 부팅후 생성되는 프로세스들은 모두 init의 자식형태로 시스템의 종료 및 재부팅에 용의
  - CentOS 7버전은 init 대신 systemd 사용
  - 명령어: pstree | head -20  (프로세스구조 확인 가능)
  - 명령어:ps aux | head

- 로그인과  로그아웃

  - 로그인

    - 사용자의 아이디와 패스워드를 임력함으로써 접근권한과 사용 권한을 획득하는 단계
    - X-Window 기반의 로그인 창은 GUI 이다
    - 로그인 메시지 관련 파일

    | 파일명         | 내용                                                         |
    | -------------- | ------------------------------------------------------------ |
    | /etc/issue     | 사용자가 로그인할떄 'login: '이라는 메시지를 보여주기 전 출력되는 내용이 담김 |
    | /etc/issue.net | /etc/issue와 역할이 같음 로컬과 텔넷을 통한 네트워크 접속의 차이(.net이 네트워크) |
    | /etc/motd      | 'Message Of the Day'의 약어 성공적으로 로그인 되었을떄 접속된 사용자에게 보여주는 메시지를 기록 |

  - 로그아웃
    - 터미널에서 명령어 logout or exit 실행
    - [Ctrl]+[D]
    - 강제적 로그아웃 설정 : /etc/profile 'TMOUT=초'로 지정

##### 2.3.3 Systemd

- Systemd의 개요 

  - 병렬처리
    - 시스템부팅속도 증가
    - 데몬의 On-demand 시작 제공
    - 서비스의 의존성 자동해결
    - 서비스를 시작하기 위해 소켓 및 D-BUS사용
    - Linux cgroups(control groups)를 사용한 프로세스 추적
    - 시스템 상태의 스냅샷및 복원 기능 제공
    - 마운트 및 자동 마운트 지점 유지 
    - 자체적인 로그 관리등의 기능 제공

- Systemd 관련 디렉터리

  | 경로                    | 설명                                                         |
  | ----------------------- | ------------------------------------------------------------ |
  | /etc/systemd/system     | 유닛의 환경 설정 파일이 위치<br />~/.wants : 특정 유닛의 구동에 필요한 유닛들의 설정 파일을 심볼릭링크로 담고있다 |
  | /run/systemd/system     | 런타임 유닛 파일 위치                                        |
  | /usr/lib/systemd/system | 설치 패키지의 유닛파일 위치                                  |
  | /lib/systemd/system     | 시스템에서 사용되는 service 및 target 유닛 파일 위치         |

- systemed의 구조

  - 유닛(unit)

    - systemd의 핵심은 unit(유닛)이라 부르는 일종의 대상(object) 파일이고, 유닛은 service, target, socket, path 등과 같이 다양한 유형(type)을 가진다 

    | 유형    | 설명                                                         |
    | ------- | ------------------------------------------------------------ |
    | service | '.service' 서버에서 제공하는 서비스, 데몬(daemon)이라고 부름 |
    | target  | '.target' 부팅레벨, 특정 동기화 지점과 같이 유닛을 그룹화 하때 사용 |
    | socket  | '.socket' 프로세스 간 통신에 사용되는 IPO(Inter-process communication) 소켓을 의미함 |
    | path    | '.path' 특정 파일 시스템이 변경될떄까지 서비스의 활성화를 지연시킬 떄 사용, 프린팅 시스템의 스풀 디렉터리를 사용하는 서비스에 사용 |

  - 서비스(service)

    - systemctl이라는 하나의 명령으로 제어됨

    - 서비스 관련 정보 상태 : systemctl status 서비스명 으로 확인
      systemctl status sshd.service

      | 상태값          | 설명                                                         |
      | --------------- | ------------------------------------------------------------ |
      | loaded          | 로드되는 유닛의 환경설정파일(/usr/lib/systemd/system/sshd.service) |
      | enabled         | 부팅시 활성화 됨을 나타냄                                    |
      | disabled        | 부팅시 비활성화 됨을 나타냄                                  |
      | active(running) | 프로세스가 하나 또는 그이상의 프로세스에 의해 동작중임을 나타냄 |
      | active(exited)  | 일회성 프로세스를 성공적으로 실행한 경우 나타남              |
      | active(wating)  | 특정이벤트에 의해 대기중인 상태를 나타낸다                   |
      | inactive(dead)  | 프로세스가 종료된 상태를 나타냄                              |
      | static          | 활성화가 되지는 않지만. 활성화되는 다른 유닛에 의해 활성화가 가능한 상태 |

  - 타겟(target)

    - 타겟은 부팅 레벨, 특정 동기화 지졈과 같이 유닛을 그룹화 할 때 사용

    - mansystemd.target 에서 확인

      cd /lib/systemd/system -> ls -l runlevel?.target

      | Target            | 설명                                                         |
      | ----------------- | ------------------------------------------------------------ |
      | poweroff.target   | 시스템을 종료시키는 타겟                                     |
      | rescue.target     | 응급복구모드(init체제의 runlevel 1)로 전환하는 타겟          |
      | emergency.target  | rescue.target과 유사 ,/를 읽기 전용으로 마운트               |
      | multi-user.target | 콘솔모드(init 체제의 runlevel 3)로 전환하는 타겟 텍스트 기반 로그인만 지원 |
      | graphical.target  | X Window(init 체제의 runlevel 5)모드로 전환하는 타겟 ,X 기반의 로그인 지원 |
      | reboot.target     | 재부팅 시키는 타겟                                           |

  - 소켓(socket)

    - man systemd.socket에서 확인

- 관련 명령어

  - systemctl : systemd 기반의 시스템 및 서비스 관리를 제어하는 명령 , 이전버전의 init체계에서 service,chkconfg,init 등의 기능을 합쳐놓은것과 같은 역할을 수행

  - 사용법 :systemctl [option] 명령 [서비스명]

  - 주요 option

    | option      | 설명                                                         |
    | ----------- | ------------------------------------------------------------ |
    | -l, --full  | 유닛 관련 정보를 출력할때<br />긴이름도 약어로 출력하지 않고 전체출력<br />systemctl , systemctl -l |
    | -t, --type= | 유닛의 유형(type)을 지정하는 옵션, '-t help'로 확인          |
    | -a, --all   | 유닛 정보를 출력할 떄 모든 유닛을 지정하는 옵션              |
    | --failed    | 실패한 유닛정보만 출력                                       |

  - 런레벨 관련 주요 명령

    | 명령               | 설명                                                         |
    | ------------------ | ------------------------------------------------------------ |
    | get-default        | 현재시스템에 설정된 런레벨 target 정보를 출력                |
    | set-default 타겟명 | 시스템의 런레벨을 지정한 target으로 변경<br />systemctl set-default multi-user.target |
    | isolate 타겟명     | 지정한 타겟의 런레벨로 '즉시' 변경<br />systemctl isolate runlevel3.target |
    | rescue             | 응급 복구 모드로 즉시 전환'emergency'와 유사<br />systemctl rescue |
    | poweroff           | 시스템을 즉시 종료.'halt'와 동일<br />systemctl poweroff     |
    | reboot             | 시스템을 즉시 재부팅'kexec'<br />systemctl reboot            |

    

  - 상태 정보 관련 주요명령

    | 명령              | 설명                                                         |
    | ----------------- | ------------------------------------------------------------ |
    | list-units        | 유닛 관련 정보를 출력 아무 옵션 없이 systemedctl명령으로도 호출<br />systemctl list-units --type=service :서비스 관련 정보만 출력<br />systemctl list-units --type=service --all :모든 서비스 관련 정보 출력 활성화 하지 못한 유닛 관련 정보도 확인 가능 |
    | list-unit-files   | 설치된 유닛 파일의 목록 및 상태 정보를 출력<br />systemctl list-unit-files |
    | list-sockets      | 소켓 관련 유닛의 정보를 출력<br />systemctl list-sockets     |
    | list-dependencies | 명시된 유닛의 의존성 관련 있는 유닛 정보 출력,명시된 유닛이 없을 경우 default.target의 의존성 정보를 출력<br />systemctl list-dependencies sshd.service |

    

  - 서비스 제어관련 주요 명령

    | 명령                | 설명                                                         |
    | ------------------- | ------------------------------------------------------------ |
    | enable 서비스명     | 부팅시에 특정 서비스 구동<br />systemctl enable sshd.service |
    | disable 서비스명    | 부팅시 특정 서비스 구동 x<br />systemctl disable sshd.service |
    | is-enabled 서비스명 | 부팅시에 특정 서비스가 구동되는지 여부확인, <br />구동되면 enable,아니면 disable<br />systemctl is-enabled sshd.service |
    | start 서비스명      | 특정 서비스 즉시 실행<br />systemctl start sshd.service      |
    | stop 서비스명       | 특정 서비스 종료<br />systemctl stop sshd.service            |
    | restart 서비스명    | 특정 서비스 재시작<br />systemctl restart sshd.service       |
    | reload 서비스명     | 특정 서비스의 환경 설정만 다시 읽어 들임<br />               |
    | mask 서비스명       | 특정 서비스의 유닛 파일을 /dev/null로 링크시켜서 시작되는것을 막을때 사용 |
    | unmask 서비스명     | mask 설정된 서비스 해제                                      |
    | is-active 데몬명    | 특정 데몬이 활성화 되어 있는지 여부 확인. active/inactive<br />systemctl is-active sshd |
    | status 데몬명       | 특정 데몬에 대한 상태정보 출력                               |
    | kill 데몬명         | 특정 데몬의 프로세스 종료                                    |
    | daemon-reload       | systemd 매니저 관련 환경 설정을 다시 읽어 들임<br />systemctl daemon-reload |

  - systemd-analyze

    - 시스템 부팅과 관련된 성능을 분석해주는 명령, 부팅에 걸린 시간을 알 수 있다.

    - 사용법 : systemd-analyze [argument]

      | 인자값         | 설명                                                         |
      | -------------- | ------------------------------------------------------------ |
      | time           | 부팅시 소요되는 시간정보 출력, 커널, 램디스크. 서비스영역 3가지 정보출력 <br />systemd-a |
      | blame          | 서비스별 부팅 시에 소요된 시간 출력 <br />systemd-analyze blame |
      | critical-chain | 각 유닛의 시간을 트리 형태로 출력 <br />@문자 ~ - 유닛이시작 또는 활성화 되기까지 소요 시간<br />+문자 ~ - 유닛을 시작하는데 소요되는 시간 <br />systemd-analyze critical-chain |
      | plot           | 관련 정보를 SVG(Scalable Vector Graphic) 이미지 파일로 생성<br />systemd-analyze plot > systemd.svg |

- 로그관리

  - 개요 : systemd 관련 로그는 systemd-journald가 생성 관리한다

    - 로그인 관련 정보 - 커널로 부터
    - 사용자 프로세스 관련 정보 - syslog로 부터
    - 메타데이터로 /run/log/journal  디렉터리에 저장 재부팅시 관련 정보 사라짐

  - 관련 명령어:journalctl

    - systemd-journald에 의해 생성된 정보를 질의할때 사용하는 명령어

    - 사용법 : journalctl [option] [항목]

    - 주요 옵션

      | 옵션           | 설명                                                         |
      | -------------- | ------------------------------------------------------------ |
      | -l ,--full     | 출력 가능한 모든 필드의 정보를 출력                          |
      | -r, --reverse  | 역순 출력 가장 최신의 것을 상단으로                          |
      | -p,--priority= | syslog에 사용하는 로그레벨 지정옵션, 레벨명이나 숫자값을 적으면 되고 지정한 레벨 이상의 정보를 출력<br />높은 순 정리 :emerg(0),alert(1),crit(2),err(3),warning(4),notice(5),info(6),debug(7)<br />journalctl -p err |
      | --since=       | 특정 날짜 이후의 정보만 출력 <br />formmat : "yyyy-MM-DD hh:mm:ss"<br />journalctl --since =2020-05-05 |
      | --until=       | 특정 날짜 까지의 정보만 출력<br />formmat : "yyyy-MM-DD hh:mm:ss"<br />journalctl --until=2020-05-05 |

    - 로그관리

      - /run/log/journal은 휘발성 정보 
      - /var/log 디렉터리 내에 journal 디렉터리를 생성하고 관련 명령을 실행해야 지속관리 가능
      - 로그파일의 환경 설정 : etc/systemd/journald.conf 에서 제어
      - 관련 정보 확인 :man journald.config

- 시스템 설정 주요 명령어

  - timedatectl

    - 시스템의 날짜 및 시간을 확인하거나 설정하는 명령

    - 사용법 : timedatectl [command]

    - 주요커멘드

      | command      | 설명                                                         |
      | ------------ | ------------------------------------------------------------ |
      | status       | 시스템 시간 및 RTC(real time clock)의 시간 정보 출력         |
      | set-time     | 시스템 시간의 설정 명령<br />formmat : "yyyy-MM-DD hh:mm:ss" |
      | set-timezone | 타임존 설정 명령 <br />우리나라 : 'Asia/Seoul'<br />timedatectl set-timezone Asia/seoul |
      | set-ntp      | NTP사용여부 지정명령 1로 설정하면 사용, 0 은 미사용          |

  - hostnamectl

    - 시스템에 설정된 호스트명 정보 출력 및 설정

    - 사용법 :  hostnamectl [설정값]

    - 주요 command

      | command      | 설명                                            |
      | ------------ | ----------------------------------------------- |
      | status       | 정보 출력                                       |
      | set-hostname | 호스트명 설정<br />hostnamectl set-hostname www |

##### 2.3.4 시스템 종료(ShutDown)

- 셧다운(ShutDown)의 개요 : 시스템의 전원을 끄거나 종료하는 행위

  - x window 환경 - [끄기]메뉴
  - termianl 환경 - shutdown .halt, reboot, poweroff,systemctl 등의 명령어를 이용

- shutdown

  - 시스템 재시작이나 전원을 종료하는 명령은 root 관리자만 가능

  - 사용법 : shutdown [option] 시간 [경고메세지]:시간은 +m 형식으로 사용 가능 m분후 종료

  - 주요 옵션

    | 옵션 | 의미                                                         |
    | ---- | ------------------------------------------------------------ |
    | -r   | 재부팅<br />shutdown -r now                                  |
    | -h   | 종료(halt) <br />shutdown -h now<br />shutdown -h +10        |
    | -c   | 예약 셧다운 명령 취소<br />shutdown -c                       |
    | -k   | 실제로 셧다운 하지않고 경고 메시지만 접속한 사용자들에게 전송 |

- reboot

  - 시스템 재시작 명령어

  - 사용법 : reboot [option] ,옵션없으면 즉시 재부팅

  - 주요 옵션

    | 옵션 | 의미                                                         |
    | ---- | ------------------------------------------------------------ |
    | -w   | 시스템을 재부팅 하지 않고 /var/log/wtmp에 셧다운한 기록만 저장 |
    | -f   | init을 호출하지 않고 즉시 시스템 재부팅                      |

- halt

  - 시스템을 종료하는 명령어

  - 사용법 : halt [option]

  - 주요옵션

    | 옵션 | 의미                                          |
    | ---- | --------------------------------------------- |
    | -p   | 시스템 종료하고 전원까지 끄는경우(--poweroff) |

- poweroff

  - 시스템 종료및 전원 끄기 명령
  - 사용법 : poweroff

- init, telinit

  - 조상 프로세스 init 프로세스에 직접 요청 실행레벨 변경 , 빠르게 실행되지만 실행중인 프로세스 무조건 종료임으로 권장 x

  - 사용법 : init 실행레벨 

  - init 0 :시스템 즉시종료

  - init 6 : 시스템 즉시 재부팅

  - init 1 : 시스템을 즉시 단일 사용자 모드로 전환

    