### index.html

`html
<!doctype html>
<html lang="vi">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>ĐỀ THI ĐỊNH LƯỢNG HSA - ĐỀ SỐ 5</title>
    <link rel="stylesheet" href="style.css" />
    <script>
      MathJax = {
        tex: { inlineMath: [["$", "$"], ["\\(", "\\)"]] },
        svg: { fontCache: "global" },
      };
    </script>
    <script id="MathJax-script" async
      src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
    </script>
  </head>
  <body>
    <!-- Màn hình chờ / hướng dẫn -->
    <div id="login-screen" class="container">
      <div class="exam-header-block" style="margin-bottom: 20px">
        <div class="exam-header-top" style="border-radius: 8px; border-bottom: 1px solid var(--border-color);">
          <div class="meta-text">BÀI THI ĐÁNH GIÁ NĂNG LỰC HSA · TƯ DUY ĐỊNH LƯỢNG</div>
          <h1 class="exam-title">ĐỀ THI ĐỊNH LƯỢNG HSA - ĐỀ SỐ 5</h1>
          <div class="meta-sub">50 câu hỏi · Trắc nghiệm &amp; Điền đáp án — thang điểm 50</div>
          <hr class="dashed-line" />
        </div>
      </div>
      <div class="card form-card">
        <div class="exam-instructions" style="text-align: left;">
          <h3 style="margin-top: 0; color: var(--navy); font-size: 16px; border-bottom: 2px solid #e2e8f0; padding-bottom: 8px; font-weight: bold;">📋 HƯỚNG DẪN &amp; QUY CHẾ THI</h3>
          <ul style="font-size: 14px; color: #334155; line-height: 1.8; padding-left: 20px; margin-bottom: 16px;">
            <li><strong>Tổng số câu hỏi:</strong> 50 câu (Bao gồm câu hỏi trắc nghiệm 4 lựa chọn và câu hỏi điền đáp án).</li>
            <li><strong>Thang điểm:</strong> Mỗi câu trả lời đúng được <strong>1 điểm</strong> (Tối đa 50 điểm).</li>
            <li><strong>Thời gian làm bài:</strong> 75 phút.</li>
            <li><span style="color: #d97706; font-weight: bold;">⚠️ Lưu ý (Với câu điền đáp án):</span> Dùng dấu phẩy (<code>,</code>) hoặc dấu chấm (<code>.</code>) để phân cách thập phân. VD: <code>1.25</code> hoặc <code>1,25</code></li>
          </ul>
          <div style="background: #fef9c3; border: 1px solid #fde047; border-radius: 6px; padding: 10px 14px; font-size: 13px; color: #854d0e; margin-bottom: 16px;">
            ⚠️ <strong>Quy chế:</strong> Nếu bạn chuyển sang tab hoặc ứng dụng khác trong khi thi, hệ thống sẽ ghi nhận số lần vi phạm và báo cáo về giáo viên.
          </div>
          <button id="btn-start-exam" class="btn-primary" style="width: 100%; padding: 12px; font-size: 16px; font-weight: bold;">
            ✅ Tôi đã đọc hướng dẫn — Bắt đầu thi
          </button>
        </div>
      </div>
      <div class="page-footer">Tư duy định lượng · tự động chấm điểm theo đúng barem &amp; lưu kết quả</div>
    </div>

    <!-- Màn hình làm bài thi -->
    <div id="exam-screen" class="hidden container">
      <div id="board-container" class="board-card">
        <h3>Bảng Điều Hướng</h3>
        <div id="question-board" class="board-wrapper"></div>
      </div>
      <div class="exam-header-block">
        <div class="exam-header-top">
          <div class="meta-text">KIỂM TRA 75 PHÚT · TƯ DUY ĐỊNH LƯỢNG</div>
          <h1 class="exam-title">ĐỀ THI ĐỊNH LƯỢNG HSA - ĐỀ SỐ 5</h1>
          <div class="meta-sub">50 câu hỏi</div>
          <hr class="dashed-line" />
        </div>
        <div class="exam-info-bar sticky">
          <div class="student-info">
            Thí sinh: <strong id="display-name" style="color: white"></strong> ·
            Lớp <strong id="display-class" style="color: white"></strong>
          </div>
          <div class="progress-info"><span id="answered-count">0/50</span> câu đã làm</div>
          <div class="timer-pill">
            <span class="green-dot">●</span> <span id="countdown">75:00</span>
          </div>
          <div class="score-pill hidden" id="score-pill">
            <span class="green-dot">✓</span> Điểm: <span id="review-score">0</span>/50
          </div>
        </div>
      </div>
      <div id="questions-container"></div>
      <div class="submit-container">
        <button id="submit-btn" class="btn-primary">Nộp bài kiểm tra</button>
      </div>
    </div>

    <!-- Màn hình kết quả -->
    <div id="result-screen" class="hidden container">
      <div class="card result-card">
        <h2 style="font-family: var(--font-serif)">Kết Quả Bài Thi</h2>
        <div class="score-display mono-font">Điểm: <span id="final-score"></span>/50</div>
        <p>Số lần rời khỏi màn hình: <span id="cheat-display">0</span></p>
        <p id="firebase-status" style="font-size: 14px; margin-top: 8px; color: #666;">⏳ Đang kết nối hệ thống lưu...</p>
        <button id="review-btn" class="btn-primary">Xem lại bài làm</button>
      </div>
    </div>

    <script type="module" src="script.js"></script>
  </body>
</html>


`

### style.css

