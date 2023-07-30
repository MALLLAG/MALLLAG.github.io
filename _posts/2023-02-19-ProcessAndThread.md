---
title: Process and Thread
tags: OperatingSystem
comments: true
---

# 프로세스 개요

**프로세스**란 실행중인 프로그램을 의미한다. <br>
프로그램은 실행되기 전까지는 보조기억장치에 있는 데이터 덩어리일 뿐이지만, 보조기억 장치에 저장된 프로그램을 메모리에 적재하고 실행하는 순간 그 프로그램은 프로세스가 된다.

프로세스 중에는 사용자가 보는 앞에서 실행되는 **포그라운드 프로세스**와 <br>
사용자가 보지 못하는 뒤 편에서 실행되는 **백그라운드 프로세스**가 존재한다.

<br>

## 프로세스 제어 블록

모든 프로세스는 실행을 위해 CPU가 필요하지만, CPU 자원은 한정되어 있어 모든 프로세스가 동시에 CPU를 사용할 수 없다. <br>
자신의 차례가 되면 정해진 시간만큼 CPU를 이용하고, 인터럽트(타이머 인터럽트)가 발생하면 자신의 차례를 양보하고 다음 차례가 올 때까지 기다린다.

운영체제는 프로세스의 실행 순서를 관리하고, 프로세스에 자원을 배분하기 위해 프로세스 제어 블록 (PCB : Process Control Block)을 이용한다. <br>
PCB는 프로세스와 관련된 정보를 저장하는 자료구조이고, 커널 영역에서 생성된다.

### 프로세스 ID (PID)

PID는 특정 프로세스를 식별하기 위해 부여하는 고유한 번호이다. <br>
같은 일을 수행하는 프로그램이라도 두 번 실행하면 PID가 다른 두 개의 프로세스가 생성된다.

### 레지스터 값

프로세스는 자신의 실행 차례가 돌아오면 이전까지 사용했던 레지스터의 중간값들을 모두 복원한다. <br>
그래야 이전까지 진행했던 작업들을 실행할 수 있다. (PCB 안에 레지스터 값들이 담긴다)

### 프로세스 상태

현재 프로세스가 어떤 상태인지도 PCB에 기록된다.

### CPU 스케줄링 정보

프로세스가 언제, 어떤 순서로 CPU를 할당받을지에 대한 정보도 PCB에 기록된다.

### 메모리 관리 정보

프로세스마다 메모리에 저장된 위치가 달라서, PCB에는 메모리 주소를 알 수 있는 정보가 담긴다.

### 사용한 파일과 입출력장치 목록

프로세스가 실행 과정에서 특정 입출력장치나 파일을 사용하면 PCB에 해당 내용이 명시된다.

<img width="823" alt="22" src="https://github.com/MALLLAG/TIL/assets/87420630/4300a8e2-53b9-4946-9260-b938184c0be9">

<br>

## 문맥 교환

프로세스 실행 순서가 넘어가면 프로세스 수행을 재개하기 위해 필요한 중간 정보가 있는데, 이를 **문맥**이라고 한다. <br>
하나의 프로세스 문맥은 해당 프로세스의 PCB에 표현되어 있다.

<br>

## 프로세스의 메모리 영역

프로세스가 생성되면 커널 영역에는 PCB가 생성되고, 사용자 영역에는 코드 영역, 데이터 영역, 힙 영역, 스택 영역이 생성된다.

### 코드 영역

코드 영역에는 실행할 수 있는 코드(기계어로 이루어진 명령어)가 저장된다. <br>
코드 영역에는 데이터가 아닌 CPU가 실행할 명령어가 담겨 있기 때문에 쓰기가 금지되어 있다.

### 데이터 영역

데이터 영역에는 프로그램이 실행되는 동안 유지할 데이터가 저장된다. (ex. 전역 변수) <br>
코드 영역과 데이터 영역은 크기가 변하지 않아서, **정적 할당 영역**이라고 부르기도 한다.

### 힙 영역

힙 영역은 프로그래머가 직접 할당할 수 있는 저장 공간이다. <br>
프로그래밍 과정에서 힙 영역에 메모리 공간을 할당했다면, 언젠가는 해당 공간을 반환해야 한다.

### 스택 영역

스택 영역은 데이터를 일시적으로 저장하는 공간이다. (ex. 매개 변수, 지역 변수) <br>
일시적으로 저장할 데이터는 스택 영역에 PUSH되고, 더 이상 필요하지 않은 데이터는 POP됨으로써 스택 영역에서 사라진다.

<br>
<hr>

# 프로세스 상태와 계층 구조

## 프로세스 상태

