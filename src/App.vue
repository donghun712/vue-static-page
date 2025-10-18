<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const wishes = ['풍성한 한가위 보내세요', '보름달처럼 마음도 꽉 채우세요', '가족과 함께 따뜻한 명절 되세요', '늘 건강하고 행복하세요']
const idx = ref(0)
const next = () => { idx.value = (idx.value + 1) % wishes.length }

// setInterval id 저장용 변수 (브라우저에서는 number)
let intervalId: number | undefined

onMounted(() => {
  intervalId = window.setInterval(next, 3500)
})

onUnmounted(() => {
  if (intervalId !== undefined) {
    clearInterval(intervalId)
  }
})
</script>

<template>
  <main class="layout">
    <!-- 하늘 그라디언트 -->
    <div class="sky">
      <!-- 보름달 -->
      <div class="moon">
        <div class="moon-shine" />
      </div>

      <!-- 구름 -->
      <div class="cloud cloud-1" />
      <div class="cloud cloud-2" />
      <div class="cloud cloud-3" />

      <!-- 학 실루엣 -->
      <div class="crane crane-1" />
      <div class="crane crane-2" />
    </div>

    <!-- 상단 배너 -->
    <header class="banner">
      <span class="badge">추석</span>
      <h1 class="title">한가위</h1>
      <span class="badge badge-alt">佳節</span>
    </header>

    <!-- 한복 배색 띠 -->
    <section class="hanbok-stripes" aria-hidden="true">
      <span class="stripe s1" />
      <span class="stripe s2" />
      <span class="stripe s3" />
      <span class="stripe s4" />
      <span class="stripe s5" />
    </section>

    <!-- 메시지 카드 -->
    <section class="card" role="region" aria-label="추석 인사">
      <p class="wish" :key="idx">{{ wishes[idx] }}</p>
      <button class="btn" type="button" @click="next" aria-label="다음 인사 보기">
        다음 인사 보기
      </button>
    </section>

    <!-- 솔잎 장식 -->
    <div class="pine-wrap">
      <div class="pine p1" />
      <div class="pine p2" />
      <div class="pine p3" />
    </div>

    <!-- 각진 지붕 실루엣 -->
    <footer class="roof" aria-hidden="true" />
  </main>
</template>

<style scoped>
/* 전통 한국 색감 참고(오방색/자연 염색 톤)에서 영감 받은 커스텀 팔레트 */
:root {
  --bg-top: #1b2745;    /* 깊은 남색 밤하늘 */
  --bg-btm: #352a3a;    /* 자줏빛 그라디언트 하늘 */
  --moon:   #ffdca8;    /* 누런 달빛(미색) */
  --shine:  #fff2cc;    /* 은은한 달무리 */
  --cloud:  #f1e9e0;    /* 구름(백색에 약간의 온기) */
  --ink:    #2a2a2a;    /* 먹색 텍스트 */
  --s-red:  #ed302b;    /* 단청/한복의 홍색 포인트 */
  --s-blue: #1f5ca8;    /* 청색 */
  --s-yellow:#e1b500;   /* 황색 */
  --s-black:#2d2d2d;    /* 흑색 */
  --s-white:#e8e5df;    /* 백색 */
  --green:  #4a6d3b;    /* 솔잎 녹색 */
  --gold:   #c9a86a;    /* 금사 포인트 */
}

/* 전체 레이아웃 */
.layout {
  min-height: 100dvh;
  display: grid;
  grid-template-rows: auto auto 1fr auto auto;
  background: linear-gradient(180deg, var(--bg-top), var(--bg-btm));
  color: var(--ink);
  overflow: hidden;
  position: relative;
}

/* 하늘/달/구름 레이어 */
.sky {
  position: relative;
  height: 42vh;
}

