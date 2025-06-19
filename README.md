
# 🏃🏻 TodoPang: 사용자/관리자 서버 개발 프로젝트
* 일상 속 작은 위시를 통해 성취감과 셀프 힐링을 추구하는 서비스, TodoPang 백엔드 서버입니다.
* 앱 사용자 기능은 컨텐츠(위시) 탐색 및 등록, 완료와 함께 리뷰를 등록하는 기능을 제공합니다.
* 관리자 기능은 비개발 직군의 데이터 관리 및 CS대응이 가능한 기능을 제공합니다.

<br>

## 😎 주요 기능 (Features)

### 사용자 기능
* Firebase를 이용한 소셜 로그인 (Google, Apple) 및 회원가입/탈퇴
* 페이지네이션 및 Fetch Join 최적화가 적용된 도전과제 목록 및 상세 정보 조회
* 사용자별 컨텐츠(위시) 등록, 포기(소프트 삭제), 완료 상태 관리
* 컨텐츠(위시)별 할 일(Todo) 진행 상태 실시간 변경 (완료/미완료) 및 적용 
* 완료한 컨텐츠(위시)에 대한 만족도 및 리뷰 제출

### 관리자 기능
* 관리자 계정 등록 및 관리 기능 제공 
* 도전과제, 카테고리, 리뷰 등 핵심 콘텐츠 CRUD 및 배포 상태 관리 (준비중/배포/삭제)

<br><br>

## ⁉️ 기술적 특징 및 해결 과제 (Technical Highlights)
이 프로젝트를 진행하며 마주친 주요 기술적 문제들과 해결 과정에 대한 상세한 내용은 아래 포트폴리오 링크에서 확인하실 수 있습니다.

* **JPA 성능 최적화**
  * N+1 문제를 인지하고, Fetch Join, DTO Projection 등을 통해 조회 성능을 개선
* **데이터 정합성을 고려한 트랜잭션 설계**
  * 복합 데이터의 업데이트 시, 단일 트랜잭션 API를 설계하고, 명시적 DTO를 활용
  * 통계 데이터 업데이트 시, 동시성 문제 해결을 위해 JPQL을 통한 원자적 업데이트 로직 구현
  * 읽기 전용 작업 시, @Transactional(readOnly = true) 옵션을 적용하여 불필요한 오버헤드를 줄이고 조회 성능을 최적화
* **유연한 데이터 모델링**
  * 데이터 이력 보존을 위해 소프트 삭제(Soft Delete) 패턴을 도입
  * 시스템 데이터와 관리 데이터를 명확히 분리하기 위해 플래그(status) 컬럼을 활용
* **비동기 처리를 통한 UX 개선**
  * 회원탈퇴의 경우, 외부 API 호출(Firebase)과 내부 DB 업데이트가 필요 
  * @Async와 CompletableFuture를 적용, 병렬 처리로 API 응답 시간을 단축하여 사용자 경험을 개선

<br><br>

## 🗺️ 아키텍처 (Architecture)
* **Controller**
  * HTTP 요청/응답 처리 및 서비스 계층 인터페이스 역할
* **Service**
  * 핵심 비즈니스 로직 수행 역할
  * 요청 DTO 검증 및 응답 DTO 조립 등의 역할을 수행하는 Service 클래스
  * 관련 DB 요청처리를 담당하는 Transaction 클래스 
* **Repository**
  * SpringData JPA 및 JPQL을 활용한 데이터베이스 접근 추상화 역할 
  * 여러 Entity들 간, 데이터 조합 조회 시 빠른 성능을 위해 DTO Projection 활용 
* **Security**
  * 웹 어드민의 원활한 사용을 위해 자체 Cors 설정 구성 및 적용
  * 자체 TokenFilter 구성을 통해 API별 검증 로직 커스텀화 적용

<br><br>

## 👥 팀원 및 역할 (Team & Roles)
<table align="center">
  <thead>
    <tr>
      <th align="center" width="220px">PM & Server Dev</th>
      <th align="center" width="220px">iOS App Dev</th>
      <th align="center" width="220px">UX/UI & Designer</th>
      <th align="center" width="220px">UX/UI & Designer</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">
        <a href="https://github.com/crossbell8368">
          <img src="https://avatars.githubusercontent.com/u/50852143?v=4" width="160" alt="서버 개발자 프로필"/>
        </a>
        <br/>
      </td>
      <td align="center">
        <a href="https://github.com/wangkobong">
          <img src="https://github.com/1OS-DevTeam/TodoPang/assets/50852143/6ae3bc74-9815-4fd2-8c7b-f59722d1b595" width="160" alt="iOS 개발자 프로필"/>
        </a>
        <br/>
      </td>
      <td align="center">
        <a href="https://github.com/1OS-DevTeam/TodoPang">
          <img src="https://github.com/1OS-DevTeam/TodoPang/assets/50852143/6a34054d-323f-4e9a-a00f-16d49182b43b" width="160" alt="디자이너1 프로필"/>
        </a>
        <br/>
      </td>
      <td align="center">
        <a href="https://github.com/1OS-DevTeam/TodoPang">
          <img src="https://github.com/1OS-DevTeam/TodoPang/assets/50852143/d5f19f34-2d61-4a0e-8ed5-7ac824b56a74" width="160" alt="디자이너2 프로필"/>
        </a>
        <br/>
      </td>
    </tr>
    <tr>
      <td align="center">인프라 구축, API 서버 설계 및 개발, DB 모델링</td>
      <td align="center">앱 UI/UX 구현, 서버 API 연동</td>
      <td align="center">App 화면 설계 및 디자인, 사용자 경험 설계</td>
      <td align="center">App 화면 설계 및 디자인, 마케팅 전략 수립</td>
    </tr>
  </tbody>
</table>

<br><br>

## 🛠️ 활용기술 (Tech Feature)
| Java | SpringBoot | PostgreSQL | JPA | Firebase | Redis | Gradle |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| <img alt="Java logo" src="https://github.com/user-attachments/assets/86fb0408-4b4d-40ad-b9f7-719ff0e96ab4" width="65" height="65" > | <img alt="SpringBoot logo" src="https://github.com/user-attachments/assets/67819669-78c5-404b-89e8-3ad25e0ba196" width="65" height="65"> | <img alt="PostgreSQL logo" src="https://github.com/user-attachments/assets/16b3398b-6c83-4648-b941-50d02ea45fc5" height="65" width="65"> | <img alt="JPA logo" src="https://github.com/user-attachments/assets/9926f6d9-c5bc-4d6d-b381-f5530000bd40" height="65" width="65"> | <img alt="Firebase logo" src="https://github.com/user-attachments/assets/89a13c6b-ea7c-4830-a918-810f97187572" height="65" width="65"> | <img alt="Redis logo" src="https://github.com/user-attachments/assets/dd6a5d37-22ed-481e-8004-403a2317dcea" height="65" width="65"> | <img alt="Gradle logo" src="https://github.com/user-attachments/assets/77fe8a25-b003-4035-85a7-9befa580394e" height="65" width="65"> 
