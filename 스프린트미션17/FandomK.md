# 스프린트 미션 17

> Fandom-K
[내가 좋아하는 아이돌을 가장 쉽게 덕질하는 방법]

__후원테이블__
- 크레딧은 Fandom-K에서 사용하는 가상 화폐에요.
- 소유하고 있는 크레딧을 내가 원하는 조공에 후원할 수 있어요.
- 후원할 크레딧은 내가 보유하고 있는 크레딧 내에서 자유롭게 결정할 수 있어요.
- 여러 유저의 후원을 통해 크레딧 목표치가 달성되면 조공이 이루어져요.

__이달의 아티스트 투표하기__
- 카테고리 별로 내가 원하는 아티스트에게 투표할 수 있어요.
- 한 번 투표하는데 일정 크레딧이 소모됩니다.
- 한 유저가 여러 아티스트에게 투표할 수 있고, 투표 횟수도 무제한이에요. 😈

__나만의 아티스트__
- 마이페이지에서 내가 좋아하는 아티스트들을 팔로우 할 수 있어요.
- 팔로우한 아티스트의 여러 소식들을 메인 화면에서 확인할 수 있어요.

__충전하기__
- 크레딧을 원하는 만큼 충전할 수 있어요.
- Fandom-K의 주요 매출은 크레딧 판매 수수료로 발생하고 있어요.

> 미션에서 필요한 요구조건 정의서

---

