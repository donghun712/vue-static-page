# Vue 3 + TypeScript + Vite

https://donghun712.github.io/vue-static-page/

# 🌕 한가위 웹페이지

Vue 3 + TypeScript + Vite로 제작한 추석(한가위) 테마 단일 페이지 애플리케이션입니다.  
전통 한국 색감(오방색)과 보름달, 학, 구름, 솔잎, 기와지붕 모티프를 CSS로 구현했습니다.

## ✨ 주요 기능

- **자동 메시지 전환**: 3.5초마다 추석 인사말이 부드럽게 바뀝니다
- **페이드 트랜지션**: Vue의 `<Transition>` 컴포넌트로 자연스러운 효과 구현
- **반응형 디자인**: 모바일부터 데스크톱까지 최적화
- **순수 CSS 그래픽**: 외부 이미지 없이 달·구름·학·솔잎을 CSS로 표현
- **전통 색감**: 오방색(청·홍·황·흑·백) 팔레트 적용

## 🛠 기술 스택

- **프론트엔드**: Vue 3 (Composition API + `<script setup>`)
- **타입 시스템**: TypeScript
- **빌드 도구**: Vite
- **스타일**: Scoped CSS + CSS Variables

## 📦 설치 및 실행

### 개발 서버 실행
npm install
npm run dev

## 📂 프로젝트 구조
<pre> 

├── src/ 
│ ├── App.vue # 메인 컴포넌트 (전체 페이지) 
│ └── main.ts # 애플리케이션 엔트리 포인트 
├── public/ # 정적 파일 
├── index.html 
├── package.json 
├── tsconfig.json 
├── vite.config.ts 
└── README.md 
</pre>

## 🎨 디자인 컨셉

### 색상 팔레트
- **배경 그라디언트**: 남색(`#1b2745`) → 자줏빛(`#352a3a`) 밤하늘
- **오방색 띠**: 청(`#1f5ca8`), 홍(`#ed302b`), 황(`#e1b500`), 흑(`#2d2d2d`), 백(`#e8e5df`)
- **보름달**: 미색(`#ffdca8`) 그라디언트
- **솔잎**: 녹색(`#4a6d3b`)

### 애니메이션
- 구름 좌우 부유 (24초 주기)
- 학 날갯짓 효과 (16초 주기)
- 메시지 페이드 인/아웃 (0.3초)
## 💬 사용한 프롬프트

### 1. 초기 App.vue 생성
vue + ts + vite를 사용해서 한가위에 잘 어울리는 웹페이지를 만들고 싶어, app.vue파일을 하나 깔끔하게 만들어줘

### 2. TypeScript 오류 해결 (TS6133)
Error: src/App.vue(17,5): error TS6133: 'timer' is declared but its value is never read.

Error: Process completed with exit code 2.

**해결 방법**: `onUnmounted` 훅에서 `clearInterval(intervalId)`로 타이머를 정리하여 변수가 실제로 "읽히도록" 수정

