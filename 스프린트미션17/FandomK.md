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
> 아티스트 정보 엔티티와 1:N 관계

#### 5. 크레딧 구매 이력(CREDIT_TRANSACTION) 엔티티

<p align='center'>
  <img src='https://github.com/user-attachments/assets/d8edaab9-15ad-47c8-be49-ce67f42ea93f'/>
</p>

> 회원정보와 구매 이력 엔티티는 1:N 관계

#### 6. 후원 정보(SUPPORT_INFO) 엔티티

<p align='center'>
  <img src='https://github.com/user-attachments/assets/110d5ba5-d709-4088-b76e-67d4c5164f5a'/>
</p>
