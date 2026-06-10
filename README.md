<div align="center">

# 🟩 TroubleLog

**AI 코드 분석 기반 모의 면접 및 트러블슈팅 리포트 생성 플랫폼**

> 내가 작성한 코드로 면접을 준비한다

[![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white)](https://vitejs.dev)
[![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)](https://react.dev)
[![TailwindCSS](https://img.shields.io/badge/TailwindCSS-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)](https://tailwindcss.com)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![Azure](https://img.shields.io/badge/Azure-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)](https://azure.microsoft.com)
[![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat-square&logo=openai&logoColor=white)](https://openai.com)

</div>

---

## 📌 프로젝트 개요

촉박한 스프린트 일정 혹은 학업을 병행하는 일정 속에서 AI에 과도하게 의존한 탓에, 본인이 선택한 기술 스택이나 작성한 코드를 제대로 설명하지 못하는 취준생을 위한 서비스.
사용자가 직접 작성한 소스코드를 AI가 분석해 맞춤형 기술 면접 질문을 생성하고, 면접 Q&A를 바탕으로 트러블슈팅 리포트를 자동 생성.

---

## ✨ 주요 기능

| 기능 | 설명 |
|------|------|
| **코드 기반 면접 질문 생성** | 제출한 소스코드 + 사전 컨텍스트(기술 스택, 역할, 예외 처리 방식 등)를 분석해 AI가 맞춤형 기술 면접 질문 생성 |
| **AI 실시간 피드백** | 답변의 구체성·논리 구조·기술 용어 사용 등을 기준으로 건설적인 코칭 제공 |
| **역량 레이더 차트** | 문제 해결력 / 기술 판단력 / 코드 신뢰성 / 커뮤니케이션 / 설계 사고력 5개 축으로 역량 시각화 |
| **트러블슈팅 리포트 자동 생성** | 면접 Q&A 기반으로 Background → Problem → Root Cause → Resolution → Result 5섹션 마크다운 리포트 자동 생성 |
| **개인정보 자동 차단** | 코드 입력 시 이메일, 전화번호, 비밀번호, API Key 등을 정규식으로 탐지해 AI 요청 전 차단 |
| **감사 로그** | AI 요청·답변 제출·인증 이력을 별도 트랜잭션으로 저장, 민감 원문은 제외하고 요약 정보만 기록 |

---

## 🛠 기술 스택

### Frontend
- **Vite + React** — SPA 구성
- **Tailwind CSS** — 유틸리티 기반 스타일링

### Backend
- **Spring Boot** — REST API 서버
- **Azure OpenAI (GPT-4o)** — 면접 질문 생성 / 답변 피드백 / 리포트 생성
- **Azure SQL Database** — 사용자 데이터 및 감사 로그 저장
- **JDBC** — DB 연결

### Infrastructure
- **Azure App Service** — 백엔드 배포
- **GitHub Actions** — CI/CD 파이프라인
- **CodeRabbit** — AI 코드 리뷰 자동화

---

## 🏗 아키텍처

```
[ User ]
   │  HTTPS
   ▼
[ React + Vite ]  ◀─── Warning Response (개인정보 감지 시)
   │  REST API
   ▼
[ Spring Boot / Azure App Service ]
   ├── Personal Info Detection  ← 정규식 기반 민감정보 탐지
   ├── AuditLogService          ← 감사 로그 (별도 트랜잭션)
   ├── HTTPS ──▶ Azure OpenAI   ← 질문 생성 / 피드백 / 리포트
   └── JDBC  ──▶ Azure SQL DB   ← 데이터 저장

[ Developer ]
   │  git push/PR
   ▼
[ GitHub ] ──trigger──▶ [ GitHub Actions ] ──Deploy──▶ Spring Boot
                └──▶ [ CodeRabbit ] (자동 코드 리뷰)
```

---

## 🔄 서비스 흐름

```
로그인 / 회원가입
      ↓
소스코드 입력  (개인정보 감지 → 경고 or 차단)
      ↓
사전 컨텍스트 입력  (코드 목적 / 기술 선택 이유 / 예외 처리 방식 / 프로젝트 규모)
      ↓
AI 모의 면접  (질문 생성 → 답변 → AI 피드백)
      ↓
역량 점수 + 트러블슈팅 리포트 확인 및 마크다운 복사
```

---

## 📁 레포지토리 구조

```
TroubleLog/
├── troublelog-client   # React + Vite 프론트엔드
└── troublelog-server    # Spring Boot 백엔드
```

---

## 👥 팀원

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/slwnoey">
        <img src="https://github.com/slwnoey.png" width="80" style="border-radius:50%"/><br/>
        <b>이연진</b>
      </a><br/>
      <sub>Frontend</sub>
    </td>
    <td align="center">
      <a href="https://github.com/lyeonj">
        <img src="https://github.com/lyeonj.png" width="80" style="border-radius:50%"/><br/>
        <b>이연재</b>
      </a><br/>
      <sub>Frontend</sub>
    </td>
    <td align="center">
      <a href="https://github.com/hgeniee">
        <img src="https://github.com/hgeniee.png" width="80" style="border-radius:50%"/><br/>
        <b>이현진</b>
      </a><br/>
      <sub>Backend</sub>
    </td>
    <td align="center">
      <a href="https://github.com/dl-tpdnjs">
        <img src="https://github.com/dl-tpdnjs.png" width="80" style="border-radius:50%"/><br/>
        <b>이세원</b>
      </a><br/>
      <sub>Backend</sub>
    </td>
  </tr>
</table>

---

## 📅 개발 기간

**2025.05.14 ~ 2025.06.10 (4주)**

---

<div align="center">
  <sub>26-1 인공지능산업체특강 | Team 7</sub>
</div>
