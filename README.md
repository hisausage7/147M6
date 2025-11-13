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
      >🏠 回首頁</a>
    <div id="container">
      <div id="welcome">
        <h1>147測驗M6校內考
        </h1>
        <div id="rules">
          <p><strong>考試注意事項 / Exam Rules:</strong></p>
          <P>!此章節沒有提供圖片題!
          </p>1. 請輸入姓名後才能開始作答。 / You must enter your name to startthe quiz.</p>
          <p>2. 考試限時80分鐘，自動倒數。 / The quiz is timed for 80 minutes,countdown starts immediately.</p>
          <p>3. 作答途中可隨時點擊「離開考試」提前結束。 / You can click "LeaveQuiz" anytime to finish early.</p>
          <p>4. 完成後會自動顯示所有答題結果與成績。 / Results and scores will bedisplayed after completion.</p>
          <p>5. 答對題目顯示O，答錯題目顯示X。 / Correct answers will show O,incorrect answers will show X.</p>
          <p>6. 測驗過程為亂序出題。 / The test process was chaotic anddisordered in setting questions.</p>
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
          placeholder="輸入題數,至多250題 / Enter number of questions"
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
              const questions =   [
                [
  {
    question: "Ferrous metals are so-called because their main constituent is:",
    options: ["A. carbon", "B. iron", "C. cementite"],
    answer: "B"
  },
  {
    question: "A metal's resistance to fracture under the action of external bending or impact forces is called:",
    options: ["A. hardness", "B. strength", "C. toughness"],
    answer: "C"
  },
  {
    question: "The maximum percentage of carbon that can be dissolved in iron at room temperature is:",
    options: [
      "A. less than when the iron is above its upper critical temperature",
      "B. more than when it is above its upper critical temperature",
      "C. the same regardless of the temperature of the iron"
    ],
    answer: "A"
  },
  {
    question: "Steel is a term given to:",
    options: [
      "A. iron that contains a percentage of carbon in solution",
      "B. iron that contains one or more elements in addition to carbon",
      "C. a metal that is predominantly made of iron"
    ],
    answer: "A"
  },
  {
    question: "High carbon steel contains:",
    options: [
      "A. 0.2% to 0.5% carbon",
      "B. 0.7% to 1.5% carbon",
      "C. 2% to 5% carbon"
    ],
    answer: "B"
  },
  {
    question: "An alloy containing 75% nickel and 25% cobalt would be called:",
    options: [
      "A. nickel steel alloy",
      "B. high nickel alloy",
      "C. low cobalt steel alloy"
    ],
    answer: "B"
  },
  {
    question: "Stainless steels must contain a minimum chromium percentage of:",
    options: ["A. 3%", "B. 5%", "C. 12%"],
    answer: "C"
  },
  {
    question: "Chromium is added to steel to:",
    options: [
      "A. give a fine grain structure and reduce brittleness",
      "B. increase its work-hardening capacity",
      "C. increase hardness and corrosion resistance"
    ],
    answer: "C"
  },
  {
    question: "Temper brittleness is a feature of:",
    options: [
      "A. nickel steel",
      "B. austenitic stainless steel",
      "C. high carbon steel"
    ],
    answer: "B"
  },
  {
    question: "A property of 'Invar' steel is that it:",
    options: [
      "A. has an extremely low coefficient of expansion",
      "B. has very high permeability",
      "C. self-hardens under mechanical pressure"
    ],
    answer: "A"
  },
  {
    question: "A small percentage of lead is added to some steels to:",
    options: [
      "A. improve their machinability",
      "B. reduce their brittleness",
      "C. improve their wear resistance"
    ],
    answer: "A"
  },
  {
    question: "A suitable material for use in an aircraft landing gear structure would be:",
    options: [
      "A. high carbon steel",
      "B. tungsten, cobalt alloy steel",
      "C. chrome, molybdenum alloy steel"
    ],
    answer: "C"
  },
  {
    question: "A suitable alloy for use in an engine turbine wheel would be:",
    options: [
      "A. ferritic stainless steel",
      "B. martensitic stainless steel",
      "C. medium carbon steel"
    ],
    answer: "A"
  },
  {
    question: "Austenitic steel:",
    options: [
      "A. does not expand or contract",
      "B. does not respond to heat treatment",
      "C. is magnetic"
    ],
    answer: "B"
  },
  {
    question: "When carbon steel is being 'tempered' it is cooled:",
    options: [
      "A. slowly in the furnace",
      "B. freely in still air",
      "C. by quenching"
    ],
    answer: "C"
  },
  {
    question: "When nickel is added to steel its main effect is to increase:",
    options: [
      "A. toughness",
      "B. hardness",
      "C. corrosion resistance"
    ],
    answer: "A"
  },
  {
    question: "The heat treatment that softens steel and makes it more ductile is called:",
    options: [
      "A. tempering",
      "B. annealing",
      "C. normalising"
    ],
    answer: "B"
  },
  {
    question: "The heat treatment that relieves locked up stresses and refines grain structure is called:",
    options: [
      "A. tempering",
      "B. annealing",
      "C. normalising"
    ],
    answer: "C"
  },
  {
    question: "The 'fatigue limit' for a component is defined as:",
    options: [
      "A. the maximum load that can be endured for an infinite number of load cycles",
      "B. the load at which the component will instantly fail",
      "C. the minimum load that can be endured for an infinite number of load cycles"
    ],
    answer: "A"
  },
  {
    question: "Yield stress is the maximum stress that can be endured without:",
    options: [
      "A. fracture",
      "B. permanent distortion",
      "C. work hardening"
    ],
    answer: "B"
  },
  {
    question: "The hardness test that is most suited to very hard and very soft materials is the:",
    options: [
      "A. Brinell hardness test",
      "B. Vickers hardness test",
      "C. Barcol hardness test"
    ],
    answer: "B"
  },
  {
    question: "An impact test result for metal test pieces is a measure of the:",
    options: [
      "A. energy remaining after impacting and breaking the test piece",
      "B. energy at the start of the pendulum's swing",
      "C. energy absorbed by the test piece"
    ],
    answer: "C"
  },
  {
    question: "Which of these statements is false? (Remember? Read the question!)",
    options: [
      "A. brittle material cannot have high tensile strength",
      "B. brittle material cannot have high toughness",
      "C. brittle material cannot have high ductility"
    ],
    answer: "A"
  },
  {
    question: "Tungsten and chromium will harden carbon steel by:",
    options: [
      "A. dissolving in ferrite and creating a fine grain structure",
      "B. distorting the grain structure",
      "C. reacting with carbon and forming carbide"
    ],
    answer: "C"
  },
  {
    question: "The term 'high speed steel' refers to alloy steels that are used for:",
    options: [
      "A. high-speed aircraft",
      "B. high-speed cutting tools",
      "C. high rotational speed components"
    ],
    answer: "B"
  },


  { question: "Pure copper can be hardened by:", options: ["A. heat treatment","B. cold working","C. case hardening"], answer: "B" },
  { question: "Precipitation treatment is given to some alloys in order to:", options: ["A. make them softer and more ductile","B. harden them","C. relieve internal locked up stresses"], answer: "B" },
  { question: "Non-ferrous metals are defined as metals that:", options: ["A. contain no iron","B. are non-magnetic","C. do not contain iron as a major constituent"], answer: "C" },
  { question: "Bronze is basically an alloy of:", options: ["A. copper and tin","B. copper and zinc","C. tin and zinc"], answer: "A" },
  { question: "Pure aluminium possesses:", options: ["A. poor ductility","B. high strength","C. high corrosion resistance"], answer: "C" },
  { question: "When copper and nickel are alloyed together, they form a:", options: ["A. solid solution that cannot be precipitation hardened","B. partially solid solution that can be precipitation hardened","C. solid solution that can be precipitation hardened"], answer: "A" },
  { question: "'Alclad' is the trade name for:", options: ["A. pure aluminium sheet, clad with 5% thickness of Duralumin on each side","B. Duralumin sheet, clad with 5% thickness of pure aluminium on each side","C. Duralumin sheet, clad with 2.5% thickness of zinc on each side"], answer: "B" },
  { question: "A small percentage of copper is alloyed with aluminium alloy to:", options: ["A. increase electrical conductivity","B. reduce brittleness","C. permit precipitation hardening"], answer: "C" },
  { question: "The main constituent in the refractory 'super-alloys', such as Nimonic 80A is:", options: ["A. nickel","B. chromium","C. tungsten"], answer: "A" },
  { question: "Following the solution treatment of Duralumin, refrigeration will:", options: ["A. delay age hardening","B. accelerate age hardening","C. have no affect on age hardening"], answer: "A" },
  { question: "The specification for an aluminium alloy is 2024 – 0. The suffix 0 means the material is:", options: ["A. hardened","B. annealed","C. solution treated"], answer: "B" },
  { question: "When you have fabricated a component from a heat treatable aluminium alloy, the final heat treatment given prior to releasing it to service is:", options: ["A. stress relief and annealing","B. precipitation treatment only","C. solution treatment and precipitation treatment"], answer: "C" },
  { question: "A light alloy that would be most suited for an aircraft skin that has a working temperature of 180°C is:", options: ["A. Duralumin","B. titanium alloy","C. aluminium - magnesium alloy"], answer: "B" },
  { question: "When caustic soda is swabbed onto the surface of Duralumin, the surface turns:", options: ["A. black","B. white","C. effervescent white"], answer: "A" },
  { question: "The material that is most suited for use in the manufacture of flexible bellows and metal diaphragms in fluid control system units is:", options: ["A. aluminium bronze","B. antimony bronze","C. beryllium bronze"], answer: "C" },
  { question: "The aluminium alloy 2024 – T6 is:", options: ["A. aluminium – copper alloy that has been solution treated and artificially aged","B. aluminium – magnesium alloy that has been strain hardened","C. aluminium – zinc alloy that has been annealed"], answer: "A" },
  { question: "Alloys that are described as 'refractories' will:", options: ["A. maintain their mechanical properties at very high temperatures","B. lose their mechanical properties at very high temperatures","C. maintain their mechanical properties at very low temperatures"], answer: "A" },
  { question: "The temperatures and times to be used for the heat treatment of metals are:", options: ["A. contained in heat treatment tables issued by the standards authority","B. contained in the material specification sheet","C. marked on the material as a temper code"], answer: "B" },
  { question: "Heat treatable, clad aluminium copper alloy can be solution treated:", options: ["A. any number of times","B. a maximum of once only","C. a maximum of three times only"], answer: "C" },
  { question: "Antimony may be added to solder to:", options: ["A. harden it","B. soften it","C. act as a flux"], answer: "A" },
  { question: "The letter that accompanies a Rockwell hardness value (HR) indicates the:", options: ["A. material tested","B. additional force used","C. scale used"], answer: "C" },
  { question: "Solder is an alloy of:", options: ["A. zinc and lead","B. tin and lead","C. copper and lead"], answer: "B" },
  { question: "Tungsten is most suited for use in:", options: ["A. high strength, lightweight alloys","B. high-speed steels","C. softening nickel alloys"], answer: "B" },
  { question: "When annealing a 2XXX series aluminium alloy, it should be cooled:", options: ["A. rapidly by quenching in cold water","B. in air or by quenching","C. at a slow controlled rate"], answer: "C" },
  { question: "Tungsten, silicon and chromium belong to a group of materials that are well known for their ability to form:", options: ["A. oxides","B. molecules","C. carbides"], answer: "C" },
  {
    question: "Pure copper can be hardened by:",
    options: [
      "A. heat treatment",
      "B. cold working",
      "C. case hardening"
    ],
    answer: "B"
  },
  {
    question: "Precipitation treatment is given to some alloys in order to:",
    options: [
      "A. make them softer and more ductile",
      "B. harden them",
      "C. relieve internal locked up stresses"
    ],
    answer: "B"
  },
  {
    question: "Non-ferrous metals are defined as metals that:",
    options: [
      "A. contain no iron",
      "B. are non-magnetic",
      "C. do not contain iron as a major constituent"
    ],
    answer: "C"
  },
  {
    question: "Bronze is basically an alloy of:",
    options: [
      "A. copper and tin",
      "B. copper and zinc",
      "C. tin and zinc"
    ],
    answer: "A"
  },
  {
    question: "Pure aluminium possesses:",
    options: [
      "A. poor ductility",
      "B. high strength",
      "C. high corrosion resistance"
    ],
    answer: "C"
  },
  {
    question: "When copper and nickel are alloyed together, they form a:",
    options: [
      "A. solid solution that cannot be precipitation hardened",
      "B. partially solid solution that can be precipitation hardened",
      "C. solid solution that can be precipitation hardened"
    ],
    answer: "A"
  },
  {
    question: "'Alclad' is the trade name for:",
    options: [
      "A. pure aluminium sheet, clad with 5% thickness of Duralumin on each side",
      "B. Duralumin sheet, clad with 5% thickness of pure aluminium on each side",
      "C. Duralumin sheet, clad with 2.5% thickness of zinc on each side"
    ],
    answer: "B"
  },
  {
    question: "A small percentage of copper is alloyed with aluminium alloy to:",
    options: [
      "A. increase electrical conductivity",
      "B. reduce brittleness",
      "C. permit precipitation hardening"
    ],
    answer: "C"
  },
  {
    question: "The main constituent in the refractory 'super-alloys', such as Nimonic 80A is:",
    options: [
      "A. nickel",
      "B. chromium",
      "C. tungsten"
    ],
    answer: "A"
  },
  {
    question: "Following the solution treatment of Duralumin, refrigeration will:",
    options: [
      "A. delay age hardening",
      "B. accelerate age hardening",
      "C. have no affect on age hardening"
    ],
    answer: "A"
  },
  {
    question: "The specification for an aluminium alloy is 2024 – 0. The suffix 0 means the material is:",
    options: [
      "A. hardened",
      "B. annealed",
      "C. solution treated"
    ],
    answer: "B"
  },
  {
    question: "When you have fabricated a component from a heat treatable aluminium alloy, the final heat treatment given prior to releasing it to service is:",
    options: [
      "A. stress relief and annealing",
      "B. precipitation treatment only",
      "C. solution treatment and precipitation treatment"
    ],
    answer: "C"
  },
  {
    question: "A light alloy that would be most suited for an aircraft skin that has a working temperature of 180°C is:",
    options: [
      "A. Duralumin",
      "B. titanium alloy",
      "C. aluminium - magnesium alloy"
    ],
    answer: "B"
  },
  {
    question: "When caustic soda is swabbed onto the surface of Duralumin, the surface turns:",
    options: [
      "A. black",
      "B. white",
      "C. effervescent white"
    ],
    answer: "A"
  },
  {
    question: "The material that is most suited for use in the manufacture of flexible bellows and metal diaphragms in fluid control system units is:",
    options: [
      "A. aluminium bronze",
      "B. antimony bronze",
      "C. beryllium bronze"
    ],
    answer: "C"
  },
  {
    question: "The aluminium alloy 2024 – T6 is:",
    options: [
      "A. aluminium – copper alloy that has been solution treated and artificially aged",
      "B. aluminium – magnesium alloy that has been strain hardened",
      "C. aluminium – zinc alloy that has been annealed"
    ],
    answer: "A"
  },
  {
    question: "Alloys that are described as 'refractories' will:",
    options: [
      "A. maintain their mechanical properties at very high temperatures",
      "B. lose their mechanical properties at very high temperatures",
      "C. maintain their mechanical properties at very low temperatures"
    ],
    answer: "A"
  },
  {
    question: "The temperatures and times to be used for the heat treatment of metals are:",
    options: [
      "A. contained in heat treatment tables issued by the standards authority",
      "B. contained in the material specification sheet",
      "C. marked on the material as a temper code"
    ],
    answer: "B"
  },
  {
    question: "Heat treatable, clad aluminium copper alloy can be solution treated:",
    options: [
      "A. any number of times",
      "B. a maximum of once only",
      "C. a maximum of three times only"
    ],
    answer: "C"
  },
  {
    question: "Antimony may be added to solder to:",
    options: [
      "A. harden it",
      "B. soften it",
      "C. act as a flux"
    ],
    answer: "A"
  },
  {
    question: "The letter that accompanies a Rockwell hardness value (HR) indicates the:",
    options: [
      "A. material tested",
      "B. additional force used",
      "C. scale used"
    ],
    answer: "C"
  },
  {
    question: "Solder is an alloy of:",
    options: [
      "A. zinc and lead",
      "B. tin and lead",
      "C. copper and lead"
    ],
    answer: "B"
  },
  {
    question: "Tungsten is most suited for use in:",
    options: [
      "A. high strength, lightweight alloys",
      "B. high-speed steels",
      "C. softening nickel alloys"
    ],
    answer: "A"
  },
  {
    question: "When annealing a 2XXX series aluminium alloy, it should be cooled:",
    options: [
      "A. rapidly by quenching in cold water",
      "B. in air or by quenching",
      "C. at a slow controlled rate"
    ],
    answer: "C"
  },
  {
    question: "Tungsten, silicon and chromium belong to a group of materials that are well known for their ability to form:",
    options: [
      "A. oxides",
      "B. molecules",
      "C. carbides"
    ],
    answer: "C"
  },
  {
    question: "The two main types of synthetic fabric materials are:",
    options: [
      "A. cotton and linen",
      "B. nylon and terylene fibre",
      "C. polyester fibre and glass fibre"
    ],
    answer: "C"
  },
  {
    question: "The seam normally used when machine stitching fabric materials is the:",
    options: [
      "A. blanket seam",
      "B. balloon seam",
      "C. lap seam"
    ],
    answer: "B"
  },
  {
    question: "The hand sewing stitch most commonly used for fabric repairs is the:",
    options: [
      "A. overlock stitch",
      "B. lock knot",
      "C. herringbone stitch"
    ],
    answer: "C"
  },
  {
    question: "Polyester fibre fabric is tautened by:",
    options: [
      "A. heat",
      "B. dope",
      "C. over-locking"
    ],
    answer: "A"
  },
  {
    question: "Glass fibre fabric material is tautened with:",
    options: [
      "A. nitrate dope",
      "B. butyrate dope",
      "C. heat"
    ],
    answer: "B"
  },
  {
    question: "Fabric should be replaced when its tensile strength when compared to new fabric falls below:",
    options: [
      "A. 50%",
      "B. 80%",
      "C. 70%"
    ],
    answer: "C"
  },
  {
    question: "The dope that is normally used for the first priming coat on natural and synthetic fabrics is:",
    options: [
      "A. butyrate dope",
      "B. acetate dope",
      "C. nitrate dope"
    ],
    answer: "C"
  },
  {
    question: "Fabric materials should be stored at a temperature of about:",
    options: [
      "A. 35°C",
      "B. 20°C",
      "C. 15°C"
    ],
    answer: "B"
  },
  {
    question: "Glass fibre fabrics are pre-treated during manufacture with:",
    options: [
      "A. nitrate dope",
      "B. butyrate dope",
      "C. fungicide"
    ],
    answer: "B"
  },
  {
    question: "A fungicidal additive is contained in the:",
    options: [
      "A. finishing coat",
      "B. filling coat",
      "C. priming coat"
    ],
    answer: "C"
  },
  {
    question: "The priming coat of dope is applied to natural fabric by:",
    options: [
      "A. brushing with thinned nitrate dope",
      "B. spraying with thinned nitrate dope",
      "C. brushing with thinned butyrate dope"
    ],
    answer: "A"
  },
  {
    question: "Blushing is a local discolouration of a doped finish that is caused by:",
    options: [
      "A. spraying over partly dried dope",
      "B. holding the spray gun too far away from the fabric",
      "C. application of dope in high ambient humidity"
    ],
    answer: "C"
  },
  {
    question: "The correct pitch for a herringbone stitch is:",
    options: [
      "A. 0.5 in or 12mm",
      "B. 0.25 in or 6mm",
      "C. 0.75 in or 18mm"
    ],
    answer: "B"
  },
  {
    question: "Aluminium dope is used to:",
    options: [
      "A. protect fabric from UV radiation",
      "B. give fabric a pleasing finish",
      "C. strengthen the fabric"
    ],
    answer: "A"
  },
  {
    question: "Fabric testing is carried out to check for:",
    options: [
      "A. tensile strength",
      "B. tautness",
      "C. moisture content"
    ],
    answer: "A"
  },
  {
    question: "When testing a fabric covering with a portable punch tester, the reading that is taken to represent the fabric condition is the:",
    options: [
      "A. highest recorded",
      "B. lowest recorded",
      "C. average of all readings"
    ],
    answer: "B"
  },
  {
    question: "Rib stringing is carried out on a wing fabric covering to:",
    options: [
      "A. prevent the top fabric lifting in flight",
      "B. stiffen the box structure",
      "C. support the rib structure when the fabric tautens"
    ],
    answer: "A"
  },
  {
    question: "Hard waxing of a doped finish is carried out:",
    options: [
      "A. immediately after the finishing coat has dried and then at monthly intervals",
      "B. one year after the finishing coat has dried and then annually",
      "C. one month after the finishing coat has dried and then annually"
    ],
    answer: "C"
  },
  {
    question: "Cotton fabric is 'mercerised' during manufacture to:",
    options: [
      "A. bleach it",
      "B. strengthen it",
      "C. remove the 'nap'"
    ],
    answer: "B"
  },
  {
    question: "If serrated scissors are not available, the edges of a repair patch may be:",
    options: [
      "A. hand frayed back by 6mm",
      "B. serrated using plain scissors",
      "C. sealed with serrated surface tape"
    ],
    answer: "A"
  },
  {
    question: "The thread angle of an ISO Metric thread is:",
    options: [
      "A. 55°",
      "B. 47½°",
      "C. 60°"
    ],
    answer: "C"
  },
  {
    question: "BA bolts are used on aircraft in place of BSF when:",
    options: [
      "A. the bolt diameter is less than 1/4 in",
      "B. the bolt diameter is greater than 1/4 in",
      "C. quick assembly is required"
    ],
    answer: "A"
  },
  {
    question: "The 'lead' on a multi-start thread is:",
    options: [
      "A. equal to the pitch",
      "B. the pitch multiplied by the number of starts",
      "C. the pitch divided by the number of starts"
    ],
    answer: "B"
  },
  {
    question: "UNJ threads are designed for:",
    options: [
      "A. fast assembly",
      "B. high temperature regions",
      "C. increased fatigue strength"
    ],
    answer: "C"
  },
  {
    question: "The pitch of a screw thread is measured from:",
    options: [
      "A. root to crest",
      "B. crest to adjoining crest",
      "C. flank centre to adjoining flank centre"
    ],
    answer: "B"
  },
  {
    question: "The 'lead' of a single start thread is:",
    options: [
      "A. equal to the pitch",
      "B. twice the pitch",
      "C. half the pitch"
    ],
    answer: "A"
  },
  {
    question: "Multi-start threads will increase the:",
    options: [
      "A. lead and the pitch",
      "B. lead without increasing the pitch",
      "C. pitch without increasing the lead"
    ],
    answer: "B"
  },
  {
    question: "A Buttress thread will transmit mechanical effort in:",
    options: [
      "A. both directions",
      "B. neither direction",
      "C. one direction only"
    ],
    answer: "C"
  },
  {
    question: "The thread angle of a screw thread is:",
    options: [
      "A. the angle included between adjacent flanks",
      "B. the angle between a flank and a line drawn perpendicular to the thread axis",
      "C. the helix angle of the thread"
    ],
    answer: "A"
  },
  {
    question: "The 'virtual' effective diameter of a thread is the:",
    options: [
      "A. diameter of a thread at half flank length",
      "B. altered position of the effective diameter due to pitch and flank angle errors",
      "C. altered position of the effective diameter due to the maximum metal condition"
    ],
    answer: "B"
  },
  {
    question: "The minor diameter of an internal thread is the:",
    options: [
      "A. root diameter",
      "B. crest diameter",
      "C. pitch diameter"
    ],
    answer: "B"
  },
  {
    question: "A ring gauge is used to check:",
    options: [
      "A. external thread diameters and pitch",
      "B. internal thread diameters and pitch",
      "C. external thread diameters and ovality"
    ],
    answer: "A"
  },
  {
    question: "UNJ threads are produced to:",
    options: [
      "A. Class 2 tolerances only",
      "B. Class 1, 2 and 3 tolerances",
      "C. Class 3 tolerances only"
    ],
    answer: "C"
  },
  {
    question: "Setting plugs are used to check the:",
    options: [
      "A. settings of adjustable ring and caliper gauges",
      "B. settings of screw plug gauges",
      "C. concentricity of internal threads"
    ],
    answer: "A"
  },
  {
    question: "When an ISO Metric thread is in the 'maximum metal condition' the:",
    options: [
      "A. internal thread crests are rounded and the external thread crests are flat",
      "B. the internal and external thread crests are rounded",
      "C. internal thread crests are flat and the external thread crests are rounded"
    ],
    answer: "C"
  },
  {
    question: "Pitch accuracy is measured:",
    options: [
      "A. at each crest-to-crest position",
      "B. over a specified length of engagement",
      "C. over the whole length of the threaded portion"
    ],
    answer: "B"
  },
  {
    question: "The taper of BSP and American pipe threads is:",
    options: [
      "A. 1:24",
      "B. 1:16",
      "C. 1:12"
    ],
    answer: "B"
  },
  {
    question: "The definition of a 'Class 3' fit Unified thread compares to a:",
    options: [
      "A. 'Close fit' ISO Metric",
      "B. 'Loose fit' ISO Metric",
      "C. 'Medium fit' ISO Metric"
    ],
    answer: "A"
  },
  {
    question: "Fine pitch threaded nuts and bolts are the preferred choice on aircraft because:",
    options: [
      "A. of their speed of assembly",
      "B. they suit aluminium components",
      "C. of their firm grip and resistance to vibration"
    ],
    answer: "C"
  },
  {
    question: "The ISO Metric thread profile is designed so that the:",
    options: [
      "A. flat at the crest is larger than the flat at the root",
      "B. flats at the crest and root are of equal size",
      "C. flat at the root is larger than the flat at the crest"
    ],
    answer: "C"
  },
  {
    question: "The symbol used to identify Unified threads is:",
    options: [
      "A. a triangle",
      "B. a letter X",
      "C. continuous circles"
    ],
    answer: "C"
  },
  {
    question: "A shear bolt may be recognised by a:",
    options: [
      "A. raised disc on the head",
      "B. thin head",
      "C. notches on the head"
    ],
    answer: "B"
  },
  {
    question: "The nominal length of a countersunk screw is the:",
    options: [
      "A. length of the threaded shank",
      "B. overall length",
      "C. length of the plain shank"
    ],
    answer: "B"
  },
  {
    question: "A raised disc on the head of a British Standard bolt indicates that it is a:",
    options: [
      "A. shear bolt",
      "B. high tensile steel cold forged bolt",
      "C. close tolerance bolt"
    ],
    answer: "C"
  },
  {
    question: "A corrosion resistant steel bolt is:",
    options: [
      "A. not plated",
      "B. cadmium plated",
      "C. anodised"
    ],
    answer: "A"
  },
  {
    question: "An ISO Metric thread bolt is classified by:",
    options: [
      "A. diameter and overall length",
      "B. diameter, pitch and tolerance class",
      "C. pitch and length of the plain shank"
    ],
    answer: "B"
  },
  {
    question: "The head markings on an ISO Metric bolt normally consist of:",
    options: [
      "A. letter M and figures indicating the mechanical property class",
      "B. continuous circles and a diameter, pitch code",
      "C. standard number followed by a diameter, length code"
    ],
    answer: "A"
  },
  {
    question: "A 'dog point' on the end of the threaded portion of a non-hexagonal bolt indicates:",
    options: [
      "A. close tolerance",
      "B. aluminium alloy",
      "C. Unified thread"
    ],
    answer: "C"
  },
  {
    question: "A stud that has a larger size thread at the 'metal end' is known as a:",
    options: [
      "A. stepped stud",
      "B. shouldered stud",
      "C. waisted stud"
    ],
    answer: "A"
  },
  {
    question: "'Nylon' insert stiff nuts should not normally be located in regions where the temperature exceeds:",
    options: [
      "A. 500°F (260°C)",
      "B. 270°F (132°C)",
      "C. 212°F (100°C)"
    ],
    answer: "B"
  },
  {
    question: "A high tensile steel BA/BSF cold rolled bolt is identified by a:",
    options: [
      "A. raised disc on the head",
      "B. recess in the head",
      "C. embossed ring on the head"
    ],
    answer: "C"
  },
  {
    question: "Unified aluminium alloy fasteners are dyed:",
    options: [
      "A. green",
      "B. blue",
      "C. black"
    ],
    answer: "A"
  },
  {
    question: "A small all-metal stiff nut may be considered to be unserviceable for use in a non-critical location when it:",
    options: [
      "A. has been used once",
      "B. can be screwed through its friction element on a new bolt by finger pressure",
      "C. can be screwed through its friction element on a worn bolt by finger pressure"
    ],
    answer: "D"
  },
  {
    question: "The minimum amount by which a bolt must protrude through the friction element of a stiff nut is:",
    options: [
      "A. three clear threads including any chamfer",
      "B. one clear thread not including the chamfer",
      "C. the length of the chamfer"
    ],
    answer: "B"
  },
  {
    question: "Notches cut into the corners of a hexagon nut indicate that it is:",
    options: [
      "A. high tensile steel",
      "B. aluminium alloy",
      "C. low tensile steel"
    ],
    answer: "A"
  },
  {
    question: "A letter L or two dashes on the head of a BSF bolt indicates that it is:",
    options: [
      "A. low tensile steel",
      "B. left hand thread",
      "C. aluminium alloy"
    ],
    answer: "C"
  },
  {
    question: "An X within a triangle marked on the head of an early series AN bolt indicates a:",
    options: [
      "A. close tolerance steel bolt",
      "B. corrosion resistant steel bolt",
      "C. aluminium alloy close tolerance bolt"
    ],
    answer: "A"
  },
  {
    question: "A BSF bolt reference A26 24E indicates that the bolt is:",
    options: [
      "A. 1.5 in nominal length and 5/16 nominal diameter",
      "B. 2.4 in nominal length and 1/4 in nominal diameter",
      "C. 3 in nominal diameter and 3/8 nominal diameter"
    ],
    answer: "B"
  },
  {
    question: "An ISO Metric bolt reference M6 × 0.75 indicates that the bolt is:",
    options: [
      "A. 6mm nominal length and 0.75 nominal diameter",
      "B. 0.75mm nominal length and 6mm nominal diameter",
      "C. 6mm nominal diameter and 0.75mm pitch"
    ],
    answer: "C"
  },
  {
    question: "An AN machine screw, reference AN174DD14, is made of:",
    options: [
      "A. aluminium alloy",
      "B. steel",
      "C. corrosion resistant steel"
    ],
    answer: "A"
  },
  {
    question: "Which of the following locking devices can be used more than once?",
    options: [
      "A. Locking plate",
      "B. Split pin",
      "C. Tab washer"
    ],
    answer: "A"
  },
  {
    question: "When wire locking a union, the angle of approach of the wire must not be:",
    options: [
      "A. less than 90° to the rotational axis",
      "B. more than 45° to the lateral axis",
      "C. less than 45° to the rotational axis"
    ],
    answer: "C"
  },
  {
    question: "Unless otherwise specified, a spring washer may be used:",
    options: [
      "A. once only",
      "B. repeatedly providing it retains its springiness and sharp edges",
      "C. a maximum of three times"
    ],
    answer: "B"
  },
  {
    question: "Shake-proof washers may be used:",
    options: [
      "A. twice providing they are reversed",
      "B. once only",
      "C. repeatedly providing they have sharp edges"
    ],
    answer: "B"
  },
  {
    question: "Circlips and locking rings are manufactured from:",
    options: [
      "A. high carbon steel",
      "B. spun cast iron",
      "C. spring steel"
    ],
    answer: "C"
  },
  {
    question: "A Dzus fastener is locked in a:",
    options: [
      "A. quarter turn clockwise",
      "B. half turn clockwise",
      "C. full turn in either direction"
    ],
    answer: "A"
  },
  {
    question: "A locking plate may be used:",
    options: [
      "A. once only",
      "B. until all spare tabs have been used once",
      "C. repeatedly providing it remains a good fit"
    ],
    answer: "C"
  },
  {
    question: "When a spring washer is used on a light alloy component, it is used:",
    options: [
      "A. without a plain washer",
      "B. with a plain washer",
      "C. with a tab washer"
    ],
    answer: "B"
  },
  {
    question: "Dzus fasteners are used on:",
    options: [
      "A. frequently removed panels",
      "B. stressed panels in pressurised areas",
      "C. panels that are infrequently removed"
    ],
    answer: "A"
  },
  {
    question: "A tab washer may be used:",
    options: [
      "A. once only",
      "B. twice providing the tab is not cracked",
      "C. repeatedly providing it remains a good fit"
    ],
    answer: "A"
  },
  {
    question: "An external plate type circlip can be used to:",
    options: [
      "A. retain a ball race inside a housing",
      "B. retain a ball race on a shaft",
      "C. do both the above tasks"
    ],
    answer: "B"
  },
  {
    question: "The maximum recommended length for unsupported double twisted strand wire locking is:",
    options: [
      "A. 24 inches",
      "B. 3 inches",
      "C. 6 inches"
    ],
    answer: "B"
  },
  {
    question: "The recommended number of twists per inch in double twisted strand wire locking is:",
    options: [
      "A. 20 to 24",
      "B. 10 to 14",
      "C. 8 to 10"
    ],
    answer: "C"
  },
  {
    question: "A recommended method of aligning a slot with a split pin hole is to:",
    options: [
      "A. loosen the nut slightly",
      "B. file the bottom of the nut",
      "C. tighten the nut slightly"
    ],
    answer: "C"
  },
  {
    question: "When a pulley wheel is designed to slide axially on a shaft whilst being driven, the key that would be used to permit this is a:",
    options: [
      "A. feather key",
      "B. woodruff key",
      "C. hollow saddle key"
    ],
    answer: "A"
  },
  {
    question: "The allowance for a key in a shaft keyway provides for a:",
    options: [
      "A. sliding fit",
      "B. interference fit",
      "C. loose fit"
    ],
    answer: "B"
  },
  {
    question: "A Camlock fastener may be secured in:",
    options: [
      "A. half a turn",
      "B. quarter of a turn",
      "C. a full turn"
    ],
    answer: "B"
  },
  {
    question: "The type of quick release latch typically used to secure engine cowling doors is a:",
    options: [
      "A. tension hook latch",
      "B. pin latch",
      "C. sealed latch"
    ],
    answer: "A"
  },
  {
    question: "Quick release 'pip pins' are designed to accept:",
    options: [
      "A. tensile loads only",
      "B. tensile and shear loads",
      "C. shear loads only"
    ],
    answer: "C"
  },
  {
    question: "A cotter pin is designed to accept:",
    options: [
      "A. double shear loads",
      "B. double tensile loads",
      "C. single shear loads"
    ],
    answer: "A"
  },
  {
    question: "American 2017 D or 2024 DD solid rivets are:",
    options: [
      "A. not subject to heat treatment",
      "B. heat treated by the operator prior to use",
      "C. heat treated by the manufacturer prior to use"
    ],
    answer: "B"
  },
  {
    question: "A British solid rivet that is anodised and dyed black is made of:",
    options: [
      "A. duralumin",
      "B. hiduminium",
      "C. aluminium"
    ],
    answer: "C"
  },
  {
    question: "A British L86 hiduminium rivet is recognisable by which anodised colour?",
    options: [
      "A. black",
      "B. violet",
      "C. green"
    ],
    answer: "B"
  },
  {
    question: "The Standard number for a British solid rivet indicates the:",
    options: [
      "A. diameter and length",
      "B. diameter and 'grip'",
      "C. head shape, material and finish"
    ],
    answer: "C"
  },
  {
    question: "An embossed letter D on the end of the shank of a British A5 rivet indicates:",
    options: [
      "A. duralumin",
      "B. oversize",
      "C. close tolerance"
    ],
    answer: "A"
  },
  {
    question: "A raised dot on the head of an American rivet indicates the material is:",
    options: [
      "A. 2017 aluminium alloy",
      "B. 1100 aluminium",
      "C. QQ N281 monel"
    ],
    answer: "A"
  },
  {
    question: "American and British SP metric rivet heads are:",
    options: [
      "A. pan head and 120° countersunk only",
      "B. universal head and 100° countersunk only",
      "C. mushroom head and 100° countersunk only"
    ],
    answer: "B"
  },
  {
    question: "An embossed cross on the head of an American rivet indicates the material is:",
    options: [
      "A. 2017 Al/Cu alloy",
      "B. 5056 Al/Mg alloy",
      "C. 7050 Al/Zn alloy"
    ],
    answer: "B"
  },
  {
    question: "Heat treatable aluminium alloy rivets are:",
    options: [
      "A. solution treated",
      "B. precipitation treated",
      "C. hardened"
    ],
    answer: "A"
  },
  {
    question: "After forming, the strength of a heat-treated rivet will:",
    options: [
      "A. decrease over time as a result of age hardening",
      "B. increase over time as a result of age hardening",
      "C. not change"
    ],
    answer: "B"
  },
  {
    question: "The diameter of a standard solid rivet is quoted in:",
    options: [
      "A. 1/64 in",
      "B. 1/16 in",
      "C. 1/32 in"
    ],
    answer: "C"
  },
  {
    question: "If the heat treatment temperature of rivets is exceeded at any time they:",
    options: [
      "A. must be re-treated",
      "B. are not affected",
      "C. must be rejected"
    ],
    answer: "C"
  },
  {
    question: "British AS solid close tolerance rivet lengths are measured in steps of:",
    options: [
      "A. 1/32 in",
      "B. 1/16 in",
      "C. 1/64 in"
    ],
    answer: "A"
  },
  {
    question: "After closing a Cherrylock rivet, the fractured head of the stem:",
    options: [
      "A. is discarded",
      "B. is replaced with a sealing pin",
      "C. remains locked in the rivet bore"
    ],
    answer: "C"
  },
  {
    question: "A Cherrylock rivet is similar to a:",
    options: [
      "A. Huck rivet",
      "B. Chobert rivet",
      "C. Imex rivet"
    ],
    answer: "A"
  },
  {
    question: "A lock bolt type that is placed by shearing off a nut on a retaining collar is a:",
    options: [
      "A. Jo-bolt",
      "B. Huck bolt",
      "C. Hi-lok"
    ],
    answer: "C"
  },
  {
    question: "One rivet type designed for use where access is limited to one side is a:",
    options: [
      "A. Hi-lok",
      "B. Hi-shear",
      "C. Blind"
    ],
    answer: "C"
  },
  {
    question: "Unless otherwise specified, the maximum number of times a rivet can be subjected to heat treatment is:",
    options: [
      "A. three",
      "B. one",
      "C. unlimited"
    ],
    answer: "A"
  },
  {
    question: "Rivets are primarily designed to react:",
    options: [
      "A. tensile stress",
      "B. shear stress",
      "C. compressive stress"
    ],
    answer: "B"
  },
  {
    question: "An American standard solid rivet identification code reads AN470DD 6-14. It is:",
    options: [
      "A. 3/8 in diameter and 7/8 in long",
      "B. 3/16 in diameter and 7/8 in long",
      "C. 3/16 in diameter and 7/16 in long"
    ],
    answer: "B"
  },
  {
    question: "The size of a rigid pipe is expressed as a measurement of the:",
    options: [
      "A. diameter of its bore",
      "B. outside diameter",
      "C. length"
    ],
    answer: "B"
  },
  {
    question: "The inner liner of a flexible hose carrying phosphate ester oil would be made of:",
    options: [
      "A. Natural rubber",
      "B. Neoprene",
      "C. Teflon"
    ],
    answer: "C"
  },
  {
    question: "A union part numbered AN1234-6 would match a:",
    options: [
      "A. 3/8in pipe",
      "B. 3/16in pipe",
      "C. 3/4in pipe"
    ],
    answer: "A"
  },
  {
    question: "The colour and the symbols displayed on a fuel pipe identification decal are:",
    options: [
      "A. Yellow and rectangles",
      "B. Red and chevrons",
      "C. Red and stars"
    ],
    answer: "C"
  },
  {
    question: "Flexible hoses are classified by:",
    options: [
      "A. diameter",
      "B. material",
      "C. maximum operating pressure"
    ],
    answer: "C"
  },
  {
    question: "The test pressure used for pipes and hose assemblies is:",
    options: [
      "A. the maximum design operating pressure",
      "B. one and a half times the maximum design operating pressure",
      "C. twice the minimum design operating pressure"
    ],
    answer: "B"
  },
  {
    question: "Rigid pipes used on gas turbine engines are normally made of:",
    options: [
      "A. stainless steel",
      "B. aluminium",
      "C. tungsten"
    ],
    answer: "A"
  },
  {
    question: "The condition in which non-corrodible steel pipes are supplied is:",
    options: [
      "A. fully hardened",
      "B. annealed",
      "C. tempered"
    ],
    answer: "B"
  },
  {
    question: "Double flaring is carried out on some rigid pipes to:",
    options: [
      "A. increase shear resistance",
      "B. increase wall thickness",
      "C. increase tensile strength"
    ],
    answer: "A"
  },
  {
    question: "An externally coned adaptor mates with a flared pipe connection that has:",
    options: [
      "A. an adaptor nipple",
      "B. no adaptor nipple",
      "C. an externally coned fitting"
    ],
    answer: "B"
  },
  {
    question: "The maximum storage life of rubber and synthetic rubber hose assemblies is:",
    options: [
      "A. three years from date of entering storage",
      "B. five years from date of manufacture",
      "C. two years from cure date"
    ],
    answer: "B"
  },
  {
    question: "The warning symbol carried on rigid pipeline decals is:",
    options: [
      "A. the skull and crossbones",
      "B. HAZARD",
      "C. DANGER"
    ],
    answer: "A"
  },
  {
    question: "Swaged hose connectors are:",
    options: [
      "A. not re-usable",
      "B. re-usable",
      "C. never used"
    ],
    answer: "A"
  },
  {
    question: "The American rigid pipe flare angle is:",
    options: [
      "A. 32°",
      "B. 45°",
      "C. 74°"
    ],
    answer: "C"
  },
  {
    question: "A universal union:",
    options: [
      "A. fits all sizes of pipe connector",
      "B. fits American and British pipe connectors",
      "C. allows for variations in the angle of connection"
    ],
    answer: "C"
  },
  {
    question: "If a flare-less pipe connector is leaking it may:",
    options: [
      "A. be tightened by a further two flats",
      "B. not be tightened any further",
      "C. be tightened until the leak stops"
    ],
    answer: "B"
  },
  {
    question: "When a flare-less pipe connector is torqued in service, it is tightened until a distinct increase in torque is felt and is then:",
    options: [
      "A. tightened a further one to two flats",
      "B. tightened a full turn",
      "C. not tightened further"
    ],
    answer: "A"
  },
  {
    question: "Rigid high-pressure pipes attached to a landing gear leg would be made from:",
    options: [
      "A. aluminium alloy",
      "B. tungsten",
      "C. non-corrodible steel"
    ],
    answer: "C"
  },
  {
    question: "The purpose of the stripe running the length of some hose assemblies is to:",
    options: [
      "A. indicate pipe twist",
      "B. identify the pipe material",
      "C. indicate the maximum working pressure"
    ],
    answer: "A"
  },
  {
    question: "Flare-less connectors are designed to:",
    options: [
      "A. reduce installation",
      "B. reduce fatigue in connectors",
      "C. reduce fatigue rigid pipe connectors"
    ],
    answer: "C"
  },
  { question: "If the length of a spring is doubled, its extension for a given load will:", options: ["A. half","B. remain unchanged","C. double"], answer: "C" },
  { question: "The 'rate' of a spring may be calculated by dividing the:", options: ["A. deflection by the load","B. load by the deflection","C. coil diameter by the wire diameter"], answer: "B" },
  { question: "The number of active coils in a spring is:", options: ["A. proportional to the spring 'rate'","B. inversely proportional to the spring 'rate'","C. inversely proportional to the spring 'index'"], answer: "B" },
  { question: "When a spring weakens in use its spring 'rate' will:", options: ["A. not alter","B. increase","C. decrease"], answer: "C" },
  { question: "Hooke's Law states that the force on a spring is:", options: ["A. directly proportional to its deflection throughout the elastic range only","B. indirectly proportional to its deflection throughout the elastic range only","C. directly proportional to its deflection at all times"], answer: "A" },
  { question: "The 'Free Length' of a compression spring refers to:", options: ["A. the overall length when the spring is unloaded","B. the overall length when the spring is fully compressed","C. the difference between the loaded and unloaded lengths"], answer: "A" },
  { question: "When a helical, conical wire spring is compressed, the coil that 'bottoms' first is:", options: ["A. the smallest diameter coil","B. the largest diameter coil","C. the middle active coil"], answer: "B" },
  { question: "A helical wire spring that has a pitch that reduces along its length is called a:", options: ["A. constant rate spring","B. progressive rate spring","C. high rate spring"], answer: "B" },
  { question: "When a constant rate helical spring is compressed, the distance between each active coil reduces:", options: ["A. more in the centre than at the ends","B. more at the ends than in the centre","C. equally"], answer: "C" },
  { question: "A suitable material for use in springs would be:", options: ["A. High carbon steel or alloy steel with a high proof stress","B. Low carbon steel or alloy steel with a low Modulus of Rigidity","C. Medium carbon steel or alloy steel with a low proof stress"], answer: "A" },
  { question: "Valve springs used in reciprocating engines are classed as:", options: ["A. General duty","B. Static duty","C. High duty"], answer: "C" },
  { question: "A spring that is manufactured with pre-tensioned closed coils is a:", options: ["A. extension spring","B. compression spring","C. spiral torsion spring"], answer: "A" },
  { question: "A soft spring that produces large deflections for low loads is classed as a:", options: ["A. high rate spring","B. low rate spring","C. progressive rate spring"], answer: "B" },
  { question: "When the volume of gas in a gas spring is halved, the gas pressure is:", options: ["A. halved","B. quadrupled","C. doubled"], answer: "C" },
  { question: "A garter spring releases its energy as a:", options: ["A. radial force","B. axial force","C. rotational force"], answer: "A" },
  { question: "The spring material specification code M (Music wire) applies to:", options: ["A. normal duty, static load springs","B. high duty, static and dynamic load springs","C. normal duty, dynamic load springs"], answer: "B" },
  { question: "The deflection of a spiral torsion spring is displayed as a:", options: ["A. change in coil diameter","B. change in strip thickness","C. change in strip length"], answer: "A" },
  { question: "When a 'damped' gas spring is used as a shock absorber it will:", options: ["A. absorb energy quickly and release it slowly","B. absorb energy slowly and release it quickly","C. absorb and release energy slowly"], answer: "A" },
  { question: "A spring used in a priority valve is normally a:", options: ["A. extension spring","B. torsion spring","C. compression spring"], answer: "C" },
  { question: "Carbon steel used in springs is normally:", options: ["A. low medium to low carbon steel","B. low carbon steel","C. high medium to high carbon steel"], answer: "C" },
  {
    question: "Needle rollers are capable of reacting:",
    options: [
      "A. Axial loads only",
      "B. Radial loads only",
      "C. Axial and radial loads"
    ],
    answer: "B"
  },
  {
    question: "Spherical roller bearings are capable of reacting:",
    options: [
      "A. radial loads only",
      "B. heavy radial and heavy axial loads",
      "C. heavy radial and moderate axial loads"
    ],
    answer: "C"
  },
  {
    question: "A universal coupling would normally have:",
    options: [
      "A. ball bearings",
      "B. tapered roller bearings",
      "C. needle roller bearings"
    ],
    answer: "C"
  },
  {
    question: "Where the possibility of temperature reducing radial internal clearance may exist, the choice of bearing used is:",
    options: [
      "A. Group 4",
      "B. Group 2",
      "C. Normal Group"
    ],
    answer: "A"
  },
  {
    question: "The type of rolling bearing that would be used to locate a shaft is a:",
    options: [
      "A. cylindrical roller bearing",
      "B. radial ball bearing",
      "C. spherical roller bearing"
    ],
    answer: "B"
  },
  {
    question: "Thrust bearings are designed to react:",
    options: [
      "A. axial loads",
      "B. radial loads",
      "C. axial and radial loads"
    ],
    answer: "A"
  },
  {
    question: "A single row tapered roller bearing will react:",
    options: [
      "A. radial and axial loads in both directions",
      "B. radial load in one direction and axial load in both directions",
      "C. axial load in one direction and radial load in both directions"
    ],
    answer: "C"
  },
  {
    question: "A single row angular contact bearing will react:",
    options: [
      "A. axial loads in one direction only",
      "B. axial loads in both directions",
      "C. radial loads only"
    ],
    answer: "A"
  },
  {
    question: "A bearing load that acts at right angles to the axis of a shaft is described as being:",
    options: [
      "A. axial",
      "B. radial",
      "C. normal"
    ],
    answer: "B"
  },
  {
    question: "The most suitable bearing metal for lining heavily loaded plain bearings is:",
    options: [
      "A. lead based white metal",
      "B. tin based white metal",
      "C. sintered bronze"
    ],
    answer: "B"
  },
  {
    question: "Ball bearings are normally made from:",
    options: [
      "A. tungsten/chromium alloy steel",
      "B. high carbon steel",
      "C. phosphor bronze"
    ],
    answer: "A"
  },
  {
    question: "The radial internal clearance in a ball bearing refers to the clearance between the:",
    options: [
      "A. outer ring and the housing",
      "B. balls and the raceways",
      "C. inner ring and the shaft"
    ],
    answer: "B"
  },
  {
    question: "Standard bearings that have the smallest radial internal clearance are designated:",
    options: [
      "A. Group 5",
      "B. Group 1",
      "C. Group 2"
    ],
    answer: "C"
  },
  {
    question: "The type of roller bearing that can absorb small errors in shaft alignment is a:",
    options: [
      "A. tapered bearing",
      "B. radial bearing",
      "C. spherical bearing"
    ],
    answer: "C"
  },
  {
    question: "Porous metal bearings are designed to:",
    options: [
      "A. carry a lubricant",
      "B. run dry",
      "C. create a cooling air flow"
    ],
    answer: "A"
  },
  {
    question: "Rolling bearing assemblies may be fitted with metal shields to:",
    options: [
      "A. act as debris guards",
      "B. retain the rolling elements",
      "C. provide protection from heat"
    ],
    answer: "A"
  },
  {
    question: "Cylindrical roller bearings may be used for shaft:",
    options: [
      "A. location",
      "B. support",
      "C. run-out"
    ],
    answer: "B"
  },
  {
    question: "Radial ball bearings may be used for shaft:",
    options: [
      "A. run-out",
      "B. support",
      "C. location"
    ],
    answer: "C"
  },
  {
    question: "Duplex bearings are able to react:",
    options: [
      "A. axial load in one direction only",
      "B. axial load in both directions",
      "C. radial loads only"
    ],
    answer: "B"
  },
  {
    question: "The radial internal clearance group designations apply to:",
    options: [
      "A. radial ball and cylindrical roller bearings only",
      "B. all types of rolling bearing",
      "C. angular contact bearings only"
    ],
    answer: "A"
  },
  {
    question: "The input and output shafts in an epicyclic gear rotate around:",
    options: [
      "A. parallel axes that are offset, one below the other",
      "B. the same axis",
      "C. axes that are at right angles to each other"
    ],
    answer: "B"
  },
  {
    question: "Gears can only operate properly if they have:",
    options: [
      "A. correct backlash and pattern",
      "B. correct pattern and no backlash",
      "C. axial thrust and end-float"
    ],
    answer: "A"
  },
  {
    question: "The type of reduction gearing used on turbo-propeller engines is:",
    options: [
      "A. bevel epicyclic",
      "B. compound spur train",
      "C. compound epicyclic"
    ],
    answer: "C"
  },
  {
    question: "When involute gear teeth mesh the pressure face contact is:",
    options: [
      "A. total area",
      "B. line contact in the middle",
      "C. point contact at the tip"
    ],
    answer: "B"
  },
  {
    question: "Double helical gears produce:",
    options: [
      "A. no axial thrust",
      "B. axial thrust",
      "C. radial thrust"
    ],
    answer: "A"
  },
  {
    question: "An idle gear placed between two gears will:",
    options: [
      "A. affect the gear ratio",
      "B. change the direction of rotation of the driven wheel",
      "C. do neither of the above"
    ],
    answer: "B"
  },
  {
    question: "When calculating the overall gear ratio of a compound gear train the ratios of the individual driver and driven gear pairs must be:",
    options: [
      "A. added",
      "B. subtracted",
      "C. multiplied"
    ],
    answer: "C"
  },
  {
    question: "The gear ratio of a pair of spur gears is derived by:",
    options: [
      "A. dividing the no. of driver gear teeth by the no. of driven gear teeth",
      "B. dividing the no. of driven gear teeth by the no. of driver gear teeth",
      "C. multiplying the no. of driver gear teeth by the no. of driven gear teeth"
    ],
    answer: "A"
  },
  {
    question: "A Vee-belt exerts a driving force on a pulley rim groove at the:",
    options: [
      "A. base",
      "B. sides",
      "C. top"
    ],
    answer: "B"
  },
  {
    question: "A crossed belt drive will:",
    options: [
      "A. reverse the direction of rotation of the follower",
      "B. reduce the gear ratio",
      "C. reverse the direction of rotation of the driver"
    ],
    answer: "A"
  },
  {
    question: "If the overall speed ratio of a system of belt driven pulleys is 0.25, an input speed of 1000 RPM will produce an output speed of:",
    options: [
      "A. 4000 RPM",
      "B. 250 RPM",
      "C. 2500 RPM"
    ],
    answer: "B"
  },
  {
    question: "When belt slip cannot be tolerated, the belt of choice would be a:",
    options: [
      "A. vee-belt",
      "B. poly-vee belt",
      "C. serrated tooth belt"
    ],
    answer: "C"
  },
  {
    question: "If a compound epicyclic reduction gear has a gear ratio of 0.1, the no. of revolutions of the input shaft required to produce one output shaft revolution is:",
    options: [
      "A. 10",
      "B. 100",
      "C. 1"
    ],
    answer: "A"
  },
  {
    question: "The planet gears in a bevel epicyclic reduction gear will:",
    options: [
      "A. reduce the gear ratio",
      "B. increase the gear ratio",
      "C. have no effect on the gear ratio"
    ],
    answer: "C"
  },
  {
    question: "Aircraft control chain is classified by:",
    options: [
      "A. length, pitch and width between outer plates",
      "B. breaking strength, pitch and length",
      "C. roller diameter, pitch and width between inner plates"
    ],
    answer: "C"
  },
  {
    question: "A bi-planar block is used to alter the:",
    options: [
      "A. linear direction of a control chain by 90°",
      "B. plane of a control chain by 90°",
      "C. plane of a control chain by 180°"
    ],
    answer: "B"
  },
  {
    question: "Sections of aircraft control chain are joined by a:",
    options: [
      "A. spring clip",
      "B. cranked link",
      "C. bolted attachment"
    ],
    answer: "C"
  },
  {
    question: "A non-reversible chain is a chain that is designed to:",
    options: [
      "A. be fitted in the correct orientation only",
      "B. move in one direction only",
      "C. resist back driving in a control system"
    ],
    answer: "A"
  },
  {
    question: "When gear teeth on gears do not mesh with the same teeth during successive revolutions the gear ratio is described as being a:",
    options: [
      "A. epicyclic ratio",
      "B. cycloid ratio",
      "C. hunting tooth ratio"
    ],
    answer: "C"
  },
  {
    question: "Cycloid profile gear teeth mesh in:",
    options: [
      "A. line contact",
      "B. point contact",
      "C. area contact"
    ],
    answer: "C"
  },
  
  { question: "British aircraft control system cables are classified by their:", options: ["A. proof load in lbf","B. minimum breaking strength in cwtf","C. construction and material"], answer: "B" },
  { question: "The main advantage offered by aircraft control system cable is that it:", options: ["A. can transmit force in compression and tension","B. transmits force in one direction only","C. is strong and light"], answer: "C" },
  { question: "An aircraft control system cable with a 7 × 19 construction has:", options: ["A. seven strands, each containing nineteen wires","B. nineteen strands, each containing seven wires","C. one core strand and seven outer strands, each containing nineteen wires"], answer: "A" },
  { question: "A fairlead is a device that is used to:", options: ["A. change the direction of a control system cable run","B. damp vibration in a control system cable and prevent chafing","C. maintain cable tension"], answer: "B" },
  { question: "A tension rod turnbuckle is checked for safety using a:", options: ["A. hardened steel pin having the same diameter as the inspection holes","B. length of 22SWG locking wire","C. tensiometer"], answer: "A" },
  { question: "A barrel type turnbuckle is considered to be in safety when a:", options: ["A. minimum of three threads are exposed at each end","B. maximum of three threads are exposed at each end","C. threads are showing in the inspection holes"], answer: "B" },
  { question: "A cable tension regulator is primarily used in a cable-operated system to:", options: ["A. check the tension","B. maintain a constant pull force","C. maintain constant tension"], answer: "C" },
  { question: "The tension in an un-regulated aircraft cable-operated system will:", options: ["A. decrease as ambient temperature decreases","B. increase as ambient temperature decreases","C. not alter with changes in ambient temperature"], answer: "A" },
  { question: "The nominal diameter of aircraft control system cable is a measure of its:", options: ["A. core strand diameter","B. wire diameter","C. maximum overall diameter"], answer: "C" },
  { question: "Turnbuckles are primarily used to:", options: ["A. join lengths of cable together","B. make minor adjustments to cable tension","C. make major adjustments to cable length"], answer: "B" },
  { question: "A Bowden cable assembly exerts:", options: ["A. push and pull","B. push only","C. pull only"], answer: "C" },
  { question: "Bowden cable nipples are secured by:", options: ["A. soldering","B. welding","C. brazing"], answer: "A" },
  { question: "Bowden cable systems are usually designed to operate:", options: ["A. a heavily loaded component in a one-way direction","B. a lightly loaded component in a one-way direction","C. any component in a two-way direction"], answer: "B" },
  { question: "A Teleflex flexible control system is designed so that it can be selected to:", options: ["A. any position in one direction of travel only","B. one fixed stop position only in each direction of travel","C. any position in both directions of travel"], answer: "C" },
  { question: "The minimum cable wrap in a single entry Teleflex control unit is:", options: ["A. 40°","B. 270°","C. 90°"], answer: "A" },
  { question: "Aluminium Teleflex conduit lined with PTFE is:", options: ["A. designed for use in the hot zones of aircraft engines","B. not to be used in hot zones","C. designed for use where relative movement exists between connection points"], answer: "B" },
  { question: "A Teleflex cable is connected into a push pull control unit by a:", options: ["A. soldered nipple","B. lock spring connector","C. sliding end fitting"], answer: "B" },
  { question: "Aircraft flying control system cable is usually manufactured from:", options: ["A. straight, galvanised steel wire strands","B. non pre-formed, single corrosion resistant steel wire strands","C. pre-formed, multiple corrosion resistant steel wire strands"], answer: "C" },
  { question: "Cable tension on a flying control wire system that incorporates a cable tension regulator is measured by using a:", options: ["A. scale reading on the tension regulator and a setting graph","B. cable tensiometer and a setting graph","C. cable tensiometer and a scale reading on the tension regulator"], answer: "A" },
  { question: "Aircraft control tubes are manufactured from:", options: ["A. aluminium alloy tubing","B. steel tubing","C. aluminium tubing"], answer: "A" },

]




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