`css
:root {
  --bg-color: #f8fafc;
  --grid-color: #e2e8f0;
  --ink: #1e293b;
  --navy: #1e3a8a;
  --blue-text: #2563eb;
  --gray-text: #64748b;
  --border-color: #e2e8f0;
  --font-sans:
    system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  --font-serif: "Times New Roman", Times, serif;
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background-color: var(--bg-color);
  background-image:
    linear-gradient(var(--grid-color) 1px, transparent 1px),
    linear-gradient(90deg, var(--grid-color) 1px, transparent 1px);
  background-size: 25px 25px;
  font-family: var(--font-sans);
  color: var(--ink);
  line-height: 1.6;
}

.hidden {
  display: none !important;
}

.container {
  max-width: 900px;
  margin: 40px auto;
  padding: 0 20px;
}

/* BẢNG ĐIỀU HƯỚNG STICKY NHỎ */
#board-container {
  position: fixed;
  bottom: 30px;
  right: 30px;
  width: 280px;
  max-height: 400px;
  background: #fff;
  border: 1px solid var(--border-color);
  border-radius: 12px;
  padding: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  z-index: 500;
  overflow-y: auto;
}

#board-container h3 {
  font-size: 13px;
  font-weight: bold;
  color: var(--navy);
  margin-bottom: 8px;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.board-legend {
  font-size: 11px;
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-bottom: 10px;
  padding: 8px;
  background: #f8fafc;
  border-radius: 6px;
}

.box {
  width: 18px;
  height: 18px;
  border: 1px solid #ccc;
  border-radius: 4px;
  display: inline-block;
  background: #fff;
}

.box.done {
  background-color: #007bff;
  border-color: #007bff;
}

.box.flagged {
  background-color: #ffc107;
  border-color: #ffc107;
}

.box-label {
  font-size: 11px;
  color: var(--gray-text);
  line-height: 18px;
}

.board-wrapper {
  display: flex;
  flex-direction: column;
  gap: 0;
}

.q-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 6px;
}

.q-box {
  padding: 8px;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
  font-size: 12px;
  background: #fff;
  transition: all 0.2s;
}

.q-box:hover {
  background: #f0f0f0;
  transform: scale(1.05);
}

.q-box.done {
  background-color: #007bff;
  color: white;
  border-color: #007bff;
}

.q-box.flagged {
  background-color: #ffc107;
  color: #333;
  border-color: #ffc107;
  font-weight: bold;
}

/* CARD CHUNG */
.card {
  background: #fff;
  border-radius: 8px;
  padding: 30px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  border: 1px solid var(--border-color);
}

.login-card,
.result-card {
  text-align: center;
  max-width: 500px;
  margin: 80px auto;
}

.form-group input {
  width: 100%;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-size: 16px;
  margin-bottom: 15px;
}

.btn-primary {
  background-color: var(--navy);
  color: #fff;
  border: none;
  padding: 12px 24px;
  font-size: 16px;
  border-radius: 6px;
  cursor: pointer;
  font-weight: bold;
  transition: 0.2s;
}

.btn-primary:hover {
  background-color: #1e3a8a;
  transform: translateY(-2px);
}

.submit-container {
  text-align: center;
  margin: 40px 0 80px 0;
}

/* HEADER BÀI THI */
.exam-header-block {
  margin-bottom: 30px;
}

.exam-header-top {
  background: #fff;
  padding: 25px 30px;
  border: 1px solid var(--border-color);
  border-radius: 12px 12px 0 0;
  border-bottom: none;
}

.meta-text {
  font-family: var(--font-sans);
  font-size: 12px;
  color: var(--gray-text);
  letter-spacing: 2px;
  text-transform: uppercase;
  margin-bottom: 10px;
}

.exam-title {
  font-family: var(--font-serif);
  font-size: 28px;
  color: var(--navy);
  margin-bottom: 10px;
}

.meta-sub {
  font-size: 14px;
  color: var(--gray-text);
}

.dashed-line {
  border: none;
  border-top: 1px dashed #cbd5e1;
  margin-top: 20px;
  position: relative;
}

.dashed-line::after {
  content: "";
  position: absolute;
  right: -5px;
  top: -5px;
  width: 8px;
  height: 8px;
  border: 1px solid #cbd5e1;
  border-radius: 50%;
  background: #fff;
}

/* THANH THÔNG TIN & TIMER */
.exam-info-bar {
  background-color: var(--navy);
  color: #94a3b8;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 30px;
  border-radius: 0 0 12px 12px;
  font-size: 14px;
}

.exam-info-bar.sticky {
  position: sticky;
  top: 0;
  z-index: 100;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
}

.timer-pill {
  background-color: #334155;
  color: #fff;
  padding: 4px 12px;
  border-radius: 20px;
  font-weight: bold;
  font-family: monospace;
  font-size: 16px;
  display: flex;
  align-items: center;
  gap: 6px;
}

.green-dot {
  color: #4ade80;
  font-size: 12px;
}

.timer-danger {
  background-color: #ef4444 !important;
  animation: pulse 1s infinite;
}

@keyframes pulse {
  0%,
  100% {
    opacity: 1;
  }
  50% {
    opacity: 0.7;
  }
}

/* TIÊU ĐỀ PHẦN */
.section-header {
  margin: 40px 0 20px 0;
  border-bottom: 1px solid var(--border-color);
  padding-bottom: 10px;
}

.section-title {
  font-family: var(--font-serif);
  font-size: 22px;
  font-weight: bold;
  color: var(--navy);
  display: flex;
  align-items: center;
  gap: 10px;
}

.badge {
  font-family: var(--font-sans);
  background-color: #e0e7ff;
  color: var(--blue-text);
  font-size: 12px;
  padding: 3px 8px;
  border-radius: 12px;
  font-weight: bold;
}

.section-subtitle {
  font-size: 14px;
  color: var(--gray-text);
  margin-top: 5px;
}

/* CÂU HỎI */
.question-card {
  background: #fff;
  border: 1px solid var(--border-color);
  border-radius: 8px;
  padding: 20px 25px;
  margin-bottom: 15px;
}

.q-layout {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.q-header {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  gap: 12px;
}

.q-num-flag {
  display: flex;
  align-items: center;
  gap: 10px;
  flex-wrap: nowrap;
}

.q-num {
  background: var(--navy);
  color: #fff;
  width: 60px;
  height: 28px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 6px;
  font-weight: bold;
  font-size: 14px;
  flex-shrink: 0;
}

.btn-flag {
  margin-bottom: 10px;
  cursor: pointer;
  padding: 4px 8px;
  width: 70px;
  height: 30px;
  background: #f0f0f0;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.btn-flag:hover {
  border-color: #ffc107;
  color: #ffc107;
  background: #fffbf0;
}

.btn-flag.active {
  background: #ffc107;
  border-color: #ffc107;
  color: #333;
}

.q-content {
  flex: 1;
}

.q-text {
  font-size: 16px;
  margin-bottom: 15px;
  margin-top: 2px;
  line-height: 1.6;
}

.q-image {
  margin: 15px 0;
  display: flex;
  justify-content: center;
}

.q-image img {
  max-width: 100%;
  height: auto;
  border: 1px solid var(--border-color);
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

/* ĐÁP ÁN TRẮC NGHIỆM */
.options-list {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.option-label {
  display: block;
  border: 1px solid var(--border-color);
  border-radius: 8px;
  padding: 12px 15px;
  cursor: pointer;
  transition: 0.2s;
}

.option-label:hover {
  border-color: #93c5fd;
  background: #f8fafc;
}

.option-label input {
  display: none;
}

.option-label.selected {
  border-color: var(--blue-text);
  background: #eff6ff;
}

.opt-letter {
  color: var(--blue-text);
  font-weight: bold;
  margin-right: 10px;
  font-family: var(--font-serif);
}

/* ĐÚNG SAI */
.tf-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 15px;
  border: 1px solid var(--border-color);
  border-radius: 8px;
  margin-bottom: 10px;
}

.tf-controls {
  display: flex;
  gap: 15px;
  flex-shrink: 0;
}

.tf-controls label {
  cursor: pointer;
  font-size: 14px;
}

.short-ans-input {
  width: 100%;
  max-width: 300px;
  padding: 10px;
  border: 1px solid var(--border-color);
  border-radius: 6px;
  font-size: 14px;
}

/* CHẤM ĐIỂM */
.correct-ans {
  background-color: #dcfce7 !important;
  border-color: #22c55e !important;
}

.wrong-ans {
  background-color: #fee2e2 !important;
  border-color: #ef4444 !important;
}

.explanation {
  margin-top: 15px;
  padding: 15px;
  background: #f8fafc;
  border-left: 3px solid var(--navy);
  font-size: 14px;
  border-radius: 4px;
}

.image-placeholder {
  background: #f1f5f9;
  border: 2px dashed #cbd5e1;
  padding: 30px;
  text-align: center;
  color: #64748b;
  margin: 15px 0;
  border-radius: 8px;
}

.page-footer {
  text-align: center;
  font-size: 12px;
  color: var(--gray-text);
  margin-top: 40px;
  padding-top: 20px;
  border-top: 1px solid var(--border-color);
}

.form-note {
  font-size: 13px;
  color: var(--gray-text);
  margin-top: 15px;
  font-style: italic;
}

/* RESPONSIVE */
@media (max-width: 768px) {
  #board-container {
    width: 240px;
    bottom: 20px;
    right: 20px;
  }

  .q-grid {
    grid-template-columns: repeat(3, 1fr);
  }

  .exam-title {
    font-size: 22px;
  }

  .container {
    margin: 20px auto;
  }
}

@media (max-width: 480px) {
  #board-container {
    width: 200px;
    bottom: 10px;
    right: 10px;
    max-height: 300px;
  }

  .q-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .q-num-flag {
    flex-direction: column;
    align-items: flex-start;
  }

  .exam-info-bar {
    flex-direction: column;
    gap: 10px;
    padding: 10px 15px;
  }

  .tf-row {
    flex-direction: column;
    align-items: flex-start;
    gap: 10px;
  }

  .tf-controls {
    width: 100%;
    justify-content: space-around;
  }
}
.score-pill {
  background-color: #16a34a;
  color: #fff;
  padding: 4px 12px;
  border-radius: 20px;
  font-weight: bold;
  font-family: monospace;
  font-size: 16px;
  display: flex;
  align-items: center;
  gap: 6px;
}

.score-pill .green-dot {
  color: #fff;
}


#toast {
  position: fixed;
  top: 70px;
  left: 50%;
  transform: translateX(-50%) translateY(-20px);
  background: #b91c1c;
  color: #fff;
  padding: 10px 20px;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 600;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.25);
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.25s, transform 0.25s;
  z-index: 10000;
}
#toast.show {
  opacity: 1;
  transform: translateX(-50%) translateY(0);
}


`

### script.js