### 필요 엔티티 정의 및 선언
#### Database 엔티티 구성도
![image](https://github.com/user-attachments/assets/93f5ebcd-9f7b-4e71-bc84-33c2acf286d5)


#### 1. 회원 정보(USER_INFO) 엔티티

<p align='center'>
  <img src='https://github.com/user-attachments/assets/72b59ea9-13bc-4634-b3f6-04da2e259a95'/>
</p>

#### 2. 아티스트 정보(ARITIST_INFO) 엔티티

<p align='center'>
  <img src='https://github.com/user-attachments/assets/5bc530bb-07d4-483d-90fa-51e400bda7f6'/>
</p>

#### 3. 팔로우(FOLLOW_INFO) 엔티티

<p align='center'>
  <img src='https://github.com/user-attachments/assets/4d3cbe0b-2dd8-4dd2-a02d-1b2cd841ede7'/>
</p>

> 팔로우 엔티티의 경우 회원정보와 아티스트 정보 엔티티 간 N:M 관계로 연결해주는 엔티티

#### 4. 아티스트 코드(ARITIST_CODE) 엔티티

<p align='center'>
  <img src='https://github.com/user-attachments/assets/932e7757-1d71-4dfc-9f39-8678f01a2769'/>
</p>

> 아티스트 코드 엔티티는 아티스트의 카테고리를 세분화하기 위한 엔티티    
> 아티스트 정보 엔티티와 1:M 관계

#### 5. 크레딧 구매 이력(CREDIT_TRANSACTION) 엔티티

<p align='center'>
  <img src='https://github.com/user-attachments/assets/d8edaab9-15ad-47c8-be49-ce67f42ea93f'/>
</p>

> 회원정보와 구매 이력 엔티티는 1:M 관계

#### 6. 후원 정보(SUPPORT_INFO) 엔티티

<p align='center'>
  <img src='https://github.com/user-attachments/assets/110d5ba5-d709-4088-b76e-67d4c5164f5a'/>
</p>

> 회원정보와 후원 정보 엔티티는 1:M 관계

#### 7. 조공 정보 (GIFT_INFO)

<p align='center'>
  <img src='https://github.com/user-attachments/assets/3a642c79-c185-491a-a93a-bec20bbe704d'/>
</p>

> 후원정보와 조공정보 엔티티는 1:M 관계
> 아티스트정보와 조공정보 엔티티는 1:M의 관계

#### 8. 조공 타입(GIFT_TYPE_CODE)

<p align='center'>
  <img src='https://github.com/user-attachments/assets/c3a3f835-4639-426f-96db-9b9b10acd4e1'/>
</p>

> 조공의 종류가 다양하고 새로운 조공 타입이 생길 수 있다고 판단하여 조공타입 엔티티 설계
> 조공정보와 조공타입 엔티티는 1:M의 관계

#### 9. 관심 아티스트 (FAV_ARTIST_INFO)

<p align='center'>
  <img src='https://github.com/user-attachments/assets/b7824efe-9aed-473f-b651-da8649af0c9a'/>
</p>

> 회원정보와 관심 아티스트 엔티티는 1:M의 관계
> 아티스트정보와 관심 아티스트 엔티티 1:M의 관계

#### 10. 크레딧 사용이력 (USED_CREDIT)

<p align='center'>
  <img src='https://github.com/user-attachments/assets/4faa5981-59e8-4ae5-9c71-e09426023eb0'/>
</p>

> 후원정보과 크레딧 사용이력 엔티티 간 1:M의 관계
> 인기투표와 크레딧 사용이력 엔티티 간 1:M의 관계

#### 11. 인기 투표 (VOTE)

<p align='center'>
  <img src='https://github.com/user-attachments/assets/ec8a675c-f3a1-4d04-9ec5-b2243b8879ad'/>
</p>

> 인기투표와 아티스트정보 간 1:1 관계

---
### DDL Query 
```
-- 데이터베이스 생성 및 사용
CREATE DATABASE FandomK;
USE FandomK;

-- ARTIST_CODE 테이블 생성 (참조되는 테이블)
CREATE TABLE ARTIST_CODE (
    CATEGORY_CODE INT NOT NULL PRIMARY KEY,
    CATEGORY_NAME VARCHAR(20) NOT NULL
);

-- GIFT_TYPE_CODE 테이블 생성 (참조되는 테이블)
CREATE TABLE GIFT_TYPE_CODE (
    GIFT_TYPE INT NOT NULL PRIMARY KEY,
    GIFT_NAME VARCHAR(20) NOT NULL
);

-- USER_INFO 테이블 생성
CREATE TABLE USER_INFO (
    USER_ID VARCHAR(20) NOT NULL PRIMARY KEY,
    USER_NAME VARCHAR(20) NOT NULL,
    USER_BIRTH DATE NOT NULL,
    USER_GENDER ENUM('남', '여') NOT NULL,
    USER_EMAIL VARCHAR(50) NOT NULL,
    USER_CREDIT INT NOT NULL,
    USER_JOIN DATETIME NOT NULL
);

-- ARTIST_INFO 테이블 생성 (ARTIST_CODE 참조)
CREATE TABLE ARTIST_INFO (
    ARTIST_ID VARCHAR(50) NOT NULL PRIMARY KEY,
    ARTIST_NAME VARCHAR(20) NOT NULL,
    ARTIST_GENDER ENUM('남', '여') NOT NULL,
    CATEGORY_CODE INT NOT NULL,
    DESCRIPTION TEXT NOT NULL,
    CREATED_AT DATE NOT NULL,
    FOREIGN KEY (CATEGORY_CODE) REFERENCES ARTIST_CODE(CATEGORY_CODE)
);

-- CREDIT_TRANSACTION 테이블 생성 (USER_INFO 참조)
CREATE TABLE CREDIT_TRANSACTION (
    TRANSACTION_ID VARCHAR(20) NOT NULL PRIMARY KEY,
    USER_ID VARCHAR(20) NOT NULL,
    AMOUNT INT NOT NULL,
    CREATED_AT DATETIME NOT NULL,
    SUM_AMOUNT INT NOT NULL,
    FOREIGN KEY (USER_ID) REFERENCES USER_INFO(USER_ID)
);

-- SUPPORT_INFO 테이블 생성 (USER_INFO 참조)
CREATE TABLE SUPPORT_INFO (
    SUPPORT_ID VARCHAR(20) NOT NULL PRIMARY KEY,
    USER_ID VARCHAR(20) NOT NULL,
    CREDIT_AMOUNT INT NULL,
    CREATED_AT DATETIME NULL,
    FOREIGN KEY (USER_ID) REFERENCES USER_INFO(USER_ID)
);

-- FOLLOW_INFO 테이블 생성 (USER_INFO, ARTIST_INFO 참조)
CREATE TABLE FOLLOW_INFO (
    FOLLOW_ID VARCHAR(20) NOT NULL PRIMARY KEY,
    FOLLOWED_AT DATETIME NOT NULL,
    USER_ID VARCHAR(20) NOT NULL,
    ARTIST_ID VARCHAR(50) NOT NULL,
    FOREIGN KEY (USER_ID) REFERENCES USER_INFO(USER_ID),
    FOREIGN KEY (ARTIST_ID) REFERENCES ARTIST_INFO(ARTIST_ID)
);

-- FAV_ARTIST_INFO 테이블 생성 (USER_INFO, ARTIST_INFO 참조)
CREATE TABLE FAV_ARTIST_INFO (
    FAV_ID VARCHAR(20) NOT NULL PRIMARY KEY,
    USER_ID VARCHAR(20) NOT NULL,
    ARTIST_ID VARCHAR(50) NOT NULL,
    FOREIGN KEY (USER_ID) REFERENCES USER_INFO(USER_ID),
    FOREIGN KEY (ARTIST_ID) REFERENCES ARTIST_INFO(ARTIST_ID)
);

-- VOTE 테이블 생성 (USER_INFO, ARTIST_INFO 참조)
CREATE TABLE VOTE (
    VOTE_ID VARCHAR(20) NOT NULL PRIMARY KEY,
    USER_ID VARCHAR(20) NOT NULL,
    ARTIST_ID VARCHAR(50) NOT NULL,
    VOTE_DATE DATETIME NOT NULL,
    FOREIGN KEY (USER_ID) REFERENCES USER_INFO(USER_ID),
    FOREIGN KEY (ARTIST_ID) REFERENCES ARTIST_INFO(ARTIST_ID)
);

-- GIFT_INFO 테이블 생성 (SUPPORT_INFO, ARTIST_INFO, GIFT_TYPE_CODE 참조)
CREATE TABLE GIFT_INFO (
    GIFT_ID VARCHAR(20) NOT NULL PRIMARY KEY,
    SUPPORT_ID VARCHAR(20) NOT NULL,
    ARTIST_ID VARCHAR(50) NOT NULL,
    GIFT_TYPE INT NOT NULL,
    FOREIGN KEY (SUPPORT_ID) REFERENCES SUPPORT_INFO(SUPPORT_ID),
    FOREIGN KEY (ARTIST_ID) REFERENCES ARTIST_INFO(ARTIST_ID),
    FOREIGN KEY (GIFT_TYPE) REFERENCES GIFT_TYPE_CODE(GIFT_TYPE)
);

-- USED_CREDIT 테이블 생성 (SUPPORT_INFO, VOTE 참조)
CREATE TABLE USED_CREDIT (
    USED_ID VARCHAR(20) NOT NULL PRIMARY KEY,
    USED_DATE DATETIME NOT NULL,
    USED_CREDIT INT NOT NULL,
    USED_REASON VARCHAR(20) NOT NULL,
    SUPPORT_ID VARCHAR(20),
    VOTE_ID VARCHAR(20),
    FOREIGN KEY (SUPPORT_ID) REFERENCES SUPPORT_INFO(SUPPORT_ID),
    FOREIGN KEY (VOTE_ID) REFERENCES VOTE(VOTE_ID)
);

```
---
### EDR Cloud vs MySQL Workbench 비교

<p align='center'>
  <img src='https://github.com/user-attachments/assets/a88a0371-a0f1-409f-8bbe-d29015d22479'/>
</p>
