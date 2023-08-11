---
title: Collections Framework
tags: Java
comments: true
---

# Collections Framework란

자바에서 데이터 관리를 편리하게 처리할 수 있도록 자료구조와 알고리즘을 구조화하여 표준화된 방법을 제공하는 클래스들을 구현한 것. <br>
사용자들은 Collections Framework의 클래스들을 통해 상황에 맞는 자료구조를 선택하고 데이터를 쉽게 조작할 수 있다.

Collections Framework의 대표적인 인터페이스는 다음과 같다

- List Interface
- Set Interface
- Map Interface

<br>
<hr>

# List

|인터페이스|구현체|설명|
|---|---|---|
|List|ArrayList|순서가 존재하며 중복을 허용하는 선형 구조의 데이터 집합|
|...|LinkedList|...|
|...|Vector|...|

## ArrayList

일반적인 배열은 생성 후 요소를 삽입하는 과정에서 배열이 가득 찬 상황에 배열의 크기가 변하지 않지만, ArrayList는 가변적인 크기를 가진다. <br>
ArrayList의 크기에 상관없이 저장 용량이 가득 찬 상황에서 요소들이 삽입될 수 있도록 크기를 재조정한다.

## LinkedList

양방향으로 삽입과 삭제가 이루어질 수 있는 이중 연결 리스트 구조이다. <br>
LinkedList는 연결 리스트의 장점을 가지므로 삽입, 삭제시에 ArrayList보다 빠르지만, 인덱스 기반이 아니므로 검색 시에는 모든 노드를 순회해야 하므로 ArrayList보다 성능이 낮다.

## Vector

ArrayList와 내부적으로 동일한 구조를 가지지만 차별성으로 동기화(synchronized)를 지원한다. <br>
멀티 스레드 환경에서 Vector 클래스로 선언된 객체는 thread-safe를 보장하지만, 하나의 스레드로만 연산하므로 속도가 떨어진다.

<br>
<hr>

# Map

|인터페이스|구현체|설명|
|---|---|---|
|Map|HashMap|순서를 보장하지 않으며 key-value의 한 쌍으로 이루어진 자료구조. key의 중복을 허용하지 않는다.|
|...|HashTable|...|
|...|TreeMap|...|
|...|...|...|

## HashMap

해싱 기법으로 데이터를 찾기 때문에 검색에 유리하지만 동기화는 지원되지 않는다. <br>
key와 value에 null을 저장할 수 있다.

## HashTable

HashMap과 달리 동기화를 지원한다.

## TreeMap

데이터 삽입 시 내부적으로 정렬을 지원한다. <br>
key를 기준으로 정렬을 수행하기 때문에 key에 null을 저장할 수 없다. 동기화는 지원되지 않는다.

<br>
<hr>

# Set

|인터페이스|구현체|설명|
|---|---|---|
|Set|HashSet|중복과 순서를 보장하지 않는 자료구조.|
|...|TreeSet|...|
|...|LinkedHashSet|...|
|...|...|...|

## HashSet

중복을 허용하지 않고 순서에 관계없이 데이터가 삽입된다.

## TreeSet

삽입된 데이터는 오름차순으로 정렬된다. <br>
중복을 허용하지 않고 정렬이 필요한 데이터 집합이 필요한 경우 사용한다.

## LinkedHashSet

HashSet과 다른 점은 데이터가 삽입된 순서대로 데이터가 저장된다.