`javascript
import { examData } from "./data.js";
import { db, ref, push, set, update, serverTimestamp } from "./firebase-config.js";
import { getMTSeduSession, showLoginRequired, insertBackButton } from "./mtsedu-auth.js";

const loginScreen = document.getElementById("login-screen");
const examScreen = document.getElementById("exam-screen");
const resultScreen = document.getElementById("result-screen");
const questionsContainer = document.getElementById("questions-container");
const questionBoard = document.getElementById("question-board");
const submitBtn = document.getElementById("submit-btn");

// ===== CHỈ THAY DÒNG NÀY =====
const MA_DE       = "HSA_DINHLUONG_DE5";
const DRAFT_KEY   = "examDraft_HSA_DINHLUONG_DE5";
const EXAM_MINUTES = 75;
const RETURN_HASH = "#math";
// ================================

let timeRemaining = EXAM_MINUTES * 60;
let timerInterval;
let userAnswers = {};
let flaggedQuestions = {};
let isFinished = false;
let cheatCount = 0;
let studentName = "";
let studentClass = "";

window.addEventListener("DOMContentLoaded", () => {
  const session = getMTSeduSession();
  const btnStart = document.getElementById("btn-start-exam");
  if (btnStart) {
    btnStart.addEventListener("click", () => {
      if (!session) {
        const loginCard = loginScreen.querySelector(".form-card") || loginScreen.querySelector(".card");
        if (loginCard) showLoginRequired(loginCard, RETURN_HASH);
        return;
      }
      const draft = JSON.parse(localStorage.getItem(DRAFT_KEY));
      if (draft && !draft.isFinished && draft.studentName === studentName) {
        loadDraftAndContinue(draft);
      } else {
        startExamDirectly();
      }
    });
  }

  if (!session) return;
  studentName = session.displayName || session.username;
  studentClass = session.username;
  insertBackButton();
});

function startExamDirectly() {
  userAnswers = {}; flaggedQuestions = {}; cheatCount = 0; isFinished = false;
  localStorage.removeItem(DRAFT_KEY);
  timeRemaining = EXAM_MINUTES * 60;
  document.getElementById("display-name").innerText = studentName;
  document.getElementById("display-class").innerText = studentClass;
  loginScreen.classList.add("hidden");
  examScreen.classList.remove("hidden");
  renderExam(); restoreDOMState(); renderBoard(); startTimer(); setupAntiCheat();
}

function loadDraftAndContinue(draft) {
  studentName = draft.studentName || studentName;
  studentClass = draft.studentClass || studentClass;
  timeRemaining = draft.timeRemaining;
  userAnswers = draft.userAnswers || {};
  flaggedQuestions = draft.flaggedQuestions || {};
  cheatCount = draft.cheatCount || 0;
  document.getElementById("display-name").innerText = studentName;
  document.getElementById("display-class").innerText = studentClass;
  loginScreen.classList.add("hidden");
  examScreen.classList.remove("hidden");
  renderExam(); restoreDOMState(); renderBoard(); startTimer(); setupAntiCheat();
}

function renderExam() {
  questionsContainer.innerHTML = "";

  const header = document.createElement("div");
  header.className = "section-header";
  header.innerHTML = `
    <div class="section-title">Phần thi: Tư duy định lượng <span class="badge">50 điểm</span></div>
    <div class="section-subtitle">Mỗi câu đúng được 1 điểm. Gồm trắc nghiệm 4 lựa chọn và điền đáp án.</div>`;
  questionsContainer.appendChild(header);

  let qCounter = 1;

  examData.forEach((q) => {
    const card = document.createElement("div");
    card.className = "question-card";
    card.id = `q-card-${q.id}`;

    let html = `<div class="q-layout"><div class="q-header"><div class="q-num-flag">
      <div class="q-num">Câu ${qCounter}</div>
      <button class="btn-flag ${flaggedQuestions[q.id] ? "active" : ""}" data-id="${q.id}" title="Đánh dấu">
        ${flaggedQuestions[q.id] ? "★" : "☆"}</button>
    </div></div><div class="q-content">
    <div class="q-text">${q.question}</div>
    ${q.image ? `<div class="q-image"><img src="${q.image}" alt="Hình câu ${qCounter}"></div>` : ""}`;

    if (q.type === "mcq") {
      html += `<div class="options-list">`;
      q.options.forEach((opt, idx) => {
        html += `<label class="option-label" id="lbl-${q.id}-${idx}">
          <input type="radio" name="ans-${q.id}" value="${idx}">
          <span class="opt-letter">${["A","B","C","D"][idx]}.</span> ${opt}</label>`;
      });
      html += `</div>`;
    } else if (q.type === "fill") {
      html += `<input type="text" class="short-ans-input" name="ans-${q.id}" placeholder="Nhập đáp án...">`;
    }

    html += `<div class="explanation hidden" id="exp-${q.id}"><strong>Hướng dẫn giải:</strong> ${q.explanation}</div></div></div>`;
    card.innerHTML = html;
    questionsContainer.appendChild(card);
    qCounter++;
  });

  document.querySelectorAll(".btn-flag").forEach((btn) => {
    btn.addEventListener("click", (e) => {
      e.preventDefault();
      const qid = e.target.closest(".btn-flag").getAttribute("data-id");
      flaggedQuestions[qid] = !flaggedQuestions[qid];
      e.target.closest(".btn-flag").classList.toggle("active");
      e.target.closest(".btn-flag").innerText = flaggedQuestions[qid] ? "★" : "☆";
      updateBoard(); saveDraft();
    });
  });

  document.querySelectorAll("input").forEach((input) => {
    input.addEventListener("change", (e) => {
      const name = e.target.name;
      if (name.startsWith("ans-") && e.target.type === "radio") {
        const qid = name.replace("ans-", "");
        document.querySelectorAll(`input[name="${name}"]`).forEach((r) =>
          r.closest(".option-label").classList.remove("selected"));
        e.target.closest(".option-label").classList.add("selected");
        userAnswers[qid] = parseInt(e.target.value);
      } else if (e.target.type === "text") {
        const qid = name.replace("ans-", "");
        userAnswers[qid] = e.target.value;
      }
      updateBoard(); saveDraft();
    });
  });

  if (window.MathJax) MathJax.typesetPromise();
}

function renderBoard() {
  if (!questionBoard) return;
  const legend = document.createElement("div");
  legend.className = "board-legend";
  legend.innerHTML = `
    <span class="box"></span><span class="box-label">Chưa làm</span>
    <span class="box done"></span><span class="box-label">Đã làm</span>
    <span class="box flagged"></span><span class="box-label">Đánh dấu</span>`;
  questionBoard.appendChild(legend);

  const grid = document.createElement("div");
  grid.className = "q-grid";
  grid.id = "q-grid-inner";
  questionBoard.appendChild(grid);

  examData.forEach((q, index) => {
    const box = document.createElement("button");
    box.className = "q-box"; box.id = `box-${q.id}`; box.innerText = index + 1; box.type = "button";
    box.addEventListener("click", (e) => {
      e.preventDefault();
      document.getElementById(`q-card-${q.id}`).scrollIntoView({ behavior: "smooth", block: "center" });
    });
    grid.appendChild(box);
  });
  updateBoard();
}

function updateBoard() {
  let answeredCount = 0;
  examData.forEach((q) => {
    let answered = false;
    if (q.type === "mcq" && userAnswers[q.id] !== undefined) answered = true;
    if (q.type === "fill" && userAnswers[q.id] && userAnswers[q.id].trim() !== "") answered = true;

    if (answered) answeredCount++;
    if (questionBoard) {
      const box = document.getElementById(`box-${q.id}`);
      if (box) {
        box.className = "q-box";
        if (flaggedQuestions[q.id]) box.classList.add("flagged");
        else if (answered) box.classList.add("done");
      }
    }
  });
  const countEl = document.getElementById("answered-count");
  if (countEl) countEl.innerText = `${answeredCount}/${examData.length}`;
}

function saveDraft() {
  localStorage.setItem(DRAFT_KEY, JSON.stringify({
    studentName, studentClass, timeRemaining,
    userAnswers, flaggedQuestions, cheatCount, isFinished,
    lastSaved: new Date().toISOString(),
  }));
}

function restoreDOMState() {
  document.querySelectorAll("input").forEach((input) => {
    const name = input.name;
    if (!name) return;
    if (input.type === "radio" && name.startsWith("ans-")) {
      const qid = name.replace("ans-", "");
      if (userAnswers[qid] == input.value) {
        input.checked = true;
        input.closest(".option-label").classList.add("selected");
      }
    } else if (input.type === "text") {
      const qid = name.replace("ans-", "");
      input.value = userAnswers[qid] || "";
    }
  });
}

let warned30 = false;

function showToast(msg) {
  let t = document.getElementById("toast");
  if (!t) {
    t = document.createElement("div");
    t.id = "toast";
    document.body.appendChild(t);
  }
  t.textContent = msg;
  t.classList.add("show");
  setTimeout(() => t.classList.remove("show"), 5000);
}

function startTimer() {
  const endAt = Date.now() + timeRemaining * 1000;
  timerInterval = setInterval(() => {
    timeRemaining = Math.max(0, Math.round((endAt - Date.now()) / 1000));
    saveDraft();
    const m = Math.floor(timeRemaining / 60).toString().padStart(2, "0");
    const s = (timeRemaining % 60).toString().padStart(2, "0");
    document.getElementById("countdown").innerText = `${m}:${s}`;
    if (timeRemaining <= 30 && !warned30) {
      warned30 = true;
      showToast("⚠️ Cảnh báo: Chỉ còn 30 giây!");
      document.querySelector(".timer-pill").classList.add("timer-danger");
    }
    if (timeRemaining <= 0) { clearInterval(timerInterval); submitExam(); }
  }, 1000);
}

function setupAntiCheat() {
  window.addEventListener("beforeunload", (e) => {
    if (!isFinished) { e.preventDefault(); e.returnValue = "Bạn chưa nộp bài!"; }
  });
  window.addEventListener("pagehide", () => { if (!isFinished) saveDraft(); });
  document.addEventListener("visibilitychange", () => {
    if (document.hidden && !isFinished) { cheatCount++; saveDraft(); }
  });
}

submitBtn.addEventListener("click", () => {
  if (confirm("Bạn có chắc muốn nộp bài?")) submitExam();
});

function parseNumber(str) {
  const t = String(str ?? "").trim().replace(/\s+/g, "").replace(",", ".");
  if (t === "") return NaN;
  const frac = t.match(/^(-?\d+(?:\.\d+)?)\/(-?\d+(?:\.\d+)?)$/);
  if (frac) return Number(frac[2]) === 0 ? NaN : Number(frac[1]) / Number(frac[2]);
  return /^-?\d+(?:\.\d+)?$/.test(t) ? Number(t) : NaN;
}

function isFillCorrect(userInput, correct) {
  const u = String(userInput ?? "").trim().toLowerCase().replace(/\s+/g, "");
  const c = String(correct).trim().toLowerCase().replace(/\s+/g, "");
  if (u === "") return false;
  if (u === c) return true;
  const un = parseNumber(u), cn = parseNumber(c);
  return !isNaN(un) && !isNaN(cn) && Math.abs(un - cn) < 1e-9;
}

function submitExam() {
  isFinished = true; clearInterval(timerInterval);
  document.querySelectorAll("input, .btn-flag").forEach((el) => (el.disabled = true));
  submitBtn.style.display = "none";
  const timerPill = document.querySelector(".timer-pill");
  if (timerPill) timerPill.classList.remove("timer-danger");

  let totalScore = 0;

  examData.forEach((q) => {
    document.getElementById(`exp-${q.id}`).classList.remove("hidden");

    if (q.type === "mcq") {
      const selected = userAnswers[q.id];
      document.getElementById(`lbl-${q.id}-${q.correctAnswer}`).classList.add("correct-ans");
      if (selected === q.correctAnswer) {
        totalScore += 1;
      } else if (selected !== undefined) {
        document.getElementById(`lbl-${q.id}-${selected}`).classList.add("wrong-ans");
      }
    } else if (q.type === "fill") {
      const input = document.querySelector(`input[name="ans-${q.id}"]`);
      if (isFillCorrect(userAnswers[q.id], q.correctAnswer)) {
        totalScore += 1;
        input.classList.add("correct-ans");
      } else {
        input.classList.add("wrong-ans");
      }
    }
  });

  const scorePill = document.getElementById("score-pill");
  document.querySelector(".timer-pill")?.classList.add("hidden");
  if (scorePill) {
    scorePill.classList.remove("hidden");
    document.getElementById("review-score").innerText = totalScore.toFixed(0);
  }

  saveExamResultToFirebase(totalScore, cheatCount);
  document.getElementById("final-score").innerText = totalScore.toFixed(0);
  document.getElementById("cheat-display").innerText = cheatCount;
  examScreen.classList.add("hidden");
  resultScreen.classList.remove("hidden");
  localStorage.removeItem(DRAFT_KEY);
}

async function saveExamResultToFirebase(tongDiem, soLanThoat) {
  const statusEl = document.getElementById("firebase-status");
  if (statusEl) statusEl.innerText = "⏳ Đang đồng bộ kết quả lên MTSedu...";
  try {
    const session = getMTSeduSession();
    const userId = session ? session.id : null;
    const resultData = {
      hoTen: studentName, lop: studentClass, maDe: MA_DE,
      tongDiem, soLanThoat,
      userId: userId || "unknown",
      thoiGianNop: new Date().toISOString(),
      serverTimestamp: serverTimestamp(),
    };
    const updates = {};
    const newResultId = push(ref(db, `testResults/${MA_DE}`)).key;
    updates[`testResults/${MA_DE}/${newResultId}`] = resultData;
    if (userId) updates[`users/${userId}/results/${newResultId}`] = resultData;
    await update(ref(db), updates);
    if (statusEl) { statusEl.style.color = "green"; statusEl.innerText = "✅ Kết quả đã được đồng bộ thành công!"; }
  } catch (error) {
    if (statusEl) { statusEl.style.color = "red"; statusEl.innerText = "❌ Lỗi: " + error.message; }
  }
}

document.getElementById("review-btn").addEventListener("click", () => {
  resultScreen.classList.add("hidden");
  examScreen.classList.remove("hidden");
  window.scrollTo({ top: 0, behavior: "smooth" });
});



`