컴퓨터를 사용할 때 여러 프로세스들이 번갈아가며 실행되는데, 그 과정에서 하나의 프로세스는 여러 상태를 거치며 실행된다. <br>
그리고 운영체제는 프로세스의 상태를 PCB를 통해 인식하고 관리한다.

### 생성 상태

프로세스를 생성중인 상태를 **생성 상태**라고 한다. <br>
생성 상태를 거쳐 실행할 준비가 완료된 프로세스는 준비 상태가 되어 CPU의 할당을 기다린다.

### 준비 상태

**준비 상태**는 CPU를 할당받아 실행할 수 있지만, 아직 자신의 차례가 아니라서 기다리고 있는 상태이다.

### 실행 상태

**실행 상태**는 CPU를 할당받아 실행 중인 상태이다. <br>
이때 프로세스가 할당된 시간을 모두 사용한다면(타이머 인터럽트가 발생하면) 다시 준비 상태가 되고 <br>
실행 도중 입출력장치를 사용하여 입출력 장치의 작업이 끝날 때까지 기다려야 한다면 대기 상태가 된다.

### 대기 상태

입출력 작업은 CPU에 비해 처리 속도가 느리기 때문에 입출력 작업을 요청한 프로세스는 <br>
입출력 장치가 입출력을 끝낼때까지(입출력 인터럽트를 받을 때) 기다려야 한다. <br>
이렇게 입출력장치의 작업을 기다리는 상태를 **대기 상태**라고 한다.

### 종료 상태

**종료 상태**는 프로세스가 종료된 상태이다. <br>
프로세스가 종료되면 운영체제는 PCB와 프로세스가 사용한 메모리를 정리한다.

<img width="612" alt="23" src="https://github.com/MALLLAG/TIL/assets/87420630/e2c61c63-2bba-4308-bc17-292bce387392">

<br>

## 프로세스 계층 구조

프로세스는 실행 도중 시스템 호출을 통해 다른 프로세스를 생성할 수 있다. <br>
이때 새 프로세스를 생성한 프로세스를 **부모 프로세스**, 부모 프로세스에 의해 생성된 프로세스를 **자식 프로세스**라고 한다.

자식 프로세스는 실행 과정에서 또 다른 자식 프로세스를 생성할 수 있고, 그 자식 프로세스가 또 다른 자식 프로세스를 생성할 수 있다. <br>
이는 트리 구조를 띄게 되는데 **프로세스 계층 구조**라고 한다.

<br>

## 프로세스 생성 기법

부모 프로세스를 통해 생성된 자식 프로세스들은 **복제와 옷 갈아입기**를 통해 실행된다. <br>
부모 프로세스는 **fork**를 통해 자신의 복사본을 자식 프로세스로 생성하고, <br>
만들어진 복사본은 **exec**를 통해 자신의 메모리 공간을 다른 프로그램으로 교체한다.

<br>
<hr>

# 스레드

**스레드**는 프로세스를 구성하는 실행의 흐름 단위이다. <br>
하나의 프로세스는 여러 개의 스레드를 가질 수 있고, 스레드를 이용해 하나의 프로세스에서 여러 부분을 동시에 실행할 수 있다.

<br>

## 프로세스와 스레드

스레드는 프로세스 내에서 각기 다른 스레드 ID, 프로그램 카운터 값을 비롯한 레지스터 값, 스택으로 구성된다. <br>
각자 이 값들을 가지고 있기에 스레드마다 각기 다른 코드를 실행할 수 있다.

프로세스의 스레드들은 실행에 필요한 최소한의 정보만을 유지한 채 프로세스 자원을 공유하며 실행된다.

<br>

## 멀티 프로세스와 스레드

여러 프로세스를 동시에 실행하는 것을 **멀티 프로세스** <br>
여러 스레드로 프로세스를 동시에 실행하는 것을 **멀티 스레드**라고 한다.

<br>

<img width="521" alt="24" src="https://github.com/MALLLAG/TIL/assets/87420630/933431a7-fde1-4aa1-be08-934a8cfa90a8">

프로세스끼리는 기본적으로 자원을 공유하지 않지만, 스레드끼리는 프로세스 내의 자원을 공유한다.

같은 작업을 하는 동일한 프로세스를 두 개 실행하면 모든 자원이 복제되어 메모리에 적재된다. <br>
PID, 메모리 주소를 제외한 모든 것이 동일한 자원이 복제되어 메모리에 적재되어, 낭비를 하게 된다.

스레드들은 프로세스가 가지고 있는 자원을 공유해, 메모리를 더 효율적으로 사용할 수 있다. <br>
또한 프로세스의 자원을 공유하기 때문에 협력과 통신에 유리하다.

