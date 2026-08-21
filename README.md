<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>대한민국 국방기밀 제1호 - K-80 비호(飛虎) 인터랙티브 청사진</title>
  <style>
    :root {
      --bg-color: #040a14;
      --panel-bg: rgba(8, 26, 48, 0.95);
      --card-bg: #07172b;
      --card-alt: #0a203c;
      --cyan: #00f3ff;
      --cyan-dim: rgba(0, 243, 255, 0.25);
      --amber: #ffd166;
      --green: #00ffaa;
      --text-bright: #f0f7ff;
      --text-muted: #9dc0e2;
      --font-mono: "SF Mono", "Consolas", "Courier New", monospace;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      background-color: var(--bg-color);
      color: var(--text-bright);
      font-family: var(--font-mono);
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      background-image: 
        linear-gradient(var(--cyan-dim) 1px, transparent 1px),
        linear-gradient(90deg, var(--cyan-dim) 1px, transparent 1px);
      background-size: 35px 35px;
      overflow-x: hidden;
    }

    /* 상단 헤더 */
    header {
      background: var(--panel-bg);
      border-bottom: 2px solid var(--cyan);
      padding: 1rem 1.5rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: 0 4px 20px rgba(0, 243, 255, 0.15);
    }
    .title-box h1 {
      font-size: 1.25rem;
      color: var(--cyan);
      letter-spacing: 2px;
      display: flex;
      align-items: center;
      gap: 10px;
    }
    .badge {
      background: #e63946;
      color: #fff;
      font-size: 0.7rem;
      padding: 2px 8px;
      border-radius: 3px;
      font-weight: bold;
    }
    .status-text {
      font-size: 0.8rem;
      color: var(--green);
      text-align: right;
    }

    /* 레이아웃 메인 */
    main {
      display: grid;
      grid-template-columns: 1fr 340px;
      gap: 1.5rem;
      padding: 1.5rem;
      flex: 1;
    }

    @media (max-width: 960px) {
      main { grid-template-columns: 1fr; }
    }

    /* 청사진 뷰어 패널 */
    .viewport-panel {
      background: var(--panel-bg);
      border: 1px solid var(--cyan);
      border-radius: 4px;
      padding: 1.2rem;
      display: flex;
      flex-direction: column;
      position: relative;
      box-shadow: inset 0 0 30px rgba(0, 243, 255, 0.05);
    }

    .controls-bar {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      gap: 10px;
      margin-bottom: 1rem;
      border-bottom: 1px dashed var(--cyan-dim);
      padding-bottom: 0.8rem;
    }

    .btn-group {
      display: flex;
      gap: 6px;
    }
    button {
      background: rgba(0, 243, 255, 0.08);
      border: 1px solid var(--cyan);
      color: var(--cyan);
      padding: 6px 12px;
      font-family: inherit;
      font-size: 0.8rem;
      cursor: pointer;
      border-radius: 2px;
      transition: all 0.2s;
    }
    button:hover, button.active {
      background: var(--cyan);
      color: #040a14;
      box-shadow: 0 0 10px var(--cyan);
      font-weight: bold;
    }

    /* SVG 캔버스 */
    .svg-container {
      flex: 1;
      width: 100%;
      min-height: 440px;
      display: flex;
      justify-content: center;
      align-items: center;
      position: relative;
    }
    svg {
      width: 100%;
      max-height: 520px;
    }

    /* 핫스팟 인터랙션 */
    .hotspot {
      cursor: pointer;
      transition: all 0.3s;
    }
    .hotspot-pulse {
      animation: pulse 1.8s infinite;
      transform-origin: center;
    }
    @keyframes pulse {
      0% { r: 6px; opacity: 1; }
      50% { r: 14px; opacity: 0.3; }
      100% { r: 20px; opacity: 0; }
    }
    .hotspot:hover .hotspot-core {
      fill: var(--amber);
      filter: drop-shadow(0 0 8px var(--amber));
    }

    /* 우측 사이드바 데이터 패널 */
    .sidebar {
      display: flex;
      flex-direction: column;
      gap: 1.2rem;
    }
    .card {
      background: var(--card-bg);
      border: 1px solid var(--cyan-dim);
      border-top: 3px solid var(--cyan);
      border-radius: 4px;
      padding: 1.2rem;
      box-shadow: 0 6px 16px rgba(0, 0, 0, 0.4);
    }
    .card h2 {
      font-size: 0.95rem;
      color: var(--cyan);
      border-bottom: 1px solid var(--cyan-dim);
      padding-bottom: 8px;
      margin-bottom: 12px;
      letter-spacing: 1px;
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .card h2::before {
      content: "■";
      font-size: 0.7rem;
      color: var(--amber);
    }

    /* 가독성이 강화된 기술 제원 테이블 */
    .spec-table {
      width: 100%;
      font-size: 0.85rem;
      border-collapse: separate;
      border-spacing: 0 4px;
    }
    .spec-table tr {
      background: var(--card-alt);
      transition: background 0.2s;
    }
    .spec-table tr:hover {
      background: #0e2d54;
    }
    .spec-table td {
      padding: 8px 10px;
    }
    .spec-table td:first-child {
      color: var(--text-muted);
      font-weight: 500;
      border-left: 2px solid var(--cyan-dim);
      border-radius: 2px 0 0 2px;
    }
    .spec-table td:last-child {
      text-align: right;
      color: var(--amber);
      font-weight: 700;
      letter-spacing: 0.5px;
      border-radius: 0 2px 2px 0;
    }

    /* 부품 상세 설명창 */
    .provenance-box {
      font-size: 0.85rem;
      line-height: 1.6;
      color: var(--text-bright);
      background: var(--card-alt);
      padding: 10px;
      border-radius: 3px;
      border-left: 3px solid var(--green);
    }
    .provenance-tag {
      display: inline-block;
      background: rgba(0, 255, 170, 0.15);
      color: var(--green);
      padding: 3px 8px;
      border-radius: 3px;
      font-size: 0.75rem;
      font-weight: bold;
      margin-bottom: 8px;
      border: 1px solid rgba(0, 255, 170, 0.3);
    }
  </style>
</head>
<body>

  <header>
    <div class="title-box">
      <h1>K-80 '비호(飛虎)' 제트기 청사진 <span class="badge">극비 1급</span></h1>
    </div>
    <div class="status-text">
      <div>국방부 과학기술국 // 프로젝트 BI-HO</div>
      <div>단기 4283년(1950) 3차 개정</div>
    </div>
  </header>

  <main>
    <section class="viewport-panel">
      <div class="controls-bar">
        <div class="btn-group">
          <button id="btn-view-top" class="active" onclick="switchView('top')">상면도 (Top View)</button>
          <button id="btn-view-side" onclick="switchView('side')">측면도 (Side Profile)</button>
        </div>
        <div class="btn-group">
          <button id="loadout-clean" class="active" onclick="setLoadout('clean')">장거리 순항 (Clean)</button>
          <button id="loadout-strike" onclick="setLoadout('strike')">지상 타격 (Strike: HVAR/Bombs)</button>
        </div>
      </div>

      <div class="svg-container">
        <svg id="blueprint-canvas" viewBox="0 0 800 500">
          <defs>
            <pattern id="grid" width="20" height="20" patternUnits="userSpaceOnUse">
              <path d="M 20 0 L 0 0 0 20" fill="none" stroke="rgba(0,243,255,0.08)" stroke-width="0.8"/>
            </pattern>
          </defs>
          <rect width="100%" height="100%" fill="url(#grid)" />

          <!-- ================= 1. 상면도 (TOP VIEW) ================= -->
          <g id="top-view">
            <!-- 주익 및 층류익 형상 -->
            <polygon points="400,160 690,260 680,310 400,290 120,310 110,260" fill="rgba(0, 243, 255, 0.05)" stroke="#00f3ff" stroke-width="2"/>
            
            <!-- 익단 보조연료탱크 -->
            <ellipse cx="110" cy="285" rx="14" ry="48" fill="rgba(0,243,255,0.15)" stroke="#00f3ff" stroke-width="1.8"/>
            <ellipse cx="690" cy="285" rx="14" ry="48" fill="rgba(0,243,255,0.15)" stroke="#00f3ff" stroke-width="1.8"/>

            <!-- 수평 꼬리날개 -->
            <polygon points="400,410 520,450 510,475 400,465 290,475 280,450" fill="rgba(0, 243, 255, 0.05)" stroke="#00f3ff" stroke-width="1.8"/>

            <!-- 중앙 동체 유선형 -->
            <path d="M 400,50 C 430,90 435,220 425,380 L 415,470 L 385,470 L 375,380 C 365,220 370,90 400,50 Z" 
                  fill="rgba(7, 23, 43, 0.95)" stroke="#00f3ff" stroke-width="2.2"/>

            <!-- 조종석 버블 캐노피 -->
            <ellipse cx="400" cy="155" rx="18" ry="42" fill="rgba(0, 255, 170, 0.15)" stroke="#00ffaa" stroke-width="1.5"/>

            <!-- 기수 12.7mm 기관포 6문 포구 라인 -->
            <line x1="392" y1="58" x2="392" y2="78" stroke="#ffb703" stroke-width="2"/>
            <line x1="408" y1="58" x2="408" y2="78" stroke="#ffb703" stroke-width="2"/>
            <line x1="387" y1="65" x2="387" y2="85" stroke="#ffb703" stroke-width="2"/>
            <line x1="413" y1="65" x2="413" y2="85" stroke="#ffb703" stroke-width="2"/>
            <line x1="382" y1="72" x2="382" y2="92" stroke="#ffb703" stroke-width="2"/>
            <line x1="418" y1="72" x2="418" y2="92" stroke="#ffb703" stroke-width="2"/>

            <!-- 상면도 지상 타격 무장 레이어 -->
            <g id="top-weapons" style="display: none;">
              <rect x="300" y="270" width="16" height="42" rx="6" fill="#e63946" stroke="#ffb703" stroke-width="1.5"/>
              <rect x="484" y="270" width="16" height="42" rx="6" fill="#e63946" stroke="#ffb703" stroke-width="1.5"/>
              <line x1="220" y1="280" x2="220" y2="310" stroke="#ffb703" stroke-width="3"/>
              <line x1="240" y1="280" x2="240" y2="310" stroke="#ffb703" stroke-width="3"/>
              <line x1="560" y1="280" x2="560" y2="310" stroke="#ffb703" stroke-width="3"/>
              <line x1="580" y1="280" x2="580" y2="310" stroke="#ffb703" stroke-width="3"/>
            </g>

            <!-- [상면도 전용 핫스팟] -->
            <g id="top-hotspots">
              <g class="hotspot" onclick="showDetail('nose')">
                <circle class="hotspot-pulse" cx="400" cy="70" r="10" fill="none" stroke="#ffb703" stroke-width="2"/>
                <circle class="hotspot-core" cx="400" cy="70" r="6" fill="#00f3ff"/>
              </g>
              <g class="hotspot" onclick="showDetail('cockpit')">
                <circle class="hotspot-pulse" cx="400" cy="155" r="10" fill="none" stroke="#00ffaa" stroke-width="2"/>
                <circle class="hotspot-core" cx="400" cy="155" r="6" fill="#00ffaa"/>
              </g>
              <g class="hotspot" onclick="showDetail('engine')">
                <circle class="hotspot-pulse" cx="400" cy="310" r="12" fill="none" stroke="#ffb703" stroke-width="2"/>
                <circle class="hotspot-core" cx="400" cy="310" r="7" fill="#ffb703"/>
              </g>
              <g class="hotspot" onclick="showDetail('wing')">
                <circle class="hotspot-pulse" cx="560" cy="270" r="10" fill="none" stroke="#00f3ff" stroke-width="2"/>
                <circle class="hotspot-core" cx="560" cy="270" r="6" fill="#00f3ff"/>
              </g>
              <g class="hotspot" onclick="showDetail('tiptank')">
                <circle class="hotspot-pulse" cx="690" cy="285" r="10" fill="none" stroke="#00f3ff" stroke-width="2"/>
                <circle class="hotspot-core" cx="690" cy="285" r="6" fill="#00f3ff"/>
              </g>
            </g>
          </g>

          <!-- ================= 2. 측면도 (SIDE VIEW) ================= -->
          <g id="side-view" style="display: none;">
            <!-- 동체 측면 실루엣 -->
            <path d="M 120,250 C 160,230 260,210 500,210 C 650,210 700,235 720,250 C 700,265 650,285 500,285 C 260,285 160,270 120,250 Z" 
                  fill="rgba(7, 23, 43, 0.95)" stroke="#00f3ff" stroke-width="2.2"/>
            
            <!-- 수직 미익 (꼬리날개) -->
            <polygon points="610,210 680,105 715,105 695,210" fill="rgba(0, 243, 255, 0.08)" stroke="#00f3ff" stroke-width="2"/>
            
            <!-- 캐노피 측면 곡선 -->
            <path d="M 230,225 Q 300,165 370,225 Z" fill="rgba(0, 255, 170, 0.2)" stroke="#00ffaa" stroke-width="1.5"/>
            
            <!-- 타원형 공기 흡입구 -->
            <path d="M 330,240 L 370,240 L 360,265 L 320,265 Z" fill="#040a14" stroke="#00f3ff" stroke-width="1.5"/>

            <!-- 측면도 지상 타격 무장 레이어 -->
            <g id="side-weapons" style="display: none;">
              <rect x="380" y="285" width="42" height="14" rx="4" fill="#e63946" stroke="#ffb703" stroke-width="1.5"/>
              <line x1="360" y1="285" x2="360" y2="295" stroke="#ffb703" stroke-width="2.5"/>
            </g>

            <!-- [측면도 전용 핫스팟] -->
            <g id="side-hotspots">
              <g class="hotspot" onclick="showDetail('nose')">
                <circle class="hotspot-pulse" cx="160" cy="245" r="10" fill="none" stroke="#ffb703" stroke-width="2"/>
                <circle class="hotspot-core" cx="160" cy="245" r="6" fill="#00f3ff"/>
              </g>
              <g class="hotspot" onclick="showDetail('cockpit')">
                <circle class="hotspot-pulse" cx="300" cy="195" r="10" fill="none" stroke="#00ffaa" stroke-width="2"/>
                <circle class="hotspot-core" cx="300" cy="195" r="6" fill="#00ffaa"/>
              </g>
              <g class="hotspot" onclick="showDetail('intake')">
                <circle class="hotspot-pulse" cx="345" cy="252" r="10" fill="none" stroke="#00f3ff" stroke-width="2"/>
                <circle class="hotspot-core" cx="345" cy="252" r="6" fill="#00f3ff"/>
              </g>
              <g class="hotspot" onclick="showDetail('engine')">
                <circle class="hotspot-pulse" cx="490" cy="248" r="12" fill="none" stroke="#ffb703" stroke-width="2"/>
                <circle class="hotspot-core" cx="490" cy="248" r="7" fill="#ffb703"/>
              </g>
              <g class="hotspot" onclick="showDetail('tail')">
                <circle class="hotspot-pulse" cx="660" cy="150" r="10" fill="none" stroke="#00f3ff" stroke-width="2"/>
                <circle class="hotspot-core" cx="660" cy="150" r="6" fill="#00f3ff"/>
              </g>
            </g>
          </g>
        </svg>
      </div>
    </section>

    <!-- 사이드바 정보 창 -->
    <aside class="sidebar">
      <div class="card">
        <h2>부품 상세 정보 (검사기)</h2>
        <div id="provenance-display" class="provenance-box">
          <span class="provenance-tag">검사 대기 중</span>
          <p>좌측 도면의 반짝이는 <strong>핫스팟 마커</strong>를 클릭하여 각 산학 부품의 상세 국산화 명세와 기여 대학을 확인하십시오.</p>
        </div>
      </div>

      <div class="card">
        <h2>기체 기술 제원 (Specs)</h2>
        <table class="spec-table">
          <tr><td>전장 (Length)</td><td>10.49 m</td></tr>
          <tr><td>익폭 (Wingspan)</td><td>11.81 m</td></tr>
          <tr><td>최고 속도 (Max Speed)</td><td>940 km/h (M 0.76)</td></tr>
          <tr><td>엔진 추력 (Thrust)</td><td>4,800 lbf (K-J33)</td></tr>
          <tr><td>기본 무장</td><td>12.7mm M3 x 6문</td></tr>
          <tr><td>작전 반경</td><td>1,300 km (순항 시)</td></tr>
        </table>
      </div>
    </aside>
  </main>

  <script>
    const details = {
      nose: {
        tag: "인천 조병창 // 기수 무장실",
        text: "<strong>12.7mm M3 브라우닝 중기관총 6문</strong> 집약 배치. 분당 총 7,200발의 막강한 밀집 화력을 투사하며 신속 탄약 재장전용 상부 힌지 도어가 장착되어 있습니다."
      },
      cockpit: {
        tag: "서울대학교 // 조종 및 여압 계통",
        text: "고공 비행용 여압 칵핏 및 <strong>버블 캐노피</strong> 적용으로 360도 전방위 시야를 확보. K-14 광학 조준경의 국내 조립 세팅이 완비되었습니다."
      },
      intake: {
        tag: "서울대학교 // 타원형 공기 흡입구",
        text: "동체 측면에 배치된 <strong>낮은 공기저항 흡입 덕트</strong>. 원심식 압축기에 최적화된 공기 유입량을 공급하며 이물질 유입 방지망이 장착되어 있습니다."
      },
      engine: {
        tag: "평양공과대학 // K-J33 제트엔진",
        text: "북부의 <strong>텅스텐·니켈 초내열 합금</strong>을 적용한 국산화 원심식 터보제트 엔진. 800°C 고온 터빈 블레이드 정밀 주조 성공으로 추력 4,800 lbf를 발휘합니다."
      },
      wing: {
        tag: "서울대학교 // NACA 층류익 설계",
        text: "풍동 실험 데이터를 기반으로 고속 비행 시 기체 항력을 22% 감소시킨 <strong>NACA 65-413 층류익</strong>을 주익에 구현했습니다."
      },
      tiptank: {
        tag: "인하공과학원 // 익단 탱크 및 정밀 지그",
        text: "대형 프레스 성형을 통한 <strong>165갤런(625L) 드롭식 연료탱크</strong>. 인천 전용 조립 지그를 통해 서해 횡단 작전 반경을 대폭 확보했습니다."
      },
      tail: {
        tag: "인하공과학원 // 전두루랄루민 수직 미익",
        text: "고속 비행 시 방향 안정성을 보장하는 <strong>올-두랄루민 수직 안정판</strong> 및 기계식 러더 계통입니다."
      }
    };

    let currentLoadout = 'clean';

    function showDetail(key) {
      const data = details[key];
      if (!data) return;
      const box = document.getElementById("provenance-display");
      box.innerHTML = `<span class="provenance-tag">${data.tag}</span><p>${data.text}</p>`;
    }

    function switchView(view) {
      document.getElementById('btn-view-top').classList.toggle('active', view === 'top');
      document.getElementById('btn-view-side').classList.toggle('active', view === 'side');

      document.getElementById('top-view').style.display = view === 'top' ? 'inline' : 'none';
      document.getElementById('side-view').style.display = view === 'side' ? 'inline' : 'none';

      setLoadout(currentLoadout);
    }

    function setLoadout(type) {
      currentLoadout = type;
      document.getElementById('loadout-clean').classList.toggle('active', type === 'clean');
      document.getElementById('loadout-strike').classList.toggle('active', type === 'strike');

      const isStrike = type === 'strike';
      document.getElementById('top-weapons').style.display = isStrike ? 'inline' : 'none';
      document.getElementById('side-weapons').style.display = isStrike ? 'inline' : 'none';
    }
  </script>
</body>
</html>