.moon {
  position: absolute;
  top: 8vh;
  left: 50%;
  transform: translateX(-50%);
  width: 18rem;
  height: 18rem;
  background: radial-gradient(55% 55% at 45% 45%, var(--moon), #f6c96d 60%, #e7b456 100%);
  border-radius: 50%;
  box-shadow: 0 0 30px 8px rgba(255, 220, 168, 0.35);
}
.moon-shine {
  position: absolute;
  inset: -2rem;
  border-radius: 50%;
  background: radial-gradient(60% 60% at 50% 50%, var(--shine), transparent 70%);
  filter: blur(2px);
  opacity: 0.6;
}

/* 구름 */
.cloud {
  position: absolute;
  background: var(--cloud);
  border-radius: 999px;
  filter: blur(0.2px);
  opacity: 0.88;
  box-shadow:
      40px 10px 0 6px var(--cloud),
      90px 5px 0 14px var(--cloud),
      140px 15px 0 8px var(--cloud);
  height: 26px;
  width: 120px;
  animation: float 24s linear infinite;
}
.cloud-1 { top: 16vh; left: 8vw; animation-delay: 0s; }
.cloud-2 { top: 22vh; right: 10vw; animation-delay: 6s; transform: scale(1.15); }
.cloud-3 { top: 28vh; left: 30vw; animation-delay: 12s; transform: scale(0.9); }

@keyframes float {
  0%   { transform: translateX(0) scale(1); }
  50%  { transform: translateX(30px) scale(1.02); }
  100% { transform: translateX(0) scale(1); }
}

/* 학(간단한 종이접기 실루엣 느낌) */
.crane {
  position: absolute;
  width: 0;
  height: 0;
  border-left: 22px solid transparent;
  border-right: 22px solid transparent;
  border-bottom: 36px solid #e9e9e9;
  transform-origin: center bottom;
  filter: drop-shadow(0 2px 2px rgba(0,0,0,0.15));
  animation: glide 16s ease-in-out infinite;
}
.crane::after {
  content: '';
  position: absolute;
  top: -18px;
  left: -3px;
  width: 6px;
  height: 26px;
  background: #e9e9e9;
  transform: rotate(15deg);
  border-radius: 2px;
}
.crane-1 { top: 10vh; left: 18vw; animation-delay: 1s; }
.crane-2 { top: 14vh; right: 22vw; transform: scale(0.9); animation-delay: 3s; }

@keyframes glide {
  0%, 100% { transform: translateY(0) rotate(0deg); }
  50%      { transform: translateY(-6px) rotate(2deg); }
}

/* 상단 배너(서예 느낌 타이포) */
.banner {
  margin: 0 auto;
  margin-top: -2rem;
  display: flex;
  align-items: baseline;
  gap: 1rem;
  justify-content: center;
  color: #f8f6f2;
  text-shadow: 0 1px 2px rgba(0,0,0,0.35);
}
.title {
  font-family: ui-serif, "Pretendard", "Noto Serif KR", "Malgun Gothic", serif;
  font-size: clamp(2.2rem, 5vw, 4rem);
  letter-spacing: 0.08em;
}
.badge {
  font-size: clamp(0.9rem, 2vw, 1.1rem);
  padding: 0.35rem 0.6rem;
  border: 1px solid rgba(248,246,242,0.45);
  border-radius: 4px;
  color: #f8f6f2;
  background: linear-gradient(180deg, rgba(255,255,255,0.08), rgba(0,0,0,0.08));
  backdrop-filter: blur(2px);
}
.badge-alt {
  border-color: rgba(201,168,106,0.65);
  color: #ffe6b0;
}

/* 한복/단청 배색 띠 */
.hanbok-stripes {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  height: 10px;
  margin: 1.2rem auto 0.8rem;
  width: min(720px, 88vw);
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 1px 0 rgba(255,255,255,0.25), 0 4px 10px rgba(0,0,0,0.15) inset;
}
.stripe { display: block; }
.s1 { background: var(--s-blue); }
.s2 { background: var(--s-red); }
.s3 { background: var(--s-yellow); }
.s4 { background: var(--s-black); }
.s5 { background: var(--s-white); }

/* 메시지 카드 */
.card {
  margin: 1.2rem auto 0;
  width: min(720px, 92vw);
  background: rgba(248,246,242,0.9);
  border: 1px solid rgba(0,0,0,0.06);
  border-radius: 14px;
  padding: 1.2rem 1.1rem;
  backdrop-filter: blur(4px);
  box-shadow: 0 6px 24px rgba(0,0,0,0.18);
}
.wish {
  font-family: "Pretendard", "Noto Sans KR", system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
  font-size: clamp(1.05rem, 2.2vw, 1.35rem);
  line-height: 1.65;
  color: #2a2a2a;
  text-align: center;
  margin: 0 0 0.9rem;
}
.btn {
  display: block;
  margin: 0.2rem auto 0;
  padding: 0.6rem 1rem;
  font-size: 0.95rem;
  color: #fff;
  background: linear-gradient(180deg, var(--s-blue), #184b87);
  border: 1px solid #134171;
  border-radius: 10px;
  cursor: pointer;
  transition: transform 0.05s ease, box-shadow 0.2s ease;
  box-shadow: 0 4px 0 #0e3258, 0 10px 16px rgba(0,0,0,0.18);
}
.btn:hover { box-shadow: 0 4px 0 #0e3258, 0 12px 20px rgba(0,0,0,0.22); }
.btn:active { transform: translateY(1px); box-shadow: 0 3px 0 #0e3258, 0 6px 10px rgba(0,0,0,0.2); }

/* 솔잎 장식 */
.pine-wrap {
  position: relative;
  width: min(720px, 92vw);
  margin: 1.1rem auto 0.6rem;
  display: flex;
  justify-content: space-between;
  pointer-events: none;
}
.pine {
  width: 0; height: 0;
  border-left: 8px solid transparent;
  border-right: 8px solid transparent;
  border-bottom: 28px solid var(--green);
  filter: drop-shadow(0 4px 2px rgba(0,0,0,0.12));
  opacity: 0.9;
}
.p1 { transform: rotate(-18deg); }
.p2 { transform: rotate(6deg); }
.p3 { transform: rotate(18deg); }

/* 기와지붕 실루엣 */
.roof {
  height: 38px;
  margin-top: 0.8rem;
  background:
      linear-gradient(180deg, rgba(0,0,0,0.25), rgba(0,0,0,0)) top/100% 12px no-repeat,
      repeating-linear-gradient(90deg, #1c1c1c, #1c1c1c 22px, #141414 22px, #141414 46px);
  box-shadow: 0 -1px 0 rgba(255,255,255,0.12) inset, 0 -8px 16px rgba(0,0,0,0.35) inset;
}

/* 반응형 미세 조정 */
@media (max-width: 480px) {
  .moon { width: 14rem; height: 14rem; top: 9vh; }
  .cloud { opacity: 0.82; }
}
</style>
