<img width="4032" height="711" alt="image" src="https://github.com/user-attachments/assets/0125adf9-cf81-4c4f-bb44-084ebf9fa808" /># 시간을 아끼는 UI/UX Research Agent

**Copilot Studio + SharePoint + Aside = Teams·Copilot에서 바로 쓰는 상품카드 리서치 에이전트**

경쟁사 PLP(상품 목록 페이지)의 상품카드 리서치부터 비교 PPT 보고서 작성까지 맡기는 에이전트를, 발표 화면 순서 그대로 누구나 따라 만들 수 있도록 정리한 Step by Step 가이드입니다.

> 발표: 김현혜 (프리랜서 UX Designer) · 2026.10.18<br>
> 발표 자료: [발표 자료](https://github.com/Ami2005/copilot-studio-uiux-agent/blob/main/%EC%8B%9C%EA%B0%84%EC%9D%84%20%EC%95%84%EB%81%BC%EB%8A%94%20UIUX%20Research%20Agent_%EB%B0%9C%ED%91%9C%EC%9E%90%EB%A3%8C_20261018.pdf](https://github.com/Ami2005/copilot-studio-uiux-agent/blob/main/UIUX_Research_Agent_20261018_v0.4.pdf)

---

## 도구 조합

| 도구 | 역할 | 하는 일 |
|---|---|---|
| **Copilot Studio** | 에이전트 빌더 | 안내(Instruction)·기술(Skill)·지식·도구 설정, Copilot Credit 종량제 과금 |
| **SharePoint** | 리서치 저장소 | `리서치 정보`(Word) / `리서치 보고서`(PPT) 폴더, 에이전트의 지식 원본 |
| **Aside** | 리서치 실행 | 경쟁사 PLP 상품카드 실측·분석 → Word 작성 → SharePoint 업로드 |
| **= Agent on Teams / Copilot** | 리서치 보고서 작성 & 목록 보기 | Teams·Copilot에서 바로 호출해 리서치 기반 PPT 비교 보고서 작성 |

### 작업 흐름

```
① Aside: 경쟁사 상품카드 리서치 실행
   └─▶ ② SharePoint '리서치 정보' 폴더에 Word 저장
          └─▶ ③ Copilot 에이전트가 리서치 정보를 근거로 PPT 비교 보고서 작성
                 └─▶ ④ SharePoint '리서치 보고서' 폴더 저장 · Teams/Copilot에서 공유
```

## 준비물

- Microsoft 365 **업무(회사) 계정** + 관리자 권한 (Power Platform·SharePoint 관리 센터 접근)
- 결제 수단이 등록된 **Azure 구독** (Copilot Credit 종량제 청구용)
- **Aside** (경쟁사 리서치 실행용)
- LLM 구독(Chat GPT, Claude 등) for Aside

---

## 따라하기 순서

### 1단계. 환경 준비

| # | 가이드 | 내용 |
|---|---|---|
| 01 | [Azure 리소스 생성](docs/01-azure-resource.md) | 청구용 Azure 리소스 그룹 만들기 |
| 02 | [Power Platform 환경 생성](docs/02-power-platform-environment.md) | 에이전트용 개발자 환경(Dataverse 포함) 만들기 |
| 03 | [Copilot Credit 설정](docs/03-copilot-credit-billing.md) | 청구 플랜으로 Azure 구독과 환경 연결 |
| 04 | [SharePoint 사이트 생성](docs/04-sharepoint-site.md) | `UIUX 리서치 관리` 사이트와 폴더 2개 만들기 |
| 05 | [Copilot Studio 환경 설정](docs/05-copilot-studio-environment.md) | 만든 환경으로 전환 |

### 2단계. 에이전트 생성

| # | 가이드 | 내용 |
|---|---|---|
| 06 | [Product Card 리서치 에이전트 만들기](docs/06-create-agent.md) | 안내·기술·지식·도구(SharePoint 파일 만들기)·추천 프롬프트 설정 |

### 3단계. 참고 자료

| # | 가이드 | 내용 |
|---|---|---|
| 07 | [Aside 채팅으로 작업하기](docs/07-reference-aside.md) | 리서치 정보·보고서 프롬프트와 실행 팁 |
| 08 | [Claude 프로젝트로 작업하기](docs/08-reference-claude.md) | Microsoft 365 커넥터 연결과 주의점 |
| 09 | [Copilot 에이전트 사용·공유](docs/09-reference-copilot-agent.md) | 구성 파일, 사용·공유 방법 |
| 10 | [실습 후 정리(삭제)](docs/10-cleanup.md) | SharePoint 사이트 → 환경 → Azure 리소스 순서로 삭제 |

---

## 레포 구성

```
.
├── README.md
├── docs/        # 단계별 가이드 (01~10)
├── prompts/     # 리서치 정보 / 리서치 보고서 프롬프트 템플릿
├── agent/       # 에이전트 구성 파일
│   ├── instructions.md                      # 안내(Instruction) - Agent Builder '안내' 칸에 붙여넣기
│   ├── SKILL.md                             # 기술(Skill) 원본
│   └── uiux-productcard-research-skill.zip  # 기술 업로드용 zip
├── images/      # 가이드 스크린샷 (빨간 박스 = 클릭/입력 위치)
└── slides/      # 발표 자료 PPT
```

## 참고

- 스크린샷의 계정 이메일, Azure 구독 ID, 사내 SharePoint 주소는 가려져 있습니다.
- `instructions.md`의 `<내 SharePoint ... 폴더 링크>` 부분은 본인이 만든 SharePoint 폴더 링크로 바꿔서 사용하세요.
- 예시 값(`2026_11`, `Hyun2026_11`, `CopilotCredit202618` 등)은 실습 때 사용한 이름이니 원하는 이름으로 바꿔도 됩니다.
- Microsoft 관리 화면은 업데이트로 메뉴 이름·위치가 조금씩 바뀔 수 있습니다.