### data.js

`javascript
export const examData = [
  {
    "id": "q1",
    "type": "fill",
    "question": "Có bao nhiêu giá trị nguyên dương của $m$ để hàm số $y = \\frac{x^2 - 4x + m + 2 + 3\\sqrt{x^2 - 4x}}{\\sqrt{x^2 - 4x} + 2}$ nghịch biến trên khoảng $(-4; 0)$?\n(Nhập đáp án vào ô trống)",
    "correctAnswer": "4",
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q2",
    "type": "mcq",
    "question": "Đạo hàm của hàm số $y = \\tan x - \\cot x$ là",
    "options": [
      "$y' = \\frac{1}{\\cos^2 2x}$.",
      "$y' = \\frac{1}{\\sin^2 2x}$.",
      "$y' = \\frac{4}{\\cos^2 2x}$.",
      "$y' = \\frac{4}{\\sin^2 2x}$."
    ],
    "correctAnswer": 3,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q3",
    "type": "mcq",
    "question": "Cho hình chóp S.ABC có đáy tam giác vuông tại $A$ có $AB=a, BC=a\\sqrt{5}$. Biết $SA=3a$ và $SA \\perp (ABC)$. Tính khoảng cách từ $A$ đến mặt phẳng $(SBC)$.",
    "options": [
      "$\\frac{6a}{7}$.",
      "$\\frac{\\sqrt{2}a}{2}$.",
      "$\\frac{3a}{7}$.",
      "$\\frac{\\sqrt{5}a}{5}$."
    ],
    "correctAnswer": 0,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q4",
    "type": "fill",
    "question": "Trong không gian Oxyz, cho mặt phẳng $(P): 2x + 3y + z - 11 = 0$, mặt cầu $(S)$ có tâm $I(1; -2; 1)$ và tiếp xúc với mặt phẳng $(P)$ tại điểm $H(a; b; c)$. Tính $T = a + b + c$.",
    "correctAnswer": "6",
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q5",
    "type": "mcq",
    "question": "Cho hình chóp $S.ABC$ có SA vuông góc với đáy, mặt phẳng $(SAB)$ vuông góc với mặt phẳng $(SBC)$, góc giữa hai mặt phẳng $(SAC)$ và $(SBC)$ là $60^\\circ, SB=a\\sqrt{2}, BSC=45^\\circ$. Thể tích khối chóp $S.ABC$ theo $a$ là",
    "options": [
      "$V = \\frac{a^3\\sqrt{2}}{15}$.",
      "$V = 2\\sqrt{3}a^3$.",
      "$V = 2\\sqrt{2}a^3$.",
      "$V = \\frac{2a^3\\sqrt{3}}{15}$."
    ],
    "correctAnswer": 3,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q6",
    "type": "mcq",
    "question": "Có tất cả bao nhiêu giá trị nguyên của $x$ để tồn tại duy nhất giá trị nguyên của $y$ sao cho thỏa mãn bất phương trình $e^{2y} + 4x^2y - y^2 + x > \\ln(x^2 - y)$?",
    "options": [
      "1.",
      "2.",
      "3.",
      "4."
    ],
    "correctAnswer": 0,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q7",
    "type": "mcq",
    "question": "Tập nghiệm của bất phương trình $\\left(\\frac{e}{\\pi}\\right)^x > 1$ là",
    "options": [
      "$\\emptyset$.",
      "$(-\\infty; 0)$.",
      "$(0; +\\infty)$.",
      "$[0; +\\infty)$."
    ],
    "correctAnswer": 1,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q8",
    "type": "fill",
    "question": "Cho hàm số $y = x^3 - 3x^2 - (m^2 - 2)x + m^2 (C_m)$. Biết rằng đồ thị hàm số cắt trục hoành tại ba điểm phân biệt $A, B, C$ ($x_A < x_B < x_C$) và có hai điểm cực trị M, N. Số các giá trị của tham số $m$ để $MN = AC$ là?",
    "correctAnswer": "2",
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q9",
    "type": "mcq",
    "question": "Cho hình chóp S.ABCD có đáy ABCD là hình vuông cạnh $a$, cạnh bên SA vuông góc với đáy và $SA = a\\sqrt{3}$. Khoảng cách từ $D$ đến mặt phẳng $(SBC)$ bằng",
    "options": [
      "$\\frac{2a\\sqrt{5}}{5}$.",
      "$a\\sqrt{3}$.",
      "$\\frac{a}{2}$.",
      "$\\frac{a\\sqrt{3}}{2}$."
    ],
    "correctAnswer": 3,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q10",
    "type": "mcq",
    "question": "Ông Đức gửi ngân hàng số tiền 500.000.000 đồng loại kỳ hạn 6 tháng với lãi suất 5,6% trên một năm theo thể thức lãi kép (tức là nếu đến kỳ hạn người gửi không rút lãi ra thì tiền lãi được tính vào vốn của kỳ kế tiếp). Hỏi sau 3 năm 9 tháng ông Đức nhận được số tiền (làm tròn đến hàng nghìn) cả gốc lẫn lãi là bao nhiêu? Biết rằng ông Đức không rút cả gốc lẫn lãi trong các kỳ hạn trước đó và nếu rút trước kỳ hạn thì ngân hàng trả lãi suất theo loại không kỳ hạn 0,00027% trên một ngày. (Một tháng tính 30 ngày).",
    "options": [
      "606.627.000 đồng.",
      "623.613.000 đồng.",
      "606.775.000 đồng.",
      "611.764.000 đồng."
    ],
    "correctAnswer": 2,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q11",
    "type": "mcq",
    "question": "Trong các nhị thức dưới đây, nhị thức nào chứa số hạng $C_n^k.(5x)^2 \\left( -6y^2 \\right)^7$ ($k \\le n; k, n \\in \\mathbb{N}$) ?",
    "options": [
      "$\\left(5x - 6y^2\\right)^{16}$.",
      "$\\left(5x - 6y^2\\right)^{11}$.",
      "$\\left(5x - 6y^2\\right)^{9}$.",
      "$\\left(5x - 6y^2\\right)^{18}$."
    ],
    "correctAnswer": 2,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q12",
    "type": "fill",
    "question": "Cho hàm số $f(x) = -x^3 + 3x$ và $g(x) = |f(2 + \\sin x) + m|$ ($m$ là tham số thực). Gọi $S$ là tập các giá trị của tham số $m$ để $\\max g(x) + \\min g(x) = 50$. Tổng các phần tử của $S$ bằng?",
    "correctAnswer": "16",
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q13",
    "type": "mcq",
    "question": "Cho hình chóp S.ABCD có đáy là hình bình hành. Các điểm M, N, P lần lượt là trung điểm các cạnh SA, BC, CD. Gọi I, J lần lượt là giao điểm của NP với AB, AD. Kéo dài MI cắt SB tại $E$, kéo dài MJ cắt SD tại $F$. Gọi $k = \\frac{EF}{IJ}$, giá trị của $k$ là?",
    "options": [
      "$k = \\frac{2}{3}$",
      "$k = \\frac{1}{9}$",
      "$k = \\frac{1}{3}$",
      "$k = \\frac{2}{9}$"
    ],
    "correctAnswer": 3,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q14",
    "type": "mcq",
    "question": "Cho hàm số $y = f(x)$ xác định trên $\\mathbb{R}$ và có đạo hàm $f'(x)$. Đồ thị hàm số $y = f'(x)$ được cho như hình bên dưới. Biết rằng $f(0) + f(1) - 2f(2) = f(4) - f(3)$. Giá trị nhỏ nhất của hàm số $y = f(x)$ trên đoạn $[0; 4]$ là?",
    "options": [
      "$f(4)$",
      "$f(3)$",
      "$f(2)$",
      "$f(1)$"
    ],
    "correctAnswer": 0,
    "explanation": "Chi tiết giải...",
    "image": "cau_14.png"
  },
  {
    "id": "q15",
    "type": "fill",
    "question": "Dãy số $\\begin{cases} u_1 = \\sqrt{2} \\\\ u_{n+1} = \\sqrt{u_n + 2} \\end{cases}$ bị chặn trên bởi $a$. Khi đó $a = ?$",
    "correctAnswer": "2",
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q16",
    "type": "mcq",
    "question": "Cho phương trình $4^{|x|} - (m + 1)2^{|x|} + m = 0$. Điều kiện của $m$ để phương trình có đúng 3 nghiệm phân biệt là:",
    "options": [
      "$m > 0, m \\ne 1$.",
      "$m \\ge 1$.",
      "$m > 1$.",
      "$m > 0$."
    ],
    "correctAnswer": 2,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q17",
    "type": "fill",
    "question": "Gọi giá trị lớn nhất và giá trị nhỏ nhất của của hàm số $y = 3 - 2\\cos 2x - \\cos^2 2x$ lần lượt là M, m. Tính giá trị biểu thức $2024M + 2025m$.",
    "correctAnswer": "8096",
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q18",
    "type": "mcq",
    "question": "Trong môi trường nuôi cấy ổn định người ta nhận thấy rằng: cứ sau đúng 5 ngày số lượng loài của vi khuẩn A tăng lên gấp đôi, còn sau đúng 10 ngày số lượng loài của vi khuẩn B tăng lên gấp ba. Giả sử ban đầu có 50 con vi khuẩn A và 100 con vi khuẩn B, hỏi sau bao nhiêu ngày nuôi cấy trong môi trường đó thì số lượng vi khuẩn của cả hai loài bằng 20900 con, biết rằng tốc độ tăng trưởng của mỗi loài ở mọi thời điểm là như nhau?",
    "options": [
      "20 ngày.",
      "30 ngày.",
      "40 ngày.",
      "50 ngày."
    ],
    "correctAnswer": 2,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q19",
    "type": "fill",
    "question": "Cho hình chóp $S.ABCD$ có đáy $ABCD$ là hình bình hành. Gọi $M$ là điểm thuộc cạnh $SD$ sao cho $SM = \\frac{2}{3}SD$. Mặt phẳng chứa $AM$ và song song với $BD$ cắt cạnh $SC$ tại $K$. Tính tỷ số $\\frac{SK}{SC}$.",
    "correctAnswer": "1/2",
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q20",
    "type": "fill",
    "question": "Một bình hoa dạng khối tròn xoay được tạo thành khi quay hình phẳng giới hạn bởi đồ thị hàm số $y = -\\sin x + 2$ và trục Ox (tham khảo hình vẽ bên dưới). Biết đáy bình hoa là hình tròn có bán kính bằng 2dm, miệng bình hoa là đường tròn bán kính bằng 1.5dm. Bỏ qua độ dày của bình hoa, tính thể tích của bình hoa. (kết quả làm tròn đến hàng đơn vị, đơn vị: dm³)",
    "correctAnswer": "103",
    "explanation": "Chi tiết giải...",
    "image": "cau_20.png"
  },
  {
    "id": "q21",
    "type": "fill",
    "question": "Trong không gian $Oxyz$, cho hai điểm $A(1;1;3), B(5;2;-1)$ và hai điểm $M, N$ thay đổi thuộc mặt phẳng $(Oxy)$ sao cho điểm $I(1;2;0)$ luôn là trung điểm của $MN$. Tính $T = 2x_M - 4x_N + 7y_M - y_N$ khi biểu thức $P = MA^2 + 2NB^2 + \\vec{MA}.\\vec{NB}$ đạt giá trị nhỏ nhất.",
    "correctAnswer": "-10",
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q22",
    "type": "mcq",
    "question": "Cho tam giác $ABC$ có $AB=7, AC=5, \\widehat{A}=60^\\circ$. Tính độ dài trung tuyến $AM$.",
    "options": [
      "$\\frac{\\sqrt{101}}{2}$",
      "$\\sqrt{39}$",
      "$\\frac{\\sqrt{109}}{2}$",
      "$\\sqrt{27}$"
    ],
    "correctAnswer": 2,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q23",
    "type": "mcq",
    "question": "Cho các đường thẳng $d_1: x+2y-3=0, d_2: 3x-4y+1=0$ và $\\Delta: x+3y-10=0$. Phương trình đường thẳng $d$ đi qua giao điểm của hai đường thẳng $d_1, d_2$ và song song với đường thẳng $\\Delta$ là:",
    "options": [
      "$x+y-4=0$",
      "$x+3y+4=0$",
      "$x+y+4=0$",
      "$x+3y-4=0$"
    ],
    "correctAnswer": 3,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q24",
    "type": "mcq",
    "question": "Cho hình chóp $S.ABCD$, đáy $ABCD$ là hình chữ nhật với $AB=3, BC=4$, tam giác $SAC$ nằm trong mặt phẳng vuông góc với đáy, $d(C; SA)=4$. Tính côsin của góc tạo bởi hai mặt phẳng $(SAB)$ và $(SAC)$.",
    "options": [
      "$\\frac{5\\sqrt{34}}{34}$",
      "$\\frac{3\\sqrt{17}}{17}$",
      "$\\frac{2\\sqrt{34}}{17}$",
      "$\\frac{3\\sqrt{34}}{34}$"
    ],
    "correctAnswer": 3,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q25",
    "type": "fill",
    "question": "Bảng tần số ghép nhóm dưới đây thống kê số giờ học của các học sinh lớp 10A như sau: Biết thời gian học của học sinh học ít nhất là 4 giờ 20 phút, thời gian học của học sinh học nhiều nhất là 8 giờ 50 phút. Giả sử khoảng biến thiên của mẫu số liệu ghép nhóm bằng $\\frac{a}{b}$ lần khoảng biến thiên của mẫu số liệu gốc ($\\frac{a}{b}$ là phân số tối giản). Tính $a^3+b^3$.",
    "correctAnswer": "1729",
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q26",
    "type": "mcq",
    "question": "Dựa vào thông tin sau và trả lời các câu hỏi từ câu 26 - 28:\nỞ một thị xã, tỉ lệ mắc căn bệnh M là 22%. Chính quyền thị xã đó muốn biết danh sách những người bị mắc bệnh nên đã tổ chức xét nghiệm cho toàn bộ người dân. Tuy nhiên bộ “test” được sử dụng trong phương pháp xét nghiệm này có những sai sót nhất định:\nNếu một người không bị bệnh thì xác suất bộ “test” cho ra kết quả dương tính là 10%.\nNếu bộ “test” cho ra kết quả dương tính thì xác suất bị bệnh là 70%.\n\nCâu 26:\nNếu một người không bị bệnh thì xác suất bộ “test” cho ra kết quả chính xác là bao nhiêu?",
    "options": [
      "10%",
      "78%",
      "70%",
      "90%"
    ],
    "correctAnswer": 3,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q27",
    "type": "mcq",
    "question": "Xác suất để bộ “test” cho ra kết quả dương tính khi xét nghiệm người bị bệnh là:",
    "options": [
      "70%",
      "82,73%",
      "84,35%",
      "80,18%"
    ],
    "correctAnswer": 1,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q28",
    "type": "mcq",
    "question": "Xác suất chẩn đoán đúng của bộ “test” là:",
    "options": [
      "88,4%",
      "81,8%",
      "96,2%",
      "74%"
    ],
    "correctAnswer": 0,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q29",
    "type": "mcq",
    "question": "Cho các hàm số $f(x)$ và $F(x)$ liên tục trên $\\mathbb{R}$ thỏa $F'(x)=f(x), \\forall x \\in \\mathbb{R}$. Tính $\\int\\limits_{0}^{1}f(x)dx$ biết $F(0)=2, F(1)=6$.",
    "options": [
      "$\\int\\limits_{0}^{1}f(x)dx = -4$",
      "$\\int\\limits_{0}^{1}f(x)dx = 8$",
      "$\\int\\limits_{0}^{1}f(x)dx = -8$",
      "$\\int\\limits_{0}^{1}f(x)dx = 4$"
    ],
    "correctAnswer": 3,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q30",
    "type": "fill",
    "question": "Tính giới hạn $\\lim\\limits_{x \\to -\\infty} \\frac{\\sqrt{x^2+2x}+3x}{\\sqrt{4x^2+1}-x+2}$.",
    "correctAnswer": "-2/3",
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q31",
    "type": "mcq",
    "question": "Cho hàm số $f(x)$ có đạo hàm và liên tục trên $\\mathbb{R}$ và bảng xét dấu đạo hàm như sau:\n\nKhẳng định nào sau đây về số cực trị của hàm số $g(x) = f(x^2+1)+x^2-x^3+x^4$ là đúng?",
    "options": [
      "Có hai cực đại và chỉ có một cực tiểu.",
      "Có hai cực tiểu và chỉ có một cực đại.",
      "Có đúng một cực tiểu và không có cực đại.",
      "Có đúng một cực đại và không có cực tiểu."
    ],
    "correctAnswer": 2,
    "explanation": "Chi tiết giải...",
    "image": "cau_31.png"
  },
  {
    "id": "q32",
    "type": "mcq",
    "question": "Cho hàm số $f(x) = ax^3+bx^2+cx+d \\ (a,b,c,d \\in \\mathbb{R})$. Đồ thị của hàm số $y=f(x)$ như hình vẽ bên. Số nghiệm thực của phương trình $3f(x)+4=0$ là?",
    "options": [
      "3",
      "0",
      "2",
      "1"
    ],
    "correctAnswer": 0,
    "explanation": "Chi tiết giải...",
    "image": "cau_32.png"
  },
  {
    "id": "q33",
    "type": "mcq",
    "question": "Cho hàm số $f(x)$ có đạo hàm trên $\\mathbb{R}$ và $e^{2x+1}$ là một nguyên hàm của hàm số $e^x . f'(x)$ trên $\\mathbb{R}$ và $f(0)=1$. Khi đó $f(1)$ bằng:",
    "options": [
      "$\\frac{e^3-e+2}{2}$",
      "$e^2-e+1$",
      "$2e^2-2e+1$",
      "$2e-1$"
    ],
    "correctAnswer": 2,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q34",
    "type": "mcq",
    "question": "Trong không gian Oxyz, cho điểm $A(1;1;1)$, mặt phẳng $(P): x+y+z-3=0$ và đường thẳng $d: \\frac{x-2}{1} = \\frac{y}{2} = \\frac{z}{-1}$. Xét đường thẳng $\\Delta$ qua A, nằm trong (P) và cách đường thẳng d một khoảng cách lớn nhất. Đường thẳng $\\Delta$ đi qua điểm nào dưới đây?",
    "options": [
      "$M(2;1;0)$",
      "$N(1;-1;3)$",
      "$P(-3;3;3)$",
      "$Q(1;2;4)$"
    ],
    "correctAnswer": 1,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q35",
    "type": "mcq",
    "question": "Cho hàm số $f(x) = ax^4+bx^2+c$ có đồ thị như hình vẽ. Biết rằng $f(x)$ đạt cực trị tại các điểm $x_1; x_2; x_3$ thỏa mãn $x_3 = x_1+2$ và $f(x_1) + f(x_3) + \\frac{2}{3}f(x_2)=0$. Gọi $S_1, S_2, S_3, S_4$ là diện tích các hình phẳng trong hình vẽ bên. Tỉ số $\\frac{S_1+S_2}{S_3+S_4}$ gần nhất với kết quả nào dưới đây?",
    "options": [
      "0,8",
      "0,6",
      "0,7",
      "0,9"
    ],
    "correctAnswer": 1,
    "explanation": "Chi tiết giải...",
    "image": "cau_35.png"
  },
  {
    "id": "q36",
    "type": "mcq",
    "question": "Cho ba điểm $A(1;2;-1), B(2;-1;3), C(-3;5;1)$. Tìm tọa độ điểm D sao cho ABCD là hình bình hành?",
    "options": [
      "$D=(-4;8;-3)$.",
      "$D=(-2;8;-3)$.",
      "$D=(-2;2;5)$.",
      "$D=(-4;8;-5)$."
    ],
    "correctAnswer": 0,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q37",
    "type": "mcq",
    "question": "Cho hàm số $y=f(x)$ có bảng biến thiên như hình vẽ:\n\nHàm số đã cho nghịch biến trên khoảng nào dưới đây?",
    "options": [
      "$(-\\infty;1)$",
      "$(1;3)$",
      "$(1;+\\infty)$",
      "$(-\\infty;2)$"
    ],
    "correctAnswer": 1,
    "explanation": "Chi tiết giải...",
    "image": "cau_37.png"
  },
  {
    "id": "q38",
    "type": "mcq",
    "question": "Trong không gian Oxyz, cho hai điểm $A(1;-2;-3), B(-1;4;1)$ và đường thẳng $d: \\frac{x+2}{1} = \\frac{y-2}{-1} = \\frac{z+3}{2}$. Phương trình đường thẳng $\\Delta$ đi qua trung điểm của đoạn AB và song song với đường thẳng d là?",
    "options": [
      "$\\Delta: \\frac{x}{1} = \\frac{y-2}{-1} = \\frac{z+2}{2}$.",
      "$\\Delta: \\frac{x}{1} = \\frac{y-1}{-1} = \\frac{z+1}{2}$.",
      "$\\Delta: \\frac{x-1}{1} = \\frac{y-1}{-1} = \\frac{z+1}{2}$.",
      "$\\Delta: \\frac{x}{1} = \\frac{y-1}{1} = \\frac{z+1}{2}$."
    ],
    "correctAnswer": 1,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q39",
    "type": "fill",
    "question": "Một hộp chứa 11 quả cầu gồm 5 quả cầu màu xanh và 6 quả cầu màu đỏ. Chọn ngẫu nhiên đồng thời 2 quả cầu từ hộp đó. Xác suất để 2 quả cầu chọn ra khác màu bằng",
    "correctAnswer": "6/11",
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q40",
    "type": "mcq",
    "question": "Cho hình hộp $ABCD.A'B'C'D'$ có $\\overrightarrow{AB}=\\vec{a}, \\overrightarrow{AC}=\\vec{b}, \\overrightarrow{AA'}=\\vec{c}$. Gọi I là trung điểm $B'C'$, K là giao điểm $A'I, B'D'$. Hãy biểu diễn vecto $\\overrightarrow{AI}$ theo các vecto $\\vec{a}, \\vec{b}, \\vec{c}$?",
    "options": [
      "$\\overrightarrow{AI} = \\frac{1}{2}\\vec{a} + \\frac{1}{2}\\vec{b} + \\vec{c}$",
      "$\\overrightarrow{AI} = -\\frac{1}{2}\\vec{a} + \\frac{3}{2}\\vec{b} + \\vec{c}$",
      "$\\overrightarrow{AI} = \\frac{3}{2}\\vec{a} + \\frac{1}{2}\\vec{b} - \\vec{c}$",
      "$\\overrightarrow{AI} = \\frac{1}{2}\\vec{a} - \\frac{1}{2}\\vec{b} - \\vec{c}$"
    ],
    "correctAnswer": 0,
    "explanation": "Chi tiết giải...",
    "image": null
  },
  {
    "id": "q41",
    "type": "mcq",
    "question": "Cho tứ diện $ABCD$. Gọi $M$, $N$, $P$, $Q$ là các điểm thỏa mãn: $\\overrightarrow{MA} = -2\\overrightarrow{MB}$, $\\overrightarrow{NB} = -2\\overrightarrow{NC}$, $\\overrightarrow{PC} = -2\\overrightarrow{PD}$, $\\overrightarrow{QD} = -2\\overrightarrow{QA}$. Hãy phân tích vecto $\\overrightarrow{MP}$ theo ba vecto $\\overrightarrow{AB}, \\overrightarrow{AC}, \\overrightarrow{AD}$?",
    "options": [
      "$\\overrightarrow{MP} = \\frac{1}{3}\\overrightarrow{AB} + \\frac{1}{3}\\overrightarrow{AC} + \\frac{1}{3}\\overrightarrow{AD}$",
      "$\\overrightarrow{MP} = \\frac{2}{3}\\overrightarrow{AB} + \\frac{1}{3}\\overrightarrow{AC} - \\frac{2}{3}\\overrightarrow{AD}$",
      "$\\overrightarrow{MP} = \\frac{2}{3}\\overrightarrow{AB} - \\frac{1}{3}\\overrightarrow{AC} + \\frac{2}{3}\\overrightarrow{AD}$",
      "$\\overrightarrow{MP} = \\frac{-2}{3}\\overrightarrow{AB} + \\frac{1}{3}\\overrightarrow{AC} + \\frac{2}{3}\\overrightarrow{AD}$"
    ],
    "correctAnswer": 3,
    "explanation": "Chi tiết giải sẽ được cập nhật sau.",
    "image": null
  },
  {
    "id": "q42",
    "type": "mcq",
    "question": "Có 50 phiếu thi Toán 12, mỗi phiếu chỉ có 1 câu hỏi, trong đó có 15 câu lý thuyết gồm 8 câu khó, 7 câu dễ và 35 câu hỏi bài tập gồm 20 câu dễ và 15 câu khó. Lấy ngẫu nhiên 1 phiếu. Tìm xác suất rút được câu lý thuyết khó",
    "options": [
      "$P = \\frac{4}{25}$",
      "$P = \\frac{8}{15}$",
      "$P = \\frac{8}{25}$",
      "$P = \\frac{3}{25}$"
    ],
    "correctAnswer": 1,
    "explanation": "Chi tiết giải sẽ được cập nhật sau.",
    "image": null
  },
  {
    "id": "q43",
    "type": "mcq",
    "question": "Cối xay gió Đôn Kihote (từ tác phẩm của nhà văn Cervantes) có phần trên là cối xay gió có dạng hình nón, chiều cao của hình nón là $40\\text{ cm}$ và thể tích của nó là $18000\\text{cm}^3$. Tính bán kính của đáy hình tròn. Làm tròn đến kết quả chữ số thập phân thứ hai. Biết rằng công thức tính thể tích hình nón là $V = \\frac{1}{3}\\pi R^2h$, trong đó $R$ là bán kính đường tròn đáy, $h$ là đường nối từ đỉnh nón đến tâm đường tròn đáy.",
    "options": [
      "$R = 22,32\\text{cm}$",
      "$R = 19,72\\text{cm}$",
      "$R = 20,72\\text{cm}$",
      "$R = 18,75\\text{cm}$"
    ],
    "correctAnswer": 2,
    "explanation": "Chi tiết giải sẽ được cập nhật sau.",
    "image": null
  },
  {
    "id": "q44",
    "type": "mcq",
    "question": "Cho hàm số $y = f(x)$ xác định và liên tục trên $\\mathbb{R}$ và có bảng biến thiên như hình vẽ:\n\nHàm số $y = f(2x + 1)$ đồng biến trên khoảng nào dưới đây?",
    "options": [
      "$(-1; 1)$",
      "$(-2; 0)$",
      "$(-3; -2)$",
      "$\\left( \\frac{1}{2}; 4 \\right)$"
    ],
    "correctAnswer": 2,
    "explanation": "Chi tiết giải sẽ được cập nhật sau.",
    "image": "cau_44.png"
  },
  {
    "id": "q45",
    "type": "mcq",
    "question": "Số đường tiệm cận của đồ thị hàm số $y = \\frac{1 + \\sqrt{x + 4}}{x^2 + 5x}$ là:",
    "options": [
      "$1$",
      "$2$",
      "$4$",
      "$3$"
    ],
    "correctAnswer": 1,
    "explanation": "Chi tiết giải sẽ được cập nhật sau.",
    "image": null
  },
  {
    "id": "q46",
    "type": "mcq",
    "question": "Trong không gian với hệ tọa độ $Oxyz$, gọi $(S)$ là mặt cầu đi qua hai điểm $A(-1; -2; 4)$, $B(2; 1; 2)$ và có tâm thuộc trục $Oz$. Bán kính của mặt cầu $(S)$ là?",
    "options": [
      "$\\sqrt{6}$",
      "$\\sqrt{5}$",
      "$6$",
      "$5$"
    ],
    "correctAnswer": 0,
    "explanation": "Chi tiết giải sẽ được cập nhật sau.",
    "image": null
  },
  {
    "id": "q47",
    "type": "mcq",
    "question": "Cho hàm số $y = f(x)$ có bảng biến thiên như hình vẽ bên dưới.\n\nSố nghiệm thực phân biệt của phương trình $f[f(x) + 1] + 2 = 0$ là:",
    "options": [
      "$5$",
      "$4$",
      "$3$",
      "$7$"
    ],
    "correctAnswer": 1,
    "explanation": "Chi tiết giải sẽ được cập nhật sau.",
    "image": "cau_47.png"
  },
  {
    "id": "q48",
    "type": "fill",
    "question": "Cho hàm số $y = x^3 - 3x$ có đồ thị $(C)$. Gọi $S$ là tập hợp tất cả các giá trị thực của $k$ để đường thẳng $d: y = k(x + 1) + 2$ cắt đồ thị hàm số $(C)$ tại ba điểm phân biệt $M$, $N$, $P$ sao cho các tiếp tuyến của $(C)$ tại $N$ và $P$ vuông góc với nhau. Biết điểm $M(-1; 2)$, tính tích tất cả các phần tử của tập $S$?",
    "correctAnswer": "1/9",
    "explanation": "Chi tiết giải sẽ được cập nhật sau.",
    "image": null
  },
  {
    "id": "q49",
    "type": "fill",
    "question": "Có tất cả bao nhiêu giá trị nguyên của $m$ để hàm số $y = x^8 + (m - 2)x^5 - (m^2 - 4)x^4 + 1$ đạt cực tiểu tại $x = 0$.",
    "correctAnswer": "4",
    "explanation": "Chi tiết giải sẽ được cập nhật sau.",
    "image": null
  },
  {
    "id": "q50",
    "type": "fill",
    "question": "Một con châu chấu nhảy từ gốc tọa độ $O(0; 0)$ đến điểm $A(9; 0)$ dọc theo trục $Ox$ của hệ trục tọa độ $Oxy$. Con châu chấu có bao nhiêu cách nhảy để đến điểm $A$ biết mỗi lần nó có thể nhảy 1 bước hoặc 2 bước (1 bước có độ dài 1 đơn vị).",
    "correctAnswer": "55",
    "explanation": "Chi tiết giải sẽ được cập nhật sau.",
    "image": null
  }
];

`

