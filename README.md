<div align="center">
  <img width="150" height="150" alt="Logo-removebg-preview" src="https://github.com/user-attachments/assets/71bf9b4c-7a3a-4a5e-b547-91c4ac8bd52e" />
</div>

# REAP service (Record Everything And Play) - Server
**STT, RAG 활용 대화 기반 검색 서비스**
24년도 컴퓨터공학부 졸업프로젝트 REAP(Record Everything And Play) Service 입니다. 
<br>
발표영상 : [유튜브 링크](https://www.youtube.com/watch?v=q-nz9tahR1w)
<br>

## 1. 프로젝트 정보
* **Team:** REAP (3팀)
* **Member:** 강병현, 김준영, 심경보, 조정범
* **Professor:** 이항원 교수님

---

## 2. 프로젝트 개요 및 소개 (Introduction)

### 💡 기획 배경
일상 속 대화에는 많은 정보가 오고갑니다. 근데 쉽게 잊혀지곤 합니다.</br>
본 프로젝트는 일상 대화 속 정보를 편리하게 관리하고, 필요한 순간 편하게 꺼내 볼 수 있는 것을 돕기 위해 시작됐습니다.

### 📝 프로젝트 요약
REAP service는 사용자의 대화를 녹음하고, 필요한 데이터를 쉽게 찾아 활용할 수 있는 서비스입니다. 사용자가 기록하고 싶은 대화를 음성 파일로 저장한 후, 이를 텍스트로 변환하여 스크립트화해서 제공합니다. RAG(Retrieval-Augmented Generation)를 활용하여 별도의 튜닝 없이도 대화 데이터에 대한 검색 및 질의응답이 가능하도록 설계하였습니다.

---

## 3. 아키텍처 (SW Architecture)
서비스의 안정적인 운영을 위해 다음과 같은 기술 스택을 사용하였습니다.

* **Client:** Android Application
* **API Server (AWS Lightsail):** Spring Boot, Spring AI, Spring Secure, Naver Clova STT API, OpenAI API(gpt)
* **Database:** MongoDB Atlas, MySQL, Redis, Chroma DB, AWS S3

---

## 4. 서비스 흐름 (Service Flow)

### ⚙️ 작동 방식
1.  사용자가 앱을 통해 대화 음성 파일을 업로드하거나 직접 녹음합니다.
2.  음성 파일은 **AWS S3**에 저장되고, **Naver Clova STT API**를 통해 텍스트로 변환됩니다.
3.  변환된 텍스트는 메타데이터를 추가하여 **MongoDB**에 저장되며, 문서를 분할 및 임베딩하여 **Chroma DB**에 저장합니다.
4.  사용자가 질문을 입력하면, 메타데이터 필터와 유사도 검색을 통해 연관성이 높은 문서를 검색하고 이를 기반으로 답변을 생성합니다.
5.  생성된 답변을 앱을 통해 사용자에게 실시간으로 제공합니다.

---

## 5. 주요 결과물 (Result)
* **캘린더 및 리스트:** 날짜별 대화 기록 관리 및 최근 녹음 목록 확인.
* **대화 스크립트:** 화자 분리 및 타임스탬프가 적용된 상세 대화 내용 제공.
* **REAP Chat:** 대화 내용을 바탕으로 질문하고 답변받는 RAG 기반 챗봇 서비스.

---

## 6. 기대효과 및 아쉬운 점 (Expectation & Limits)

### ✅ 기대효과
* **효율적인 정보 검색:** 질문에 맞는 관련 데이터를 즉각적으로 제공.
* **업무 활용 가능:** 회의록 기록 및 비즈니스 환경에서의 활용도 높음.
* **기능 확장성:** 대화 데이터 기반의 다양한 추가 기능 확장 가능.

### ⚠️ 아쉬운 점
* **법적 문제:** 실시간 수집의 법적 한계(제3자 녹음 등)로 인해 사용자 직접 업로드 방식으로 범위 축소.
* **STT 정확도:** 주변 소음 및 발음 차이에 따른 변환 정확도의 가변성 존재.

## 7. 소프트웨어 아키텍처
![image](https://github.com/user-attachments/assets/9a549bbf-e677-4c45-9f09-e2b39a8359cc)
