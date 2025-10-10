<吃飽太閒做的網站，能幫到你我覺得很開心>
<html lang="zh-Hant">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>147測驗｜單一檔案版</title>
    <style>
                  /* 回首頁浮動按鈕 */
            #homeBtn {
        position: absolute;
        top: 100px;               /* 深色模式在20px，這裡放在它下方 */
        right: 20px;
        padding: 10px 20px;
        background: #28a745;
        color: #fff;
        border: none;
        border-radius: 8px;
        text-decoration: none;
        font-size: 1em;
        box-shadow: 0 4px 12px rgba(0,0,0,.15);
        transition: background .3s, transform .2s, box-shadow .2s;
        z-index: 1000;
      }
      #homeBtn:hover {
        background: #218838;
        transform: translateY(-2px);
        box-shadow: 0 6px 16px rgba(0,0,0,.25);
      }
      body.dark #homeBtn {
        background: #2e7d32;
      }
      body.dark #homeBtn:hover {
        background: #25652a;
      }

                  body {
                    font-family: Arial, sans-serif;
                    margin: 0;
                    padding: 40px;
                    font-size: 1.6em;
                    background: #f0f4f8;
                    color: #000;
                    transition: background-color 0.5s, color 0.5s;
                  }
                  body.dark { background: #121212; color: #fff; }
                  #container {
                    max-width: 1200px; margin: auto; background: #fff; padding: 40px;
                    border-radius: 20px; box-shadow: 0 0 10px rgba(0,0,0,.1);
                    transition: background-color .5s, color .5s;
                  }
                  body.dark #container { background: #1e1e1e; }
                  .hidden { display: none; }
                  h1, h2 { text-align: center; font-size: 2.4em; }
                  #rules {
                    background: #e9ecef; padding: 20px; margin-bottom: 40px;
                    border-radius: 10px; font-size: 1.2em;
                  }
                  body.dark #rules { background: #333; }
                  .btn {
                    background: #007bff; color: #fff; border: none; padding: 20px 40px;
                    margin: 10px; border-radius: 10px; cursor: pointer; font-size: 1.2em;
                    transition: background-color .3s;
                  }
                  .btn:hover { background: #0056b3; }
                  #leaveBtn { background: #dc3545; }
                  #progress, #timer { font-weight: bold; font-size: 1.4em; }
                  .progress-container {
                    background: #ddd; height: 10px; border-radius: 5px; margin-top: 20px; overflow: hidden;
                  }
                  body.dark .progress-container { background: #555; }
                  .progress-bar { height: 100%; width: 0; background: #007bff; transition: width .6s ease; }
                  .question { margin: 40px 0 20px; font-size: 1.8em; }
                  .options label { display: block; margin-bottom: 16px; font-size: 1.4em; }
                  table { width: 100%; border-collapse: collapse; margin-top: 40px; font-size: 1.2em; }
                  th, td { border: 1px solid #ccc; padding: 16px; text-align: left; }
                  tr.wrong { background-color: #ffe6e6; }
                  body.dark tr.wrong { background-color: #661111; }
                  #darkModeToggle {
                    position: absolute; top: 20px; right: 20px; padding: 10px 20px;
                    background: #333; color: #fff; border: none; border-radius: 8px; cursor: pointer; font-size: 1em;
                    transition: background .3s;
                  }
                  #darkModeToggle:hover { background: #555; }
    </style>
  </head>
  <body>
    <button id="darkModeToggle">深色模式 / Dark Mode</button>
    <a id="homeBtn" href="https://hisausage7.github.io/147test/" title="回首頁"
      >🏠 回首頁</a
    >

    <div id="container">
      <div id="welcome">
        <h1>147測驗M9校內考</h1>
        <div id="rules">
          <p><strong>考試注意事項 / Exam Rules:</strong></p>
          <p>
            1. 請輸入姓名後才能開始作答。 / You must enter your name to start
            the quiz.
          </p>
          <p>
            2. 考試限時80分鐘，自動倒數。 / The quiz is timed for 80 minutes,
            countdown starts immediately.
          </p>
          <p>
            3. 作答途中可隨時點擊「離開考試」提前結束。 / You can click "Leave
            Quiz" anytime to finish early.
          </p>
          <p>
            4. 完成後會自動顯示所有答題結果與成績。 / Results and scores will be
            displayed after completion.
          </p>
          <p>
            5. 答對題目顯示O，答錯題目顯示X。 / Correct answers will show O,
            incorrect answers will show X.
          </p>
          <p>
            6. 測驗過程為亂序出題。 / The test process was chaotic and
            disordered in setting questions.
          </p>
          <p>!版權及源代碼所有-航機系008沈崑宸!</p>
          <p>!僅作為自我測驗使用!</p>
        </div>
        <input
          type="text"
          id="nameInput"
          placeholder="輸入姓名 / Enter your name"
          style="width:100%;padding:8px;margin-bottom:10px;font-size:1.4em;"
        />
        <input
          type="number"
          id="questionLimit"
          placeholder="輸入題數,至多102題 / Enter number of questions"
          style="width:100%;padding:8px;margin-bottom:10px;font-size:1.4em;"
        />
        <button id="startBtn" class="btn">開始測驗 / Start Quiz</button>
      </div>

      <div id="quiz" class="hidden">
        <div>
          <span id="welcomeName"></span>
          <span id="timer" style="float:right">80:00</span>
        </div>
        <div id="progress">
          題數: <span id="current">0</span> / <span id="total">0</span>
        </div>
        <div class="progress-container">
          <div id="progressBar" class="progress-bar"></div>
        </div>
        <div class="question" id="questionText"></div>
        <div class="options" id="options"></div>
        <button id="prevBtn" class="btn" style="background:#6c757d">
          上一題 / Previous
        </button>
        <button id="leaveBtn" class="btn">離開考試 / Leave Quiz</button>
      </div>

      <div id="results" class="hidden">
        <h2>測驗結果 / Results</h2>
        <div>
          <button id="retryBtn" class="btn">重新開始 / Retry</button>
          <button id="showWrongBtn" class="btn" style="background:#ffc107">
            只看錯題 / Wrong Only
          </button>
          <button id="showAllBtn" class="btn">看全部結果 / Show All</button>
        </div>
        <table>
          <thead>
            <tr>
              <th>題目</th>
              <th>您的答案</th>
              <th>正確答案</th>
              <th>結果</th>
            </tr>
          </thead>
          <tbody id="resultsBody"></tbody>
        </table>
        <div
          id="scoreSummary"
          style="text-align:center;margin-top:20px;font-size:1.2em"
        ></div>
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
                      "C. turn off the gas supply, ventilate the area and then treat the casualties"], answer: "B" },
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

        let shuffledQuestions;
        let current = 0, total = 0, timer = 80 * 60, interval, answers = [];

        function fmtTime(s) {
          const m = Math.floor(s / 60).toString().padStart(2, "0");
          const sec = (s % 60).toString().padStart(2, "0");
          return m + ":" + sec;
        }

        const startBtn = document.getElementById("startBtn");
        const prevBtn = document.getElementById("prevBtn");
        const leaveBtn = document.getElementById("leaveBtn");
        const retryBtn = document.getElementById("retryBtn");
        const showWrongBtn = document.getElementById("showWrongBtn");
        const showAllBtn = document.getElementById("showAllBtn");
        const darkModeToggle = document.getElementById("darkModeToggle");
        const progressBar = document.getElementById("progressBar");

        startBtn.addEventListener("click", () => {
          const n = document.getElementById("nameInput").value.trim();
          const qLimit = parseInt(document.getElementById("questionLimit").value);

          if (!n) return alert("請輸入姓名 / Enter your name");
          if (!qLimit || qLimit <= 0) return alert("請輸入要作答的題數,最多105題 / Enter number of questions");

          shuffledQuestions = shuffle([...questions]).slice(0, Math.min(qLimit, questions.length));
          total = shuffledQuestions.length;
          current = 0; answers = []; timer = 80 * 60;

          document.getElementById("welcome").classList.add("hidden");
          document.getElementById("quiz").classList.remove("hidden");
          document.getElementById("welcomeName").innerText = "歡迎: " + n;
          document.getElementById("total").innerText = total;
          updateProgress();

          interval = setInterval(() => {
            if (timer > 0) {
              timer--;
              document.getElementById("timer").innerText = fmtTime(timer);
            } else {
              clearInterval(interval);
              finish();
            }
          }, 1000);

          showQ();
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
        showWrongBtn.addEventListener("click", filterResultsWrong);
        showAllBtn.addEventListener("click", showAllResults);
        darkModeToggle.addEventListener("click", () => document.body.classList.toggle("dark"));

        function showQ() {
          if (current >= total) return finish();
          document.getElementById("current").innerText = current + 1;
          updateProgress();

          const q = shuffledQuestions[current];
          document.getElementById("questionText").innerText = q.question;

          const optDiv = document.getElementById("options");
          optDiv.innerHTML = "";

          let optionsWithFlag = q.options.map((option) => ({
            text: option,
            isAnswer: option.charAt(0) === q.answer,
          }));
          optionsWithFlag = shuffle(optionsWithFlag);

          optionsWithFlag.forEach((opt) => {
            const lbl = document.createElement("label");
            const rd = document.createElement("input");
            rd.type = "radio";
            rd.name = "opt";
            rd.value = opt.text;
            rd.onchange = () => {
              answers.push({
                q,
                selectedText: opt.text,
                correctText: q.options.find((optItem) => optItem.charAt(0) === q.answer),
                correct: opt.isAnswer,
              });
              current++;
              showQ();
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
          document.getElementById("quiz").classList.add("hidden");
          document.getElementById("results").classList.remove("hidden");
          renderResults(answers);
          document.getElementById("scoreSummary").innerText =
            `答對 ${answers.filter((a) => a.correct).length} 題 / 已作答 ${answers.length} 題 / 共 ${total} 題`;
          window.scrollTo({ top: 0, behavior: "smooth" });
        }

        function renderResults(data) {
          const tb = document.getElementById("resultsBody");
          tb.innerHTML = "";
          data.forEach((a) => {
            const tr = document.createElement("tr");
            tr.innerHTML = `
              <td>${a.q.question}</td>
              <td>${a.selectedText}</td>
              <td>${a.correctText}</td>
              <td>${a.correct ? "O" : "X"}</td>
            `;
            if (!a.correct) tr.classList.add("wrong");
            tb.append(tr);
          });
        }

        function filterResultsWrong() { renderResults(answers.filter((a) => !a.correct)); }
        function showAllResults() { renderResults(answers); }
      });
    </script>
  </body>
</html>
