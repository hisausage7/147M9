<吃飽太閒做的網站，能幫到你我覺得很開心>
<html lang="zh-Hant">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>147測驗｜單一檔案版</title>

    <!-- 預先套用主題避免閃爍 -->
    <script>
      (function () {
        try {
          var saved = localStorage.getItem('theme');
          if (saved === 'dark' || (!saved && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
            document.documentElement.classList.add('preload-dark');
            document.documentElement.setAttribute('data-theme','dark');
          }
        } catch(e){}
      })();
    </script>

    <style>
      :root{
        --bg:#f0f4f8; --txt:#000; --card:#fff; --rule:#e9ecef; --muted:#666;
        --primary:#007bff; --primary-800:#0056b3; --danger:#dc3545;
        --green:#28a745; --green-800:#218838; --teal:#17a2b8; --teal-800:#138496;
        --table-bd:#ccc;

        /* 正解強調（淺色） */
        --ans-chip-bg:#e7f6ec; --ans-chip-fg:#136d3a;
        --ans-row-bg:#f5fbf7; --ans-row-bd:#cce8d5;
      }
      body.dark {
        --bg:#121212; --txt:#fff; --card:#1e1e1e; --rule:#333; --table-bd:#444; --muted:#aaa;

        /* 正解強調（深色） */
        --ans-chip-bg:#1f3a29; --ans-chip-fg:#b9f6ca;
        --ans-row-bg:#12301f; --ans-row-bd:#2c5a3f;
      }

      html, body { height: 100%; }
      body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 40px;
        /* 基礎自適應字級（桌機普遍上限 24px） */
        font-size: clamp(16px, 1.1vw + 12px, 24px);
        background: var(--bg);
        color: var(--txt);
        transition: background-color .4s, color .4s;
      }

      #container {
        max-width: 1320px; margin: auto; background: var(--card); padding: 40px;
        border-radius: 20px; box-shadow: 0 0 10px rgba(0,0,0,.1);
        transition: background-color .4s, color .4s;
      }

      .hidden { display: none; }
      h1, h2 { text-align: center; font-size: 1.6em; margin: .2em 0 .6em; }
      #rules { background: var(--rule); padding: 16px; margin-bottom: 28px; border-radius: 10px; font-size: .95em; }

      .btn {
        background: var(--primary); color: #fff; border: none; padding: 14px 24px;
        margin: 8px; border-radius: 10px; cursor: pointer; font-size: .95em;
        transition: background-color .2s, transform .1s;
        white-space: nowrap;
      }
      .btn:hover { background: var(--primary-800); }
      #leaveBtn { background: var(--danger); }
      #openBankBtn { background: var(--teal); }
      #openBankBtn:hover { background: var(--teal-800); }

      /* 進度條 */
      #progress, #timer { font-weight: bold; font-size: 1em; }
      .progress-container { background: #ddd; height: 10px; border-radius: 5px; margin-top: 14px; overflow: hidden; }
      body.dark .progress-container { background: #555; }
      .progress-bar { height: 100%; width: 0; background: var(--primary); transition: width .6s ease; }

      .question { margin: 24px 0 12px; font-size: 1.2em; }
      .options label { display: block; margin-bottom: 12px; font-size: 1em; }

      /* 表格與響應式容器 */
      .table-responsive { width: 100%; overflow-x: auto; -webkit-overflow-scrolling: touch; }
      table { width: 100%; border-collapse: collapse; margin-top: 16px; font-size: 1em; min-width: 460px; }
      th, td {
        border: 1px solid var(--table-bd); padding: 12px 14px; text-align: left; vertical-align: top;
        color: var(--txt); word-break: break-word;
      }

      /* 錯題列色（深色模式改亮字） */
      tr.wrong { background-color: #ffe6e6; }
      body.dark tr.wrong { background-color: #5a1a1a; }
      body.dark tr.wrong td { color: #fff; }

      /* 正解強調（提高優先度，避免被錯題底色吃掉） */
      .ans-chip { display:inline-block; padding:2px 8px; border-radius:999px; background: var(--ans-chip-bg); color: var(--ans-chip-fg); font-size:.9em; margin-right:6px; }
      .ans-cell  { background: var(--ans-row-bg) !important; border-left: 3px solid var(--ans-row-bd) !important; color: var(--txt) !important; }
      .opt-row   { display:block; padding:4px 6px; margin:2px 0; border-radius:6px; }
      .opt-row.is-correct { background: var(--ans-row-bg) !important; border-left: 3px solid var(--ans-row-bd) !important; color: var(--txt) !important; }
      tr.wrong td.ans-cell { background: var(--ans-row-bg) !important; color: var(--txt) !important; }

      /* 右上角按鈕固定 */
      #darkModeToggle, #homeBtn {
        position: fixed; right: 20px; padding: 10px 16px; border: none; border-radius: 8px;
        cursor: pointer; font-size: .95em; z-index: 2000; box-shadow: 0 4px 12px rgba(0,0,0,.15);
      }
      #darkModeToggle { top: 20px; background: #333; color: #fff; }
      #darkModeToggle:hover { background: #555; }
      #homeBtn { top: 68px; background: var(--green); color: #fff; text-decoration: none; }
      #homeBtn:hover { background: var(--green-800); }

      .mono { font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Courier New", monospace; }
      .muted { opacity: .8; color: var(--muted); }

      /* 小尺寸優化 */
      @media (max-width: 768px) {
        body { padding: 20px; font-size: clamp(14px, 2.2vw + 8px, 17px); }
        #container { padding: 20px; border-radius: 16px; }
        .btn { padding: 12px 16px; margin: 6px; font-size: .95em; }
        #darkModeToggle, #homeBtn { right: 12px; }
        #darkModeToggle { top: 12px; }
        #homeBtn { top: 56px; }
      }
      @media (max-width: 540px) {
        /* 手機上把「您的答案」隱藏，保留題目/正解/OX */
        #results table th:nth-child(2), #results table td:nth-child(2) { display:none; }
      }
      @media (max-width: 420px) {
        #bank .controls { display: grid; grid-template-columns: 1fr; gap: 8px; }
      }

      /* —— 大螢幕加碼放大（到 4K 前） —— */
      @media (min-width: 1200px) {
        body       { font-size: clamp(18px, 0.9vw + 12px, 26px); }
        #container { max-width: 1440px; }
        h1, h2     { font-size: 2rem; }
      }
      @media (min-width: 1800px) {
        body       { font-size: clamp(20px, 0.7vw + 12px, 28px); }
        #container { max-width: 1680px; }
        h1, h2     { font-size: 2.2rem; }
      }
      @media (min-width: 2400px) {
        body       { font-size: clamp(22px, 0.6vw + 14px, 32px); }
        #container { max-width: 1920px; }
        h1, h2     { font-size: 2.4rem; }
      }

      /* —— 2560×1440（含以上）專用上限 —— */
      @media (min-width: 2560px) and (min-height: 1400px) {
        body       { font-size: clamp(22px, 0.55vw + 16px, 34px); } /* 上限 34px */
        #container { max-width: 2000px; }
        h1, h2     { font-size: 2.6rem; }
      }

      /* 預載深色（head 腳本使用），load 後會移除 */
      .preload-dark body, .preload-dark { background:#121212; color:#fff; }
    </style>
  </head>
  <body>
    <button id="darkModeToggle" aria-pressed="false">深色模式 / Dark Mode</button>
    <a id="homeBtn" href="https://hisausage7.github.io/147test/" title="回首頁">🏠 回首頁</a>

    <div id="container">
      <!-- 歡迎頁 -->
      <div id="welcome">
        <h1>147測驗M9-校內考</h1>
        <div id="rules">
          <p><strong>考試注意事項 / Exam Rules:</strong></p>
          <p>1. 請輸入姓名後才能開始作答。 / You must enter your name to start the quiz.</p>
          <p>2. 考試限時80分鐘，自動倒數。 / The quiz is timed for 80 minutes, countdown starts immediately.</p>
          <p>3. 作答途中可隨時點擊「離開考試」提前結束。 / You can click "Leave Quiz" anytime to finish early.</p>
          <p>4. 完成後會自動顯示所有答題結果與成績。 / Results and scores will be displayed after completion.</p>
          <p>5. 答對題目顯示O，答錯題目顯示X。 / Correct answers will show O, incorrect answers will show X.</p>
          <p>6. 測驗過程為亂序出題。 / The test process was chaotic and disordered in setting questions.</p>
          <p>!版權及源代碼所有-航機系008沈崑宸!</p>
          <p>!僅作為自我測驗使用!</p>
        </div>
        <input type="text" id="nameInput" placeholder="輸入姓名 / Enter your name"
               style="width:100%;padding:8px;margin-bottom:10px;font-size:1em;" />
        <input type="number" id="questionLimit" placeholder="輸入題數,至多102題 / Enter number of questions"
               style="width:100%;padding:8px;margin-bottom:10px;font-size:1em;" />
        <div style="text-align:center; display:flex; flex-wrap:wrap; justify-content:center;">
          <button id="startBtn" class="btn">開始測驗 / Start Quiz</button>
          <button id="openBankBtn" class="btn">題庫瀏覽 / Browse Bank</button>
        </div>
      </div>

      <!-- 測驗頁 -->
      <div id="quiz" class="hidden">
        <div style="display:flex; align-items:center; gap:8px;">
          <span id="welcomeName"></span>
          <span id="timer" style="margin-left:auto">80:00</span>
        </div>
        <div class="mono" id="progress">題數: <span id="current">0</span> / <span id="total">0</span></div>
        <div class="progress-container"><div id="progressBar" class="progress-bar"></div></div>
        <div class="question" id="questionText"></div>
        <div class="options" id="options"></div>
        <div style="display:flex;gap:10px;flex-wrap:wrap">
          <button id="prevBtn" class="btn" style="background:#6c757d">上一題 / Previous</button>
          <button id="leaveBtn" class="btn">離開考試 / Leave Quiz</button>
        </div>
      </div>

      <!-- 結果頁 -->
      <div id="results" class="hidden">
        <h2>測驗結果 / Results</h2>
        <div style="display:flex; flex-wrap:wrap; justify-content:center;">
          <button id="retryBtn" class="btn">重新開始 / Retry</button>
          <button id="showWrongBtn" class="btn" style="background:#ffc107">只看錯題 / Wrong Only</button>
          <button id="showAllBtn" class="btn">看全部結果 / Show All</button>
          <button id="toBankFromResults" class="btn" style="background:#17a2b8">題庫瀏覽 / Browse Bank</button>
        </div>
        <div class="table-responsive">
          <table>
            <thead>
              <tr><th>題目</th><th>您的答案</th><th>正確答案</th><th>結果</th></tr>
            </thead>
            <tbody id="resultsBody"></tbody>
          </table>
        </div>
        <div id="scoreSummary" style="text-align:center;margin-top:12px;font-size:1em"></div>
      </div>

      <!-- 題庫瀏覽頁 -->
      <div id="bank" class="hidden">
        <h2>題庫瀏覽 / Question Bank</h2>
        <div class="controls">
          <input id="bankSearch" type="text" placeholder="關鍵字搜尋（會搜尋題目與選項）" />
          <label>每頁顯示
            <select id="perPage">
              <option value="5">5</option>
              <option value="10" selected>10</option>
              <option value="20">20</option>
              <option value="50">50</option>
              <option value="all">全部</option>
            </select>
            題
          </label>
          <button id="backToWelcome" class="btn" style="padding:12px 18px">返回首頁 / Home</button>
        </div>
        <div class="table-responsive">
          <table>
            <thead>
              <tr>
                <th style="width:70px">#</th>
                <th>題目</th>
                <th style="width:34%">選項</th>
                <th style="width:160px">正確答案</th>
              </tr>
            </thead>
            <tbody id="bankBody"></tbody>
          </table>
        </div>
        <div class="pagination" style="display:flex;justify-content:center;align-items:center;gap:10px;margin-top:10px;">
          <button id="prevPage" class="btn" style="padding:10px 16px">上一頁</button>
          <span id="pageInfo" class="mono"></span>
          <button id="nextPage" class="btn" style="padding:10px 16px">下一頁</button>
        </div>
        <div style="text-align:center;margin-top:8px">
          <small class="muted">提示：可用右上角「深色模式」切換外觀；搜尋支援中英文與數字。</small>
        </div>
      </div>
    </div>

    <script>
      document.addEventListener("DOMContentLoaded", function () {
        const questions = [
          { question: "The area in the brain that processes information from the eyes is known as the visual:",
            options: ["A. centre", "B. nerve", "C. cortex"], answer: "C" },
          { question: "Long sighted people have an eyeball that is:",
            options: ["A. shorter than normal","B. longer than normal","C. oval"], answer: "A" },
          { question: "Peripheral vision occurs through the action of the:",
            options: ["A. cones","B. rods","C. cornea"], answer: "B" },
          { question: "When the intensity of light increases, the pupil of the eye will:",
            options: ["A. grow smaller","B. grow larger","C. not be affected"], answer: "A" },
          { question: "The region of the retina that produces the highest visual acuity is the:",
            options: ["A. periphery","B. fovea","C. choroid"], answer: "B" },
          { question: "When damage occurs to the eardrum or the ossicles, the type of deafness that may occur is known as:",
            options: ["A. presbycusis","B. noise induced hearing loss","C. conductive deafness"], answer: "C" },
          { question: "The otoliths in the inner ear detect:",
            options: ["A. angular movement","B. linear acceleration","C. high tone sound"], answer: "B" },
          { question: "The second action level that requires the use of warning signs occurs at:",
            options: ["A. 90db","B. 85db","C. 140db"], answer: "A" },
          { question: "The Time Weighted Average Sound Level (TWA) above which permanent deafness can occur is:",
            options: ["A. 80db","B. 90db","C. 150db"], answer: "B" },
          { question: "Balance is maintained by the action of the:",
            options: ["A. ossicles and the cochlea","B. tympanic and basilar membranes","C. otoliths and the semi-circular canals"], answer: "C" },
          { question: "Motor Programmes are stored in the:",
            options: ["A. long-term memory as behavioural sub-routines","B. short-term memory as reflex actions","C. sensory stores as automatic actions"], answer: "A" },
          { question: "The capacity of the short-term memory may be increased by:",
            options: ["A. rehearsing information","B. breaking information into 'chunks'","C. transferring information into long-term memory"], answer: "B" },
          { question: "The maximum number of unrelated items of information that can be stored in the working memory at any one time is normally limited to between:",
            options: ["A. 4 and 5","B. 5 and 9","C. 9 and 11"], answer: "B" },
          { question: "Information can be held in the working memory for:",
            options: ["A. 5 to 10 minutes","B. 1 to 2 seconds","C. 10 to 20 seconds"], answer: "C" },
          { question: "Amnesia tends to affect the:",
            options: ["A. episodic memory","B. echoic memory","C. semantic memory"], answer: "A" },
          { question: "Overhearing your name mentioned whilst engaged in a separate conversation is known as:",
            options: ["A. focused attention","B. divided attention","C. cocktail party effect"], answer: "C" },
          { question: "The most accurate and enduring part of the long-term memory is the:",
            options: ["A. semantic memory","B. episodic memory","C. iconic memory"], answer: "A" },
          { question: "We need an attention gaining mechanism because the:",
            options: ["A. episodic memory is unreliable","B. capacity of the sensory stores is limited","C. capacity of the working memory store is limited"], answer: "C" },
          { question: "Claustrophobia is associated with:",
            options: ["A. confined spaces","B. heights","C. body measurements"], answer: "A" },
          { question: "The distance that a person with normal hearing should be able to hear an average conversational voice in a quiet room is:",
            options: ["A. three metres or nine feet","B. two metres or six feet","C. four metres or twelve feet"], answer: "B" },
          { question: "The term 'risky shift' is:",
            options: ["A. the early morning shift","B. a shift that has experienced disrupted sleep patterns","C. the tendency of a group to make a more risky decision than an individual"], answer: "C" },
          { question: "The behaviour of an individual working as an aircraft engineer is ideally:",
            options: ["A. goal and person directed","B. goal directed only","C. person directed only"], answer: "A" },
          { question: "When a democratic leader has to reach a non-urgent decision he/she would:",
            options: ["A. make the decision and then tell the group","B. invite suggestions from the group and then make the decision","C. leave the group to make the decision"], answer: "B" },
          { question: "Personality is:",
            options: ["A. resistant to change","B. easily modified by experience","C. easily changed by discipline"], answer: "A" },
          { question: "A person is more likely to comply with a decision made by someone with:",
            options: ["A. more experience","B. higher status","C. a stronger personality"], answer: "B" },
          { question: "A decision made by a group, compared to that made by an individual tends to be:",
            options: ["A. worse and over-cautious","B. better but less extreme","C. better but more extreme"], answer: "C" },
          { question: "If you are a good leader you will ideally make people:",
            options: ["A. do what they do not want to do","B. want to do what you want them to do","C. want to do what they want to do"], answer: "B" },
          { question: "When an individual feels driven to conform to colleague's views it is normally as result of:",
            options: ["A. groupthink","B. group culture","C. peer pressure"], answer: "C" },
          { question: "Diffusion of responsibility occurs when:",
            options: ["A. each team member assumes someone else is going to do the work","B. there is no appointed leader","C. two groups are engaged on one task"], answer: "A" },
          { question: "The desire of a group to reach collective agreement at the expense of rational decision making is called:",
            options: ["A. The Hawthorne Effect","B. Groupthink","C. Peer pressure"], answer: "B" },
          { question: "An individual who relies on his/her lack of effort going unnoticed within the collective effort of a group is engaging in:",
            options: ["A. peer pressure","B. group polarisation","C. social loafing"], answer: "C" },
          { question: "A manager who permits staff to make their own decisions within prescribed limits is exercising:",
            options: ["A. permissive leadership","B. democratic leadership","C. autocratic leadership"], answer: "A" },
          { question: "In the hierarchy of human needs the initial needs are:",
            options: ["A. self-esteem","B. physical","C. social"], answer: "B" },
          { question: "When a certifying engineer signs a Certificate of Release to Service for work done by non-certifying staff, the responsibility for the actual work done:",
            options: ["A. remains with those who carried it out","B. passes to the supervisor of the work","C. passes to the person making the certifying signature"], answer: "C" },
          { question: "The correct sequence for managing a task is:",
            options: ["A. organise, motivate, plan and control","B. plan, organise, motivate and control","C. plan, control, organise and motivate"], answer: "B" },
          { question: "The culture of an organisation is the:",
            options: ["A. way they do things","B. type of work they do","C. management structure"], answer: "A" },
          { question: "Group polarisation results in:",
            options: ["A. more extreme decisions","B. less extreme decisions","C. no decisions"], answer: "A" },
          { question: "An organisation acquires a safety culture when:",
            options: ["A. it is introduced as company policy","B. it develops amongst the staff","C. it is included in the Mission Statement"], answer: "B" },
          { question: "Motivation is:",
            options: ["A. making an individual to do something","B. how quickly an individual does something","C. the individual's will to do something"], answer: "C" },
          { question: "Circadian rhythms have a time cycle of approximately:",
            options: ["A. 7 days","B. 23 hours","C. 25 hours"], answer: "C" },
          { question: "The cycle of REM sleep occurs every:",
            options: ["A. 60 minutes","B. 90 minutes","C. 30 minutes"], answer: "B" },
          { question: "A person is classified as being obese if their body mass index is over:",
            options: ["A. 30","B. 25","C. 20"], answer: "A" },
          { question: "When a person is short of oxygen and compensates by increasing their rate and depth of breathing, the process is called:",
            options: ["A. anoxia","B. hypoxia","C. hyperventilation"], answer: "C" },
          { question: "When taking a new prescribed medication for the first time you should:",
            options: ["A. give it a 24 hour trial before reporting for duty","B. not report for duty until you have completed the course","C. carry on as normal"], answer: "A" },
          { question: "One unit of alcohol is roughly equivalent to",
            options: ["A. half a pint of beer or a 125ml glass of wine or a single measure of spirit",
                     "B. one pint of beer or 250ml glass of wine or a double measure of spirit",
                     "C. one pint of beer or a half standard glass of wine or spirit"], answer: "A" },
          { question: "The effect of 'Jet Lag' is more pronounced when you fly:",
            options: ["A. South to North","B. East to West","C. West to East"], answer: "C" },
          { question: "Oxygen is used in the human body to:",
            options: ["A. cleanse the blood of impurities","B. oxidise food and produce energy","C. produce carbon dioxide to regulate breathing"], answer: "B" },
          { question: "The minimum recommended amount of exercise a person should engage in to reduce the risk of heart disease is:",
            options: ["A. three twenty minute sessions a week that double the heart rate",
                      "B. one thirty minute session a day at double the heart rate",
                      "C. ten miles walking a week at triple the heart rate"], answer: "A" },
          { question: "A person who drinks alcohol to alleviate the symptoms of stress is engaging in:",
            options: ["A. coping strategy","B. defence strategy","C. diversion strategy"], answer: "B" },
          { question: "REM sleep is used to:",
            options: ["A. restore body tissue","B. raise body temperature","C. strengthen and organise the memory"], answer: "C" },
          { question: "In the normal Circadian rhythm, the period of lowest performance occurs around:",
            options: ["A. 5am","B. 3pm","C. midnight"], answer: "A" },
          { question: "The recommended cycle for a rolling shift pattern would be:",
            options: ["A. night shift to late shift to early shift",
                      "B. early shift to late shift to night shift",
                      "C. late shift to early shift to night shift"], answer: "B" },
          { question: "In the sleep credit system one hour of good quality sleep is worth:",
            options: ["A. one hour of activity","B. four hours of activity","C. two hours of activity"], answer: "C" },
          { question: "The majority of stage 2 to 4 sleep occurs:",
            options: ["A. in the later part of the sleep period",
                      "B. in the early part of the sleep period",
                      "C. throughout the sleep period"], answer: "B" },
          { question: "If a person is awakened halfway through the sleep period they will be deprived mainly of:",
            options: ["A. REM and stage 2 sleep","B. non-REM sleep","C. stage 2 to 4 and non-REM sleep"], answer: "A" },
          { question: "Oxygen is passed into the bloodstream in the:",
            options: ["A. trachea in the throat","B. aorta in the heart","C. alveoli in the lungs"], answer: "C" },
          { question: "Good stress management involves:",
            options: ["A. developing a defence strategy","B. identifying the stressor and coping","C. avoiding stress"], answer: "B" },
          { question: "The use of 'pep' pills by an aircraft engineer when working is:",
            options: ["A. recommended during night shifts to reduce risk of error",
                      "B. permitted only when prescribed by a doctor",
                      "C. not permitted"], answer: "C" },
          { question: "After a long night shift, the recommended meal would be:",
            options: ["A. high in proteins","B. low in carbohydrates","C. high in carbohydrates"], answer: "C" },
          { question: "An excessive noise level would increase a person's performance:",
            options: ["A. during high arousal periods","B. during low arousal periods","C. never"], answer: "C" },
          { question: "A general guide to assist in judging when ear defenders are required when working in a hangar environment is when:",
            options: ["A. you are not able to hear clearly a conversational voice at 6 feet or 2m",
                      "B. the noise level causes temporary deafness",
                      "C. when you cannot hear clearly a shouted voice at 6 feet or 2m"], answer: "A" },
          { question: "White finger syndrome is:",
            options: ["A. a disorder of the finger caused by continuous use of vibratory tools",
                      "B. an accumulation of white blood cells in the fingers",
                      "C. an allergic reaction to the pigments in white paint"], answer: "A" },
          { question: "The high frequency ultra-sounds that are emitted by jet engines are:",
            options: ["A. not injurious to the hearing","B. always injurious to the hearing","C. only injurious if they are heard"], answer: "B" },
          { question: "COSHH assessment defines the hazards, limits and protection requirements for:",
            options: ["A. the general use of substances found in the work place",
                      "B. local exhaust ventilation systems",
                      "C. the use of a hazardous substance in a work process in a given work location"], answer: "C" },
          { question: "Poor lighting conditions will:",
            options: ["A. not affect colour vision but will reduce the ability to detect fine detail",
                      "B. affect colour vision and the ability to detect fine detail",
                      "C. affect colour vision but will not affect the ability to detect fine detail"], answer: "B" },
          { question: "Hypothermia is a condition that is associated with:",
            options: ["A. low body temperature","B. high body temperature","C. heat stroke"], answer: "A" },
          { question: "The low frequency range of vibration that is most injurious to the hands is:",
            options: ["A. 20 Hz to 20 kHz","B. 50 Hz to 150 Hz","C. 0.5 kHz to 150 kHz"], answer: "B" },
          { question: "The components of a working environment are:",
            options: ["A. the physical environment, the social environment and the tasks",
                      "B. noise, illumination, fumes and vibration",
                      "C. the hangar and office accommodation"], answer: "A" },
          { question: "If the working environment on line maintenance reaches an unacceptable level:",
            options: ["A. more time should be allotted to tasks",
                      "B. more personnel should be assigned to tasks",
                      "C. work should be suspended until satisfactory conditions are re-established"], answer: "C" },
          { question: "If an engineer suspects the presence of fumes in the work area, he/she should:",
            options: ["A. don a suitable respirator before continuing with work",
                      "B. warn colleagues and the supervisor and evacuate the area",
                      "C. not use equipment that could create sparks"], answer: "B" },
          { question: "When someone is working in an enclosed space they:",
            options: ["A. should comply with the maintenance manual",
                      "B. should be instructed on the possible hazards",
                      "C. require extra supervision and communication"], answer: "C" },
          { question: "The major risk encountered when carrying out repetitive work is that personnel can become:",
            options: ["A. complacent","B. too specialised","C. bored"], answer: "A" },
          { question: "Ergonomics is a study of:",
            options: ["A. the musculoskeletal system",
                      "B. people in relation to their working environment",
                      "C. timescales in relation to work processes"], answer: "B" },
          { question: "Visual inspection of a structure should be ideally carried out:",
            options: ["A. in one uninterrupted period to avoid breaking concentration",
                      "B. in reduced lighting to avoid straining the eyes",
                      "C. in short discrete periods with frequent breaks"], answer: "C" },
          { question: "Errors made during visual inspection are likely to be due to:",
            options: ["A. vision being the least sensitive stimuli","B. lack of concentration","C. eyestrain"], answer: "B" },
          { question: "The best visual scan pattern is to:",
            options: ["A. make random eye movements","B. keep the head still when moving the eyes","C. make frequent eye movements"], answer: "C" },
          { question: "A complex system in terms of one person's conception of it is said to be:",
            options: ["A. opaque","B. transparent","C. easily understood"], answer: "A" },
          { question: "The Hawthorne Effect is linked to:",
                  options: ["A. perceived recognition", "B. poor working conditions","C. regular working hours"], answer: "A" },
          { question: "Good communication skills should be possessed by the:",
            options: ["A. sender and the recipient","B. sender only","C. recipient only"], answer: "A" },
          { question: "Information on an urgent safety-related maintenance action can be disseminated by:",
            options: ["A. locally authorised hand-written amendment to the maintenance manual",
                      "B. alert bulletin from a manufacturer",
                      "C. formal revision procedure to the maintenance manual only"], answer: "B" },
          { question: "Records of completed work should be completed:",
            options: ["A. at shift handovers","B. at the end of a maintenance task","C. progressively as the work is carried out"], answer: "C" },
          { question: "Backup discs or tapes of maintenance records kept on computers should be held:",
            options: ["A. at the computer terminal","B. in a separate location","C. by the supervisor"], answer: "B" },
          { question: "The effective dissemination of information is an essential part of the:",
            options: ["A. safety culture","B. team culture","C. Integrated Maintenance Information System"], answer: "A" },
          { question: "An alerting system for a vital aircraft system failure should ideally be:",
            options: ["A. a warning light","B. a dolls eye","C. an audio warning"], answer: "C" },
          { question: "The behaviour pattern of an individual carrying out a standard maintenance procedure would be:",
            options: ["A. rule-based","B. skill-based","C. motor-based"], answer: "A" },
          { question: "A motor programme is:",
            options: ["A. rule-based behaviour that requires no conscious thought",
                      "B. a learned behaviour that does not require conscious thought",
                      "C. skill-based behaviour that requires conscious thought"], answer: "B" },
          { question: "When carrying out a cockpit drill in response to an engine fire warning you are using:",
            options: ["A. rule-based behaviour","B. skill-based behaviour","C. knowledge-based behaviour"], answer: "A" },
          { question: "The biggest risk of error associated with using checklists is that:",
            options: ["A. they can be misread","B. they can invoke automatic responses","C. the user may be distracted"], answer: "B" },
          { question: "Skill-based behaviour is associated with:",
            options: ["A. experience","B. rules","C. motor programmes"], answer: "C" },
          { question: "An individual who has developed his/her own unauthorised way of regularly performing a task is:",
            options: ["A. in routine violation","B. using initiative","C. unintentionally in error"], answer: "A" },
          { question: "A wrongly set torque wrench would most likely produce a",
            options: ["A. variable error","B. constant error","C. Type 1 error"], answer: "B" },
          { question: "An inspector who fails to detect a fault and passes an item as serviceable when it is not has made a:",
            options: ["A. latent error","B. active error","C. Type II error"], answer: "C" },
          { question: "A Maintenance Error Management System (MEMS) is used to:",
            options: ["A. investigate reports on all incidents and accidents",
                      "B. process Mandatory Occurrence Reports (MORs) only",
                      "C. investigate Confidential Human Incident Reports (CHIRP) only"], answer: "A" },
          { question: "When a mechanic inadvertently carries out a procedure that is no longer current he/she has made an error connected to:",
            options: ["A. optimised violation","B. environmental capture","C. reversionary behaviour"], answer: "C" },
          { question: "Violations are errors that are:",
            options: ["A. always unintentional","B. always intentional","C. intentional or unintentional"], answer: "B" },
          { question: "The duty of care for the health and safety of people at work rests with:",
            options: ["A. employers only","B. the Health and Safety Executive","C. employers and employees"], answer: "C" },
          { question: "The three basic steps in dealing with an emergency are:",
            options: ["A. assess, make safe and then summon assistance",
                      "B. make safe, summon assistance and then assess",
                      "C. summon assistance, assess and then make safe"], answer: "A" },
          { question: "When dealing with an emergency, the first priority is to protect:",
            options: ["A. buildings and equipment","B. yourself and others","C. others only"], answer: "B" },
          { question: "When evacuating casualties you would first move:",
            options: ["A. walking wounded","B. fatalities","C. the most seriously wounded if incapacitated"], answer: "A" },
          { question: "When faced with casualties that have been overcome with gas, you should:",
            options: ["A. treat the casualties, ventilate the area and then turn off the gas supply",
                      "B. turn off the gas supply, ventilate the area and then treat the casualties",
                      "C. ventilate the area, treat the casualties and then turn off the gas supply"], answer: "B" },
          { question: "Hazards found in the workplace are the result of unsafe:",
            options: ["A. human conditions only","B. environmental conditions only","C. human and environmental conditions"], answer: "C" },
            {
        question: "What constitutes a good handover?",
        options: ["A. Verbal", "B. Written", "C. Written plus verbal"],
        answer: "C",
      },
        ];

        function shuffle(array) {
          for (let i = array.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [array[i], array[j]] = [array[j], array[i]];
          }
          return array;
        }
        function fmtTime(s) {
          const m = Math.floor(s / 60).toString().padStart(2, "0");
          const sec = (s % 60).toString().padStart(2, "0");
          return m + ":" + sec;
        }
        function showView(idToShow) {
          ["welcome","quiz","results","bank"].forEach(id => {
            const el = document.getElementById(id);
            if (!el) return;
            if (id === idToShow) el.classList.remove("hidden");
            else el.classList.add("hidden");
          });
          window.scrollTo({ top: 0, behavior: "smooth" });
        }

        /* ====== 深色模式：持久化 ====== */
        const darkBtn = document.getElementById("darkModeToggle");
        function applyInitialTheme() {
          try {
            const saved = localStorage.getItem('theme');
            const isDark = (saved === 'dark') || (!saved && window.matchMedia('(prefers-color-scheme: dark)').matches);
            document.body.classList.toggle('dark', isDark);
            darkBtn.setAttribute('aria-pressed', String(isDark));
          } catch(e) {}
          document.documentElement.classList.remove('preload-dark');
        }
        applyInitialTheme();
        darkBtn.addEventListener('click', function(){
          const willDark = !document.body.classList.contains('dark');
          document.body.classList.toggle('dark', willDark);
          darkBtn.setAttribute('aria-pressed', String(willDark));
          try { localStorage.setItem('theme', willDark ? 'dark' : 'light'); } catch(e){}
        });

        /* ====== 測驗狀態 ====== */
        let shuffledQuestions;
        let current = 0, total = 0, timer = 80 * 60, interval, answers = [];
        let quizActive = false;
        const progressBar = document.getElementById("progressBar");

        /* ====== 元件 ====== */
        const startBtn = document.getElementById("startBtn");
        const prevBtn = document.getElementById("prevBtn");
        const leaveBtn = document.getElementById("leaveBtn");
        const retryBtn = document.getElementById("retryBtn");
        const showWrongBtn = document.getElementById("showWrongBtn");
        const showAllBtn = document.getElementById("showAllBtn");
        const openBankBtn = document.getElementById("openBankBtn");
        const toBankFromResults = document.getElementById("toBankFromResults");

        /* ====== 題庫瀏覽 ====== */
        const bankBody = document.getElementById("bankBody");
        const bankSearch = document.getElementById("bankSearch");
        const perPageSel = document.getElementById("perPage");
        const pageInfo = document.getElementById("pageInfo");
        const prevPageBtn = document.getElementById("prevPage");
        const nextPageBtn = document.getElementById("nextPage");
        const backToWelcome = document.getElementById("backToWelcome");
        const pagination = document.querySelector('#bank .pagination');

        let bankFiltered = questions.slice();
        let page = 1;
        function totalPages() {
          const sel = perPageSel.value;
          if (sel === 'all') return 1;
          return Math.max(1, Math.ceil(bankFiltered.length / parseInt(sel || "10")));
        }

        /* ====== 測驗流程 ====== */
        startBtn.addEventListener("click", () => {
          const n = document.getElementById("nameInput").value.trim();
          const qLimit = parseInt(document.getElementById("questionLimit").value);

          if (!n) return alert("請輸入姓名 / Enter your name");
          if (!qLimit || qLimit <= 0) return alert("請輸入要作答的題數,最多5題 / Enter number of questions");

          shuffledQuestions = shuffle(questions.slice()).slice(0, Math.min(qLimit, questions.length));
          total = shuffledQuestions.length;
          current = 0; answers = []; timer = 80 * 60;
          quizActive = true;

          document.getElementById("welcomeName").innerText = "歡迎: " + n;
          document.getElementById("total").innerText = total;
          updateProgress();

          interval = setInterval(() => {
            if (timer > 0 && quizActive) {
              timer--;
              document.getElementById("timer").innerText = fmtTime(timer);
            } else if (quizActive && timer <= 0) {
              clearInterval(interval);
              finish();
            }
          }, 1000);

          showQ();
          showView("quiz");
        });

        prevBtn.addEventListener("click", () => {
          if (current > 0) {
            current--;
            answers.pop();
            showQ();
          }
        });

        leaveBtn.addEventListener("click", finish);
        retryBtn.addEventListener("click", () => location.reload());
        showWrongBtn.addEventListener("click", () => renderResults(answers.filter(a => !a.correct)));
        showAllBtn.addEventListener("click", () => renderResults(answers));
        openBankBtn.addEventListener("click", enterBank);
        toBankFromResults.addEventListener("click", enterBank);

        /* ====== 題庫事件 ====== */
        bankSearch.addEventListener("input", applyFilter);
        perPageSel.addEventListener("change", () => { page = 1; renderBank(); });
        prevPageBtn.addEventListener("click", () => { if (page > 1) { page--; renderBank(); } });
        nextPageBtn.addEventListener("click", () => { if (page < totalPages()) { page++; renderBank(); } });
        backToWelcome.addEventListener("click", () => showView("welcome"));

        function enterBank() {
          if (quizActive) { alert("測驗進行中不可瀏覽題庫。請先完成或離開考試。"); return; }
          if (!bankSearch.value) { bankFiltered = questions.slice(); page = 1; }
          renderBank();
          showView("bank");
        }

        function applyFilter() {
          const kw = bankSearch.value.trim().toLowerCase();
          bankFiltered = kw
            ? questions.filter(q => q.question.toLowerCase().includes(kw) ||
                                    q.options.some(o => o.toLowerCase().includes(kw)))
            : questions.slice();
          page = 1; renderBank();
        }

        function renderBank() {
          bankBody.innerHTML = "";
          const sel = perPageSel.value;
          const per = (sel === 'all') ? bankFiltered.length : parseInt(sel || "10");
          const start = (page - 1) * per;
          const items = (sel === 'all') ? bankFiltered.slice() : bankFiltered.slice(start, start + per);

          items.forEach((q, idx) => {
            const tr = document.createElement("tr");
            const num = (sel === 'all') ? (idx + 1) : (start + idx + 1);
            const correctText = q.options.find(o => o.charAt(0) === q.answer) || "";

            const optsHtml = q.options.map(o => {
              const isC = (o.charAt(0) === q.answer);
              return `<span class="opt-row ${isC ? 'is-correct' : ''}">${isC ? '<span class="ans-chip">正解</span>' : ''}${o}</span>`;
            }).join("");

            tr.innerHTML =
              '<td class="mono">#' + num + "</td>" +
              "<td>" + q.question + "</td>" +
              "<td>" + optsHtml + "</td>" +
              '<td class="mono ans-cell">' + (q.answer + "｜" + correctText) + "</td>";
            bankBody.append(tr);
          });

          const tp = totalPages();
          if (sel === 'all') {
            if (pagination) pagination.style.display = 'none';
            pageInfo.textContent = "全部顯示（共 " + bankFiltered.length + " 題）";
            prevPageBtn.disabled = true; nextPageBtn.disabled = true;
          } else {
            if (pagination) pagination.style.display = 'flex';
            pageInfo.textContent = "第 " + page + " / " + tp + " 頁（共 " + bankFiltered.length + " 題）";
            prevPageBtn.disabled = (page <= 1); nextPageBtn.disabled = (page >= tp);
          }
        }

        /* ====== 測驗：出題/進度/結束 ====== */
        function showQ() {
          if (current >= total) return finish();
          document.getElementById("current").innerText = current + 1;
          updateProgress();

          const q = shuffledQuestions[current];
          document.getElementById("questionText").innerText = q.question;

          const optDiv = document.getElementById("options");
          optDiv.innerHTML = "";

          let optionsWithFlag = q.options.map(option => ({ text: option, isAnswer: option.charAt(0) === q.answer }));
          optionsWithFlag = shuffle(optionsWithFlag);

          optionsWithFlag.forEach(opt => {
            const lbl = document.createElement("label");
            const rd = document.createElement("input");
            rd.type = "radio"; rd.name = "opt"; rd.value = opt.text;
            rd.onchange = function () {
              answers.push({
                q, selectedText: opt.text,
                correctText: q.options.find(optItem => optItem.charAt(0) === q.answer),
                correct: opt.isAnswer
              });
              current++; showQ();
            };
            lbl.append(rd, " ", opt.text);
            optDiv.append(lbl);
          });
        }

        function updateProgress() {
          const percent = (current / total) * 100;
          progressBar.style.width = percent + "%";
        }

        function finish() {
          clearInterval(interval);
          quizActive = false; // 結束後可進入題庫
          showView("results");
          renderResults(answers);
          document.getElementById("scoreSummary").innerText =
            "答對 " + answers.filter(a => a.correct).length +
            " 題 / 已作答 " + answers.length + " 題 / 共 " + total + " 題";
        }

        function renderResults(data) {
          const tb = document.getElementById("resultsBody");
          tb.innerHTML = "";
          data.forEach(a => {
            const tr = document.createElement("tr");
            tr.innerHTML =
              "<td>" + a.q.question + "</td>" +
              "<td>" + a.selectedText + "</td>" +
              '<td class="ans-cell">' + a.correctText + "</td>" +
              "<td>" + (a.correct ? "O" : "X") + "</td>";
            if (!a.correct) tr.classList.add("wrong");
            tb.append(tr);
          });
        }
      });
    </script>
  </body>
</html>


</html>
