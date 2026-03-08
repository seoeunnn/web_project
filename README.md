# 🛡️Spring Boot 게시판 웹 취약점 분석 프로젝트

## 목차

- [1. 프로젝트 소개](#1-프로젝트-소개)
- [2. 기술 스택](#2-기술-스택)
- [3. 프로젝트 설치 및 실행 방법](#3-프로젝트-설치-및-실행-방법)
- [4. 프로젝트 구조](#4-프로젝트-구조)
- [5. 분석 대상 기능](#5-분석-대상-기능)
- [6. 분석 예정 취약점](#6-분석-예정-취약점)
- [7. 프로젝트 진행 계획](#7-프로젝트-진행-계획)

<br>

## 1. 프로젝트 소개

본 프로젝트는 **Spring Boot 기반 게시판 서비스를 대상으로 웹 취약점 분석을 진행하는 보안 실습 프로젝트**입니다.

GitHub에 공개된 Spring Boot 게시판 프로젝트를 기반으로 환경을 구축한 뒤,  
실제 웹 서비스 환경과 유사한 구조에서 다음 과정을 수행합니다.

- 취약점 분석
- 공격 재현
- Secure Coding을 통한 보완

이를 통해 **웹 애플리케이션 보안과 취약점 분석 과정에 대한 이해를 높이는 것**을 목표로 합니다.

### 🔗 Original Repository
https://github.com/hojunnnnn/board

해당 프로젝트는 **Fork하여 개인 레포지토리에서 실습 환경을 구성**하였습니다.

<br>

## 2. 기술 스택

### Backend
- Java
- Spring Boot
- Spring Security
- JPA

### Database
- MySQL (Docker)

### Tools
- Burp Suite
- DBeaver
- Git / GitHub

<br>

## 3. 프로젝트 설치 및 실행 방법

### 1. 저장소 클론

```bash
git clone https://github.com/seoeunnn/web_project.git
```

### 2. Docker로 MySQL 실행

```bash
docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=1234 -e MYSQL_DATABASE=coco --name mysql-coco mysql:8
```

### 3. Spring Boot 

```bash
./gradlew bootRun 
```
또는 IDE(IntelliJ)에서 Spring Boot 애플리케이션 실행

### 4. 서비스 접속
Burp Suite 프록시 사용을 위해 기본 포트(8080)가 사용되므로
Spring Boot 서버는 8081 포트에서 실행하도록 설정했습니다.

http://localhost:8081

<br>

## 4. 프로젝트 구조
```text
src
├─ main
│  ├─ java/com/coco/board
│  │  ├─ presentation        # Controller (사용자 요청 처리)
│  │  │  ├─ CommentApiController.java
│  │  │  ├─ PostsApiController.java
│  │  │  ├─ PostsIndexController.java
│  │  │  ├─ UserApiController.java
│  │  │  └─ UserController.java
│  │  │
│  │  ├─ application         # Service (비즈니스 로직)
│  │  │  ├─ CommentService.java
│  │  │  ├─ PostsService.java
│  │  │  └─ UserService.java
│  │  │
│  │  ├─ domain              # Entity (DB 모델)
│  │  │  ├─ Comment.java
│  │  │  ├─ Posts.java
│  │  │  ├─ User.java
│  │  │  └─ Role.java
│  │  │
│  │  ├─ infrastructure
│  │  │  ├─ persistence      # Repository (DB 접근)
│  │  │  │  ├─ CommentRepository.java
│  │  │  │  ├─ PostsRepository.java
│  │  │  │  └─ UserRepository.java
│  │  │  │
│  │  │  └─ config           # Spring Security 설정
│  │  │     ├─ SecurityConfig.java
│  │  │     └─ WebConfig.java
│  │  │
│  │  └─ BoardApplication.java
│  │
│  └─ resources
│     ├─ templates           # Mustache View
│     │  ├─ posts
│     │  ├─ comment
│     │  └─ user
│     │
│     └─ static              # CSS / JS
│
└─ test                      # 테스트 코드
```

<br>

## 5. 분석 대상 기능
본 프로젝트에서는 다음과 같은 기능을 중심으로 취약점 분석을 진행합니다.

- 회원가입
- 로그인
- 게시글 작성 / 수정 / 삭제
- 게시글 검색
- 댓글 작성 / 수정 / 삭제

<br>

## 6. 분석 예정 취약점

본 프로젝트에서는 다음과 같은 **웹 취약점**을 중심으로 분석을 진행할 예정입니다.

- **SQL Injection**
- **CSRF (Cross Site Request Forgery)**
- **Cross Site Scripting (XSS)**
- **IDOR (Insecure Direct Object Reference)**

<br>

## 7. 프로젝트 진행 계획
1. 프로젝트 환경 구축
2. HTTP 요청 분석 (Burp Suite)
3. 서비스 구조 및 코드 분석
4. 취약점 공격 재현
5. Secure Coding 적용
6. 모의해킹 보고서 작성