### firebase-config.js

`javascript
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.1/firebase-app.js";
import {
  getDatabase, ref, push, set, update, serverTimestamp,
} from "https://www.gstatic.com/firebasejs/10.8.1/firebase-database.js";

const firebaseConfig = {
  apiKey: "AIzaSyC8AT2g3vS54-Qco3uU36xYsXN04trj0Yw",
  authDomain: "mtsedu-85ea3.firebaseapp.com",
  databaseURL: "https://mtsedu-85ea3-default-rtdb.asia-southeast1.firebasedatabase.app",
  projectId: "mtsedu-85ea3",
  storageBucket: "mtsedu-85ea3.firebasestorage.app",
  messagingSenderId: "73617729802",
  appId: "1:73617729802:web:e7fa3c3c3b9ded7522f2f3",
  measurementId: "G-JHQC9DSKY5"
};

const app = initializeApp(firebaseConfig);
const db = getDatabase(app);
export { db, ref, push, set, update, serverTimestamp };



`

### mtsedu-auth.js

`javascript
const SESSION_KEY = 'mtsedu_session';

export function getMTSeduSession() {
  const params = new URLSearchParams(window.location.search);
  const urlUsername = params.get('mtsedu_user');
  const urlName = params.get('mtsedu_name');
  const urlId = params.get('mtsedu_id');
  const returnUrl = params.get('mtsedu_return');

  if (urlUsername) {
    const session = {
      username: urlUsername,
      displayName: urlName || urlUsername,
      id: urlId || ('user_' + urlUsername),
      returnUrl: returnUrl || 'https://mtsedu.vercel.app'
    };
    try { localStorage.setItem(SESSION_KEY, JSON.stringify(session)); } catch {}
    return session;
  }

  try {
    const raw = localStorage.getItem(SESSION_KEY);
    if (!raw) return null;
    const user = JSON.parse(raw);
    return (user && user.username) ? user : null;
  } catch { return null; }
}

export function getReturnUrl() {
  const session = getMTSeduSession();
  return (session && session.returnUrl) ? session.returnUrl : 'https://mtsedu.vercel.app';
}

export function isLoggedIn() { return getMTSeduSession() !== null; }

export function getStudentName() {
  const s = getMTSeduSession();
  return s ? (s.displayName || s.username) : '';
}

export function clearSession() {
  try { localStorage.removeItem(SESSION_KEY); } catch {}
}

export function showLoginRequired(container, returnHash = '') {
  const mtseduUrl = 'https://mtsedu.vercel.app/' + returnHash;
  container.innerHTML = `
    <div style="max-width:480px;margin:0 auto;padding:36px;background:white;border-radius:16px;
      box-shadow:0 4px 24px rgba(0,0,0,0.08);text-align:center;
      font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;">
      <div style="font-size:48px;margin-bottom:16px;">🔒</div>
      <h2 style="font-size:22px;font-weight:700;margin:0 0 8px;color:#111;">Vui lòng đăng nhập</h2>
      <p style="color:#666;font-size:15px;margin:0 0 28px;line-height:1.6;">
        Bạn cần đăng nhập vào hệ thống <strong>MTS Education</strong> để làm bài thi này.
      </p>
      <a href="${mtseduUrl}" style="display:inline-block;background:#000;color:#fff;
        text-decoration:none;padding:14px 32px;border-radius:10px;font-size:15px;font-weight:600;">
        Đăng nhập tại MTS Education →
      </a>
      <p style="margin-top:20px;font-size:13px;color:#999;">Tài khoản được cung cấp bởi giáo viên</p>
    </div>
  `;
}

export function insertBackButton() {
  const session = getMTSeduSession();
  const returnUrl = (session && session.returnUrl) ? session.returnUrl : 'https://mtsedu.vercel.app';
  const btn = document.createElement('div');
  btn.id = 'mtsedu-back-btn';
  btn.innerHTML = `
    <a href="${returnUrl}" style="display:inline-flex;align-items:center;gap:8px;
      position:fixed;top:14px;left:14px;z-index:9999;background:rgba(0,0,0,0.85);
      color:white;text-decoration:none;padding:9px 18px;border-radius:50px;
      font-size:14px;font-weight:600;font-family:-apple-system,sans-serif;
      backdrop-filter:blur(8px);box-shadow:0 2px 12px rgba(0,0,0,0.3);"
      onmouseover="this.style.background='rgba(0,0,0,1)'"
      onmouseout="this.style.background='rgba(0,0,0,0.85)'">
      ← Trang chủ
    </a>
  `;
  document.body.appendChild(btn);
}



`

