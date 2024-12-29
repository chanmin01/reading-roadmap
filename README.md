
# 📚 독서 로드맵 추천 시스템

---

## 프로젝트 개요
독서를 통해 개인의 목표를 체계적으로 달성할 수 있도록 돕는 플랫폼입니다.  
사용자는 목표를 설정하고, 목표 달성에 적합한 추천 도서 로드맵을 제공받으며, 독서 기록을 관리하고 통계 및 피드백을 통해 진행 상황을 확인할 수 있습니다.  
또한, 커뮤니티 기능을 통해 다른 사용자들과 독서 경험을 공유하며, 추후 AI 기반 맞춤형 추천 시스템도 도입할 예정입니다.

---

## 주요 기능

### 1. 사용자 관리
- 회원 가입 및 로그인
- 사용자 프로필 설정 (닉네임, 관심사, 독서 성향)

### 2. 목표 및 로드맵 관리
- **목표 설정**: 사용자가 목표를 설정하고 자유롭게 로드맵 구성
- **로드맵 수정**: 사용자가 원하는 책을 추가/제거하고 로드맵을 재구성
- **추천 로드맵**: 기초 → 심화 → 응용 단계로 구성된 도서 로드맵 추천 (업데이트 예정)

### 3. 독서 기록 관리
- **읽기 상태 관리**:
  - 사용자가 책의 상태를 "읽기 시작", "읽는 중", "완독"으로 변경 가능.
  - 상태 변경 시 날짜와 시간을 기록하여 독서 진행 상황을 추적.
- **읽은 페이지 수 입력**:
  - 사용자가 현재까지 읽은 페이지 수를 직접 입력.
  - 상태 변경 시 페이지 수와 상태를 함께 전송.
- **월간 독서 통계**:
  - 사용자가 특정 월에 읽은 책 수, 독서 시간, 평균 독서량 확인.

### 4. 통계 및 피드백
- 목표 진행률 확인
- 월간 독서 패턴 분석 및 통계 제공

### 5. 커뮤니티 기능 (업데이트 예정)
- 책 리뷰 및 추천 공유
- 댓글과 좋아요를 통해 사용자 간 상호작용

### 6. AI 기반 맞춤 추천 (업데이트 예정)
- 사용자 독서 데이터를 기반으로 개인화된 책 추천

---

## ERD
![read-to-achieve](https://github.com/user-attachments/assets/adc375b7-e686-4dda-b187-787617af8954)

---

## 📜 API 문서

### 1. 사용자 관리
| API Name       | Method | Endpoint           | Description             | Request Body Example                                     |
|----------------|--------|--------------------|-------------------------|---------------------------------------------------------|
| 회원가입         | POST   | `/auth/signup`     | 사용자 회원가입           | `{ "email": "user@example.com", "password": "1234", "nickname": "User" }` |
| 로그인           | POST   | `/auth/login`      | 사용자 로그인             | `{ "email": "user@example.com", "password": "1234" }`    |

---

### 2. 목표 관리
| API Name        | Method | Endpoint               | Description                              | Request Body Example                                     |
|-----------------|--------|------------------------|------------------------------------------|---------------------------------------------------------|
| 목표 생성         | POST   | `/goals`               | 새로운 목표를 생성                        | `{ "title": "Java 학습", "description": "기초부터 고급까지 배우기" }` |
| 목표 상세 조회    | GET    | `/goals/{id}`          | 특정 목표와 연결된 책 리스트 조회          | N/A                                                     |
| 목표에 책 추가    | POST   | `/goals/{id}/books`    | 특정 목표에 사용자가 추가한 책 연결        | `{ "isbn": "9780134685991" }`                           |

---

### 3. 독서 기록 관리
| API Name        | Method | Endpoint               | Description                              | Request Body Example                                     |
|-----------------|--------|------------------------|------------------------------------------|---------------------------------------------------------|
| 독서 기록 추가    | POST   | `/records`             | 특정 책의 독서 상태 추가                  | `{ "book_isbn": "9780134685991", "status": "reading", "currentPage": 120 }` |
| 독서 기록 조회    | GET    | `/records`             | 사용자의 독서 기록 목록 조회              | N/A                                                     |

---

### 4. 통계 및 피드백
| API Name         | Method | Endpoint               | Description                              | Request Body Example                                     |
|------------------|--------|------------------------|------------------------------------------|---------------------------------------------------------|
| 목표 진행률 조회   | GET    | `/stats/progress`      | 특정 목표의 독서 진행률 반환              | N/A                                                     |
| 독서 패턴 분석     | GET    | `/stats/patterns`      | 월별 독서 통계 및 패턴 제공               | `?month=2024-12`                                        |

---

## Google Books API 정보

### Primary Key (`id`)
Google Books API는 각 책에 대해 고유 식별자인 **`id` 필드**를 제공합니다.  
이 `id` 필드는 Google Books 시스템 내에서 책을 식별하는 Primary Key 역할을 하며, ISBN이 없는 책도 고유하게 관리할 수 있도록 도와줍니다.

#### **예제 응답**
```json
{
  "id": "OEBQDwAAQBAJ",
  "volumeInfo": {
    "title": "Effective Java",
    "authors": ["Joshua Bloch"],
    "pageCount": 416,
    "language": "en"
  }
}
```
---

## 기술 스택

### 🛠️ 백엔드
<img src="https://img.shields.io/badge/spring-6DB33F?style=for-the-badge&logo=spring&logoColor=white">
<img src="https://img.shields.io/badge/spring%20security-6DB33F?style=for-the-badge&logo=springsecurity&logoColor=white">

### 🗄️ 데이터베이스
<img src="https://img.shields.io/badge/mysql-4479A1?style=for-the-badge&logo=mysql&logoColor=white">
<img src="https://img.shields.io/badge/redis-DC382D?style=for-the-badge&logo=redis&logoColor=white">

### 🔍 API 문서화 및 테스트
<img src="https://img.shields.io/badge/swagger-85EA2D?style=for-the-badge&logo=swagger&logoColor=white">
<img src="https://img.shields.io/badge/postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white">

### ☁️ 배포
<img src="https://img.shields.io/badge/AWS%20EC2-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white">

---
