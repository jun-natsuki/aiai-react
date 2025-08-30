# aiai-react
React + Vite starter project for AiAi
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>AiAi — 한·일 결혼/교제 매칭 (MVP)</title>
  <style>
    /* ---------- Design tokens ---------- */
    :root{
      --bg:#ffffff;
      --panel:#ffffff;
      --card:#ffffff;
      --muted:#6b7280;
      --text:#0b0f19;
      --accent:#111111;
      --accent-2:#e5e7eb;
      --good:#16a34a;
      --bad:#dc2626;
      --border:#e5e7eb;
      --shadow: 0 8px 30px rgba(0,0,0,.06);
      --radius: 16px;
    }

    /* ---------- Base ---------- */
    *{box-sizing:border-box}
    html,body{height:100%}
    body{margin:0;background:var(--bg);color:var(--text);font-family:system-ui,-apple-system,Segoe UI,Roboto,Pretendard,'Noto Sans KR','Apple SD Gothic Neo',Arial,sans-serif}
    a{color:inherit}

    /* ---------- Header / Nav ---------- */
    header{position:sticky;top:0;z-index:10;background:rgba(255,255,255,.9);backdrop-filter:blur(8px);border-bottom:1px solid var(--border)}
    .bar{max-width:1100px;margin:auto;display:flex;gap:12px;align-items:center;justify-content:space-between;padding:12px 16px}
    .brand{font-weight:800;letter-spacing:.2px;display:flex;align-items:center;gap:12px;text-decoration:none}
    .brand .brand-sub{font-size:18px;line-height:1.2}

    nav{display:flex;gap:18px;flex-wrap:wrap;align-items:center}
    .navlink{display:inline-flex;align-items:center;font-size:16px;font-weight:700;background:transparent;border:none;padding:8px 0;color:var(--text);cursor:pointer;text-decoration:none}
    .navlink:hover{text-decoration:underline}
    .navlink[aria-current="page"]{text-decoration:underline 2px}

    /* ---------- Layout ---------- */
    main.container{max-width:1100px;margin:28px auto;padding:0 16px}
    .card{background:var(--card);border:1px solid var(--border);border-radius:var(--radius);padding:22px;box-shadow:var(--shadow)}
    .hero{text-align:center;display:grid;grid-template-columns:1fr;gap:16px}

    .grid{display:grid;grid-template-columns:repeat(12,minmax(0,1fr));gap:12px}
    .sm-3{grid-column:span 3}
    .sm-4{grid-column:span 4}
    .sm-6{grid-column:span 6}
    .sm-8{grid-column:span 8}
    .sm-12{grid-column:span 12}

    .features-grid{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:12px}
    .feat{display:flex;gap:12px;align-items:flex-start;padding:14px;border:1px solid var(--border);border-radius:12px}
    .feat .ico{font-size:22px;line-height:1}

    .row{display:flex;gap:10px;flex-wrap:wrap;align-items:center}

    /* ---------- Type helpers ---------- */
    .kicker{font-size:14px;color:var(--muted);margin:0 0 8px}
    .headline{font-size:36px;line-height:1.2;margin:0 0 10px;color:#0b0f19}
    .sub{color:#4b5563;margin:0 0 14px}
    .muted{color:var(--muted)}
    .help{font-size:14px;color:var(--muted)}
    .divider{height:1px;background:var(--border);margin:16px 0}

    /* ---------- Buttons ---------- */
    .btn{appearance:none;border:1px solid var(--border);background:#fff;color:#111;padding:10px 14px;border-radius:999px;cursor:pointer;font-weight:700}
    .btn:hover{background:#fafafa}
    .primary{border-color:#111;background:#111;color:#fff}
    .primary:hover{opacity:.9}
    .ghost{background:transparent}

    /* ---------- Forms ---------- */
    .input-row{display:flex;flex-direction:column;gap:6px;margin:10px 0}
    label.req::after{content:' *';color:var(--bad)}
    input,select{width:100%;padding:12px 12px;border:1px solid var(--border);border-radius:12px;font-size:16px}
    .sticky-cta{position:sticky;bottom:10px;justify-content:flex-end;background:linear-gradient(180deg,rgba(255,255,255,0),#fff 40%);padding-top:8px}

    /* ---------- Badges ---------- */
    .badge{display:inline-flex;align-items:center;gap:8px;padding:6px 10px;border-radius:999px;border:1px solid var(--border);font-weight:700;font-size:13px}
    .badge.warn{background:#fffbea;border-color:#fef3c7;color:#92400e}
    .badge.good{background:#ecfdf5;border-color:#d1fae5;color:#065f46}

    /* ---------- Hero visual placeholder ---------- */
    .hero-illus{height:160px;border-radius:14px;background:linear-gradient(135deg,#f6f7ff,#f0fbff);border:1px dashed var(--border)}

    /* ---------- Avatars / Pills / Lists ---------- */
    .avatar{width:72px;height:72px;border-radius:14px;border:1px solid var(--border);object-fit:cover;background:#fff}
    .list{display:flex;flex-wrap:wrap;gap:8px}
    .pill{display:inline-flex;align-items:center;gap:6px;border:1px solid var(--border);border-radius:999px;padding:6px 10px;font-size:14px}

    /* ---------- Toast ---------- */
    .toast{position:fixed;left:50%;bottom:18px;transform:translateX(-50%);background:#111;color:#fff;padding:10px 14px;border-radius:999px;display:none;z-index:20}

    /* ---------- Modal ---------- */
    .modal{position:fixed;inset:0;background:rgba(0,0,0,.4);display:none;align-items:center;justify-content:center;z-index:30}
    .modal .inner{background:#fff;border-radius:16px;border:1px solid var(--border);padding:18px;max-width:420px;width:90%}

    /* ---------- Footer ---------- */
    footer{border-top:1px solid var(--border);background:#fff}
    footer .foot-wrap{max-width:1100px;margin:0 auto;padding:18px 16px;display:flex;justify-content:center;gap:12px;flex-wrap:wrap}

    /* ---------- Responsive ---------- */
    @media (max-width: 900px){
      .features-grid{grid-template-columns:1fr 1fr}
      .sm-3,.sm-4,.sm-6,.sm-8{grid-column:span 12}
      .headline{font-size:30px}
    }
    @media (max-width: 520px){
      .features-grid{grid-template-columns:1fr}
      .brand .brand-sub{font-size:16px}
    }
  </style>
</head>
<body>
  <header>
    <div class="bar">
      <a class="brand" href="#home" onclick="ui.go('home');return false;">
        <!-- 로고 이미지 제거(요청) -->
        <span class="brand-sub">Ai<b>Ai</b> 아이아이 • <span lang="ja">相愛</span> • 한일결혼정보</span>
      </a>
      <div id="userBadge" class="badge warn">로그아웃 상태</div>
    </div>
    <div class="bar" style="padding-top:0">
      <nav>
        <a id="nav-home" class="navlink" href="#home" onclick="ui.go('home');return false;">홈</a>
        <a id="nav-login" class="navlink" href="#signup" onclick="ui.openAuth();return false;">로그인</a>
        <a id="nav-profile" class="navlink" href="#profile" onclick="ui.goProtected('profile');return false;">정보기입</a>
        <a id="nav-match" class="navlink" href="#match" onclick="ui.goProtected('match');return false;">매칭</a>
        <a id="nav-chat" class="navlink" href="#chat" onclick="ui.goProtected('chat');return false;">대화</a>
        <a id="nav-logout" class="navlink" href="#logout" onclick="ui.logout();return false;" style="display:none">로그아웃</a>
      </nav>
    </div>
  </header>

  <main class="container">
    <!-- HOME -->
    <section id="home" class="card hero">
      <div>
        <p class="kicker">AiAi — Korea ⇔ Japan</p>
        <h1 class="headline">간단히 시작하는 <b>진지한 만남</b></h1>
        <p class="sub">AI 1차 점수 + 매니저 최종 매칭. <b>10분 내 매칭</b>을 약속하는 한·일 결혼/교제 서비스.</p>
        <div class="row">
          <button class="btn primary" onclick="ui.openAuth()">지금 시작하기</button>
        </div>
      </div>
      <div class="hero-illus" aria-hidden="true"></div>
    </section>

    <!-- 강점/주요 기능 -->
    <section class="card features">
      <h2 style="margin-top:0">AiAi의 강점</h2>
      <div class="features-grid">
        <div class="feat"><div class="ico">⏱️</div><div><b>10분 내 매칭</b><div class="muted">AI 스코어링 후 매니저가 최종 선택</div></div></div>
        <div class="feat"><div class="ico">🗣️</div><div><b>자동 번역 채팅</b><div class="muted">KO⇄JA 실시간 대화(데모 모의)</div></div></div>
        <div class="feat"><div class="ico">🛡️</div><div><b>안전 검증</b><div class="muted">본인인증 + 운영자 검수</div></div></div>
        <div class="feat"><div class="ico">🎯</div><div><b>정교한 이상형</b><div class="muted">딜브레이커/성격 매트릭스</div></div></div>
        <div class="feat"><div class="ico">🌏</div><div><b>한·일 문화 케어</b><div class="muted">양국 문화/매너 가이드</div></div></div>
        <div class="feat"><div class="ico">📅</div><div><b>만남 스케줄링</b><div class="muted">오프라인/ZOOM 일정 조율</div></div></div>
      </div>
    </section>

    <!-- 왜 AiAi인가요? -->
    <section class="card">
      <h2 style="margin-top:0">왜 AiAi인가요?</h2>
      <div class="grid">
        <div class="sm-4 card"><h3>① 10분 내 매칭</h3><p class="muted">AI 점수로 상위 후보 선별 후 매니저가 최종 선택.</p></div>
        <div class="sm-4 card"><h3>② 번역 걱정 끝</h3><p class="muted">대화창에서 자동 번역(모의)로 언어 장벽 최소화.</p></div>
        <div class="sm-4 card"><h3>③ 안심 서비스</h3><p class="muted">본인인증과 운영자 검수로 유령 계정/리스크 감소.</p></div>
      </div>
    </section>

    <!-- 이용 순서 -->
    <section class="card">
      <h2 style="margin-top:0">이용 순서</h2>
      <div class="grid">
        <div class="sm-3 card"><h3>1. 가입/인증</h3><p class="muted">이메일·비번 입력 후 인증.</p></div>
        <div class="sm-3 card"><h3>2. 정보 기입</h3><p class="muted">기본·본인·이상형 3단계.</p></div>
        <div class="sm-3 card"><h3>3. 매칭 신청</h3><p class="muted">후보 5명 추천 → 선택.</p></div>
        <div class="sm-3 card"><h3>4. 대화/만남</h3><p class="muted">자동 번역 채팅·만남 조율.</p></div>
      </div>
    </section>

    <!-- AUTH (가입 + 로그인 한 화면) -->
    <section id="signup" class="card" style="display:none">
      <h2 style="margin-top:0">계정 생성 / 로그인</h2>
      <div class="help">가입→기본 정보→본인 정보→이상형 순으로 진행됩니다. <b>자세히 입력할수록 매칭될 확률이 높습니다.</b></div>
      <div class="grid">
        <div class="sm-6 card">
          <h3>기본 정보 기입(1단계)</h3>
          <div class="input-row"><label class="req">이메일</label><input id="su_email" type="email" placeholder="you@example.com"></div>
          <div class="input-row"><label class="req">닉네임</label><input id="su_nick" placeholder="별명"></div>
          <div class="input-row"><label class="req">비밀번호</label><input id="su_pw" type="password" placeholder="8자 이상"></div>
          <div class="input-row"><label>약관동의</label><label class="row" style="gap:8px"><input id="su_tos" type="checkbox"> 서비스 약관에 동의합니다</label></div>
          <button class="btn primary" onclick="auth.signup()">계정 생성</button>
          <div class="divider"></div>
          <h3>본인인증(모의)</h3>
          <div class="input-row"><label>연락수단</label>
            <select id="su_verify_type"><option value="sms">휴대폰(SMS)</option><option value="email">이메일</option></select>
          </div>
          <div class="input-row"><label>연락처</label><input id="su_verify_target" placeholder="010-0000-0000 / you@example.com"></div>
          <div class="row">
            <button class="btn ghost" onclick="auth.sendCode()">인증코드 전송(모의)</button>
            <input id="su_code" placeholder="인증코드 6자리" style="width:160px">
            <button class="btn ghost" onclick="auth.verifyCode()">인증 확인</button>
          </div>
          <div id="su_verify_msg" class="help"></div>
          <div class="divider"></div>
          <h3>기본 정보</h3>
          <div class="input-row"><label class="req">성별</label>
            <select id="ob_gender"><option value="male">남성</option><option value="female">여성</option></select>
          </div>
          <div class="input-row"><label class="req">출생년도</label><input id="ob_birth" type="number" min="1950" max="2010" placeholder="1998"></div>
          <div class="input-row"><label class="req">국가</label>
            <select id="ob_country"><option value="KR">대한민국</option><option value="JP">일본</option></select>
          </div>
          <div class="row sticky-cta"><button class="btn primary" onclick="ui.nextFromStep1()">다음: 본인 정보</button></div>
        </div>
        <div class="sm-6 card">
          <h3>이미 계정이 있으신가요?</h3>
          <div class="input-row"><label>이메일</label><input id="li_email" type="email"></div>
          <div class="input-row"><label>비밀번호</label><input id="li_pw" type="password"></div>
          <div class="row">
            <button class="btn ghost" onclick="auth.login()">로그인</button>
          </div>
          <div id="li_msg" class="help"></div>
        </div>
      </div>
    </section>

    <!-- PROFILE (SELF INFO) -->
    <section id="profile" class="card" style="display:none">
      <h2>정보 기입(2단계)</h2>
      <div class="help"><b>자세히 입력할수록 매칭될 확률이 높습니다.</b></div>
      <div class="grid">
        <div class="sm-6 card">
          <div class="row">
            <img id="pf_avatar" class="avatar" 
     src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///ywAAAAAAQABAAACAUwAOw==" 
     alt="avatar" />
            <div class="help">정면 증명사진 권장. 데모에서는 로컬 파일만 미리보기.</div>
          </div>
          <div class="input-row"><label>이름(실명)</label><input id="pf_realname" placeholder="홍길동"></div>
          <div class="input-row"><label>사진 업로드</label><input id="pf_photo" type="file" accept="image/*"></div>
          <div class="input-row"><label>나이</label><input id="pf_age" type="number" min="18" max="80"></div>
          <div class="input-row"><label>직업</label><input id="pf_job" placeholder="직업"></div>
          <div class="input-row"><label>연봉(만원)</label><input id="pf_income" type="number" step="100" placeholder="예: 4200"></div>
          <div class="input-row"><label>키(cm)</label><input id="pf_height" type="number" step="1" placeholder="예: 175"></div>
          <div class="input-row"><label>체형</label>
            <select id="pf_body"><option>슬렌더</option><option>보통</option><option>살집 있음</option></select>
          </div>
          <div class="input-row"><label>MBTI</label>
            <select id="pf_mbti"></select>
          </div>
          <div class="input-row"><label>종교</label>
            <select id="pf_religion"><option>무교</option><option>기독교</option><option>천주교</option><option>불교</option><option>기타</option></select>
          </div>
          <div class="input-row"><label>학력</label>
            <select id="pf_edu"><option>고졸</option><option>전문대졸</option><option>대졸</option><option>대학원 이상</option></select>
          </div>
          <div class="input-row"><label>흡연</label>
            <select id="pf_smoke"><option>비흡연</option><option>가끔</option><option>흡연</option></select>
          </div>
          <div class="input-row"><label>음주</label>
            <select id="pf_drink"><option>비음주</option><option>가끔</option><option>자주</option></select>
          </div>
          <div class="input-row"><label>자녀 계획</label>
            <select id="pf_child"><option>원함</option><option>아직 미정</option><option>원하지 않음</option></select>
          </div>
          <div class="input-row"><label>취미(자유)</label><input id="pf_hobby" placeholder="등산, 카페, 게임…"></div>
          <div class="input-row"><label>한마디 소개</label><input id="pf_bio" placeholder="본인을 한마디로…"></div>
          <button class="btn primary" onclick="data.saveProfile()">저장</button>
        </div>
        <div class="sm-6 card">
          <h3>성격 매트릭스(카테고리별 최대 3개)</h3>
          <div id="matrix"></div>
          <div class="divider"></div>
          <button class="btn ghost" onclick="matrix.clear()">선택 초기화</button>
        </div>
      </div>
      <div class="sticky-cta row"><button class="btn primary" onclick="ui.nextFromStep2()">다음: 이상형 정보</button></div>
    </section>

    <!-- PREFERENCES (IDEAL TYPE) -->
    <section id="prefs" class="card" style="display:none">
      <h2>이상형 정보 기입(3단계)</h2>
      <div class="help"><b>자세히 입력할수록 매칭될 확률이 높습니다.</b></div>
      <div class="grid">
        <div class="sm-6 card">
          <div class="input-row"><label>나이 선호</label>
            <select id="pr_age_type"><option>동갑</option><option>연하</option><option>연상</option></select>
          </div>
          <div class="row">
            <input id="pr_age_min" type="number" placeholder="최소" style="width:100px">
            <input id="pr_age_max" type="number" placeholder="최대" style="width:100px">
          </div>
          <div class="input-row"><label>연봉 최소(만원)</label><input id="pr_income_min" type="number" step="100"></div>
          <div class="input-row"><label>키 범위(cm)</label>
            <div class="row"><input id="pr_height_min" type="number" placeholder="최소" style="width:100px"><input id="pr_height_max" type="number" placeholder="최대" style="width:100px"></div>
          </div>
          <div class="input-row"><label>체형</label>
            <select id="pr_body"><option>무관</option><option>슬렌더</option><option>보통</option><option>살집 있음</option></select>
          </div>
          <div class="input-row"><label>MBTI</label>
            <select id="pr_mbti"><option>무관</option></select>
          </div>
          <div class="input-row"><label>취미(희망)</label><input id="pr_hobby" placeholder="상대 취미 희망"></div>
        </div>
        <div class="sm-6 card">
          <h3>성격 선호(카테고리별 3개)</h3>
          <div id="matrixPref"></div>
          <label class="row" style="margin-top:8px"><input id="pr_deal" type="checkbox"> 선택 조건을 필수(Dealbreaker)로 적용</label>
          <div class="divider"></div>
          <button class="btn ghost" onclick="matrixPref.clear()">선택 초기화</button>
        </div>
      </div>
      <div class="sticky-cta row"><button class="btn primary" onclick="data.savePrefs()">저장</button></div>
    </section>

    <!-- MATCHING -->
    <section id="match" class="card" style="display:none">
      <h2>5. 매칭</h2>
      <div class="help">버튼을 누르면 AI 점수(모의)로 상위 후보를 고르고, 매니저 최종 선택을 시뮬레이션합니다.</div>
      <div class="row" style="margin:8px 0">
        <button class="btn primary" onclick="engine.match()">매칭 신청</button>
        <button class="btn ghost" onclick="demo.seed()">데모용 프로필 재생성</button>
        <span id="match_msg" class="help"></span>
      </div>
      <div id="match_results" class="grid"></div>
    </section>

    <!-- CHAT -->
    <section id="chat" class="card" style="display:none">
      <h2>6. 대화 + 자동 번역(모의)</h2>
      <div class="help">실서비스에서는 번역 API(Google/DeepL 등) 연동. 데모는 언어 감지/번역을 <b>흉내</b>냅니다.</div>
      <div class="grid">
        <div class="sm-8 card">
          <div id="chat_log" style="height:260px;overflow:auto;border:1px solid var(--border);border-radius:12px;padding:8px;background:#fff"></div>
          <div class="row" style="margin-top:8px">
            <input id="chat_input" placeholder="메시지를 입력…" style="flex:1">
            <button class="btn primary" onclick="chat.send()">보내기</button>
          </div>
        </div>
        <div class="sm-4 card">
          <h3>7. 만남 신청</h3>
          <p class="help">양측이 모두 동의하면 오프라인/온라인(ZOOM) 중 선택하여 스케줄 조율.</p>
          <div class="row">
            <button class="btn ghost" onclick="chat.requestMeet('offline')">오프라인 만남 신청</button>
            <button class="btn ghost" onclick="chat.requestMeet('online')">ZOOM 만남 신청</button>
          </div>
          <div id="meet_status" class="help" style="margin-top:8px"></div>
        </div>
      </div>
    </section>
  </main>

  <div id="toast" class="toast"></div>

  <!-- Modal: 로그인 필요 -->
  <div id="modal" class="modal">
    <div class="inner">
      <h3>로그인 이후 사용 가능합니다</h3>
      <p class="help">계정으로 로그인 또는 신규 가입 후 이용하세요.</p>
      <div class="row" style="margin-top:8px">
        <button class="btn primary" onclick="ui.openAuth();ui.hideModal()">로그인 하러 가기</button>
        <button class="btn ghost" onclick="ui.hideModal()">닫기</button>
      </div>
    </div>
  </div>

  <footer>
    <div class="foot-wrap">
      <span class="muted">© 2025 AiAi</span>
      <span class="muted">｜</span>
      <a href="#home" class="muted" onclick="ui.go('home');return false;">홈</a>
      <span class="muted">｜</span>
      <a href="#signup" class="muted" onclick="ui.openAuth();return false;">시작하기</a>
    </div>
  </footer>

  <script>
    // ---- Utilities ----
    const $ = sel => document.querySelector(sel);
    const el = (tag, attrs={}, children=[])=>{const n=document.createElement(tag);Object.entries(attrs).forEach(([k,v])=>{if(k==='class') n.className=v; else if(k==='html') n.innerHTML=v; else if(k==='style') n.setAttribute('style',v); else n.setAttribute(k,v)});children.forEach(c=>n.appendChild(c));return n};
    const toast=(msg)=>{const t=$('#toast');t.textContent=msg;t.style.display='block';setTimeout(()=>t.style.display='none',1800)};
    const store={get:(k,d)=>{try{return JSON.parse(localStorage.getItem(k))??d}catch(e){return d}},set:(k,v)=>localStorage.setItem(k,JSON.stringify(v)),del:(k)=>localStorage.removeItem(k)};

    // ---- Auth (client-only mock) ----
    const auth={
      signup(){
        const email=$('#su_email').value?.trim();
        const nick=$('#su_nick').value?.trim();
        const pw=$('#su_pw').value;
        const tos=$('#su_tos').checked;
        if(!email||!nick||!pw||!tos){toast('필수 항목을 확인하세요');return;}
        const users=store.get('users',{});
        if(users[email]){toast('이미 가입된 이메일입니다');return;}
        users[email]={email,nick,pw,verified:false,createdAt:Date.now()};
        store.set('users',users);
        store.set('session',email);
        ui.badge();
        ui.refreshNav();
        toast('가입 완료. 인증을 진행하세요');
        ui.openAuth();
      },
      sendCode(){
        const email=store.get('session');
        if(!email){toast('먼저 가입/로그인 하세요');return;}
        const code=(Math.random()*900000+100000|0).toString();
        store.set('verify',{email,code,ts:Date.now()});
        $('#su_verify_msg').textContent=`인증코드(모의): ${code}`;
        toast('인증코드 전송(모의)');
      },
      verifyCode(){
        const vv=store.get('verify');
        const code=$('#su_code').value?.trim();
        const users=store.get('users',{});
        if(!vv){toast('코드 전송 후 시도하세요');return;}
        if(code===vv.code){
          users[vv.email].verified=true;
          store.set('users',users);
          toast('본인인증 완료');
          $('#su_verify_msg').textContent='인증됨';
          ui.badge();
        } else { toast('코드가 올바르지 않습니다'); }
      },
      login(){
        const email=$('#li_email').value?.trim();
        const pw=$('#li_pw').value;
        const u=store.get('users',{})[email];
        if(!u||u.pw!==pw){$('#li_msg').textContent='이메일/비밀번호를 확인하세요';return;}
        store.set('session',email);
        $('#li_msg').textContent='로그인 성공';
        toast('로그인');
        ui.badge();
        ui.refreshNav();
      },
      logout(){
        store.del('session');
        toast('로그아웃');
        ui.badge();
        ui.refreshNav();
      }
    };

    // ---- UI routing & guards ----
    const ui={
      go(id){
  document.querySelectorAll('main section[id]').forEach(s=>s.style.display='none');
  const el=document.getElementById(id); if(el){el.style.display='block'}
  const map={home:'nav-home',signup:'nav-login',profile:'nav-profile',match:'nav-match',chat:'nav-chat'};
  document.querySelectorAll('nav .navlink').forEach(a=>a.removeAttribute('aria-current'));
  const target=document.getElementById(map[id]); if(target) target.setAttribute('aria-current','page');
  window.scrollTo({top:0,behavior:'smooth'});
},
      goProtected(id){const email=store.get('session'); if(!email){ui.showModal();return;} ui.go(id);},
      openAuth(){ui.go('signup');},
      badge(){
        const email=store.get('session');
        const badge=$('#userBadge');
        if(email){
          const u=store.get('users',{})[email];
          const verified=u?.verified;
          badge.textContent=u?`${u.nick||email} · ${verified?'인증됨':'인증 필요'}`:'로그인';
          badge.className='badge '+(verified?'good':'warn');
        } else {
          badge.textContent='로그아웃 상태';
          badge.className='badge warn';
        }
      },
      refreshNav(){
        const logged=!!store.get('session');
        $('#nav-login').style.display=logged?'none':'inline-flex';
        $('#nav-logout').style.display=logged?'inline-flex':'none';
      },
      logout(){auth.logout();},
      showModal(){$('#modal').style.display='flex';},
      hideModal(){$('#modal').style.display='none';},
      nextFromStep1(){
        const g=$('#ob_gender').value;
        const b=$('#ob_birth').value;
        const c=$('#ob_country').value;
        if(!g||!b||!c){toast('기본 정보를 모두 입력하세요');return;}
        ui.go('profile');
      },
      nextFromStep2(){
        const need=['#pf_realname','#pf_age','#pf_income','#pf_height'];
        for(const sel of need){const v=$(sel).value?.trim(); if(!v){toast('본인 정보를 모두 입력하세요');return;}}
        const mb=$('#pf_mbti').value; if(!mb){toast('MBTI를 선택하세요');return;}
        data.saveProfile(); ui.go('prefs');
      }
    };

    // ---- MBTI options ----
    const MBTIs=["INTJ","INTP","ENTJ","ENTP","INFJ","INFP","ENFJ","ENFP","ISTJ","ISFJ","ESTJ","ESFJ","ISTP","ISFP","ESTP","ESFP"];
    function fillMBTI(){
      const sel=$('#pf_mbti');
      const sel2=$('#pr_mbti');
      MBTIs.forEach(x=>{const o=document.createElement('option');o.text=x;o.value=x;sel.appendChild(o)});
      MBTIs.forEach(x=>{const o=document.createElement('option');o.text=x;o.value=x;sel2.appendChild(o)});
    }

    // ---- Personality Matrix ----
    const MATRIX={
      "의사소통":["공감을 잘하는","외향적인","내성적인","다정한","설득력 있는","센스 있는","애교 있는","예의 바른","재미있는","조력적인"],
      "자기개발":["개인적인","고상한","대담한","부지런한","야심만만한","열정적인","영적인","재능 있는","전문적인"],
      "문제해결":["감각적","객관적인","격정적인","경계심이 강한","관찰력이 뛰어난","긍정적인","기발한","끈기 있는","모험심이 강한"],
      "팀워크":["감성적","겸손한","고마워할 줄 아는","놀기 좋아하는","느긋한","다가가기 쉬운","사심이 없는","순종적인","우호적인","위트 있는"],
      "리더십":["결단력 있는","관대한","관용적인","매력적인","영감을 주는","온화한","자비로운","잘 보살피는","중심이 잡힌","침착한"],
      "직업윤리":["건전한","꼼꼼한","낙천적인","명예를 중시하는","반듯한","방어적인","보수적인","사회적 인식이 높은","소박한","순수한"]
    };

    function buildMatrix(containerId,key){
      const wrap=$(containerId);
      wrap.innerHTML='';
      Object.entries(MATRIX).forEach(([cat,tags])=>{
        const box=el('div',{class:'card'});
        box.appendChild(el('h3',{html:`${cat}`}));
        const list=el('div',{class:'list'});
        tags.forEach(tag=>{
          const id=`${key}:${cat}:${tag}`;
          const item=el('label',{class:'pill'});
          const cb=el('input',{type:'checkbox',id});
          cb.addEventListener('change',()=>limitCategory(key,cat,3,id));
          item.appendChild(cb); item.appendChild(el('span',{html:tag}));
          list.appendChild(item);
        });
        box.appendChild(list);wrap.appendChild(box);
      });
    }
    const limitCategory=(key,cat,max,id)=>{
      const cbs=[...document.querySelectorAll(`input[id^="${key}:${cat}:"]`)];
      const selected=cbs.filter(x=>x.checked);
      if(selected.length>max){
        const last=document.getElementById(id);
        last.checked=false;
        toast(`${cat}는 최대 ${max}개`);
      }
    };
    const matrix={
      clear(){document.querySelectorAll('input[id^="self:"]').forEach(x=>x.checked=false);},
      read(){const out={};Object.keys(MATRIX).forEach(cat=>{out[cat]=[...document.querySelectorAll(`input[id^="self:${cat}:"]`)].filter(x=>x.checked).map(x=>x.id.split(':').pop())});return out;}
    };
    const matrixPref={
      clear(){document.querySelectorAll('input[id^="pref:"]').forEach(x=>x.checked=false);},
      read(){const out={};Object.keys(MATRIX).forEach(cat=>{out[cat]=[...document.querySelectorAll(`input[id^="pref:${cat}:"]`)].filter(x=>x.checked).map(x=>x.id.split(':').pop())});return out;}
    };

    // ---- Data save/load ----
    const data={
      saveProfile(){
        const email=store.get('session');
        if(!email){toast('로그인 필요');return;}
        const profile={
          realname:$('#pf_realname').value,
          age:+$('#pf_age').value||null,
          job:$('#pf_job').value,
          income:+$('#pf_income').value||null,
          height:+$('#pf_height').value||null,
          body:$('#pf_body').value,
          mbti:$('#pf_mbti').value,
          religion:$('#pf_religion').value,
          edu:$('#pf_edu').value,
          smoke:$('#pf_smoke').value,
          drink:$('#pf_drink').value,
          child:$('#pf_child').value,
          hobby:$('#pf_hobby').value,
          bio:$('#pf_bio').value,
          matrix:matrix.read(),
          country:$('#ob_country')?.value,
          gender:$('#ob_gender')?.value,
          birthYear:+$('#ob_birth')?.value||null,
          photo:store.get('tmp_photo_'+email)
        };
        const db=store.get('profiles',{});
        db[email]=profile;
        store.set('profiles',db);
        toast('프로필 저장 완료');
      },
      savePrefs(){
        const email=store.get('session');
        if(!email){toast('로그인 필요');return;}
        const ageMin=$('#pr_age_min').value, ageMax=$('#pr_age_max').value;
        if(!ageMin||!ageMax){toast('나이 범위를 입력하세요');return;}
        const prefs={
          ageType:$get('#pr_age_type'),
          ageMin:+ageMin,
          ageMax:+ageMax,
          incomeMin:+($('#pr_income_min').value)||0,
          heightMin:+($('#pr_height_min').value)||null,
          heightMax:+($('#pr_height_max').value)||null,
          body:$get('#pr_body'),
          mbti:$get('#pr_mbti'),
          hobby:$('#pr_hobby').value,
          matrix:matrixPref.read(),
          deal:$('#pr_deal').checked
        };
        const db=store.get('prefs',{});
        db[email]=prefs;
        store.set('prefs',db);
        toast('이상형 저장 완료');
        ui.go('match');
      }
    };
    function $get(sel){const v=$(sel)?.value;return v===undefined?null:v;}

    // photo preview
    window.addEventListener('change',e=>{
      if(e.target && e.target.id==='pf_photo'){
        const f=e.target.files?.[0];
        if(!f) return;
        const r=new FileReader();
        r.onload=()=>{store.set('tmp_photo_'+store.get('session'),r.result);$('#pf_avatar').src=r.result};
        r.readAsDataURL(f);
      }
    });

    // ---- Matching Engine (mock) ----
    const engine={
      score(me,pref,other){
        if(!other||!other.profile) return -1;
        const p=other.profile; let s=0;
        if(pref.heightMin && p.height>=pref.heightMin) s+=5;
        if(pref.heightMax && p.height<=pref.heightMax) s+=5;
        if(p.income && p.income>=(pref.incomeMin||0)) s+=6;
        if(pref.body && pref.body!=='무관' && p.body===pref.body) s+=4;
        const comp={"INTJ":["ENFP","ENTP"],"ENFP":["INTJ","INFJ"],"ISTJ":["ENFP","ESFP"],"ENFJ":["INFP","ISFP"]};
        if(pref.mbti && pref.mbti!=='무관'){
          if(p.mbti===pref.mbti) s+=4;
          if((comp[pref.mbti]||[]).includes(p.mbti)) s+=2;
        }
        const inter=(a,b)=>Object.keys(a).reduce((acc,k)=>acc+ a[k].filter(x=>b[k]?.includes(x)).length,0);
        s+= inter(pref.matrix,p.matrix)*2;
        if(pref.hobby && p.hobby && p.hobby.toLowerCase().includes(pref.hobby.toLowerCase())) s+=3;
        if(pref.deal){
          const ok=Object.keys(pref.matrix).every(k=>pref.matrix[k].length===0 || pref.matrix[k].some(t=>p.matrix[k]?.includes(t)));
          if(!ok) return -1;
        }
        return s;
      },
      match(){
        const email=store.get('session');
        if(!email){toast('로그인 필요');return;}
        const meProf=store.get('profiles',{})[email];
        const pref=store.get('prefs',{})[email];
        if(!meProf||!pref){toast('프로필/이상형을 먼저 저장하세요');return;}
        const all=store.get('demoUsers',[]).filter(u=>u.email!==email && u.profile?.gender!==meProf.gender);
        const ranked=all.map(u=>({u,score:this.score(meProf,pref,u)})).filter(x=>x.score>=0).sort((a,b)=>b.score-a.score).slice(0,5);
        const host=$('#match_results');
        host.innerHTML='';
        if(!ranked.length){host.innerHTML='<p class="help">조건에 맞는 후보가 없습니다. (데모 데이터 재생성 시도)</p>';return;}
        ranked.forEach(({u,score},i)=>{
          const c=el('div',{class:'sm-6 card'});
          c.appendChild(el('h3',{html:`후보 #${i+1} · 점수 <b>${score}</b>`}));
          const row=el('div',{class:'row'});
          const img=el('img',{class:'avatar',src:u.profile.photo||''});
          row.appendChild(img);
          const d=el('div');
          d.innerHTML=`<b>${u.profile.realname||u.nick}</b> (${u.profile.age||'?'}세) · ${u.profile.height||'?'}cm · ${u.profile.body}<br><span class=\"muted\">${u.profile.job||'직업 미상'} · 연봉 ${u.profile.income||'?'}만</span><br>MBTI ${u.profile.mbti||'-'} · 취미 ${u.profile.hobby||'-'}`;
          row.appendChild(d);
          c.appendChild(row);
          const btn=el('button',{class:'btn primary',html:'이 사람과 매칭'},[]);
          btn.addEventListener('click',()=>{store.set('chat_with',u.email);toast('매칭 성공 (데모)');ui.go('chat')});
          c.appendChild(el('div',{class:'row' },[btn]));
          host.appendChild(c);
        });
        $('#match_msg').textContent=`${ranked.length}명 추천됨 (모의 점수)`;
      }
    };

    // ---- Chat + Meeting (mock) ----
    const chat={
      send(){
        const box=$('#chat_input');
        const txt=box.value.trim();
        if(!txt) return;
        box.value='';
        const log=store.get('chat',[]);
        const withEmail=store.get('chat_with');
        const me=store.get('session');
        log.push({from:me,to:withEmail,txt,ts:Date.now(),lang:detect(txt),tr:translateMock(txt)});
        store.set('chat',log);
        this.render();
      },
      render(){
        const withEmail=store.get('chat_with');
        const me=store.get('session');
        const log=store.get('chat',[]).filter(m=> (m.from===me&&m.to===withEmail)||(m.from===withEmail&&m.to===me));
        const host=$('#chat_log'); host.innerHTML='';
        log.forEach(m=>{
          const mine=m.from===me;
          const bubble=el('div',{class:'card',style:`margin:6px 0;${mine?'border-color:#bbf7d0;background:#ecfdf5':''}`});
          bubble.innerHTML=`<div class=\"kicker\">${mine?'나':'상대'}</div><div>${escapeHtml(m.txt)}</div><div class=\"help\">언어:${m.lang} · 번역:${escapeHtml(m.tr)}</div>`;
          host.appendChild(bubble);
        });
        host.scrollTop=host.scrollHeight;
      },
      requestMeet(type){
        const st={type,status:'대기',ts:Date.now()};
        store.set('meet_req',st);
        $('#meet_status').textContent=`${type==='offline'?'오프라인':'ZOOM'} 만남 신청 보냈습니다 (모의)`;
      }
    };
    function detect(t){return /[ぁ-んァ-ヶ一-龯]/.test(t)?'JA':/[가-힣]/.test(t)?'KO':'EN'}
    function translateMock(t){const l=detect(t); if(l==='KO') return '[JA 번역 모의] '+t; if(l==='JA') return '[KO 번역 모의] '+t; return '[KO/JA 번역 모의] '+t}
    function escapeHtml(s){return s.replace(/[&<>"']/g,m=>({"&":"&amp;","<":"&lt;",">":"&gt;","\"":"&quot;","'":"&#39;"}[m]))}

    // ---- Demo data ----
    const demo={
      seed(){
        const pool=[
          {email:'jp1@demo',nick:'Yui',profile:{gender:'female',realname:'Yui',age:27,height:162,body:'슬렌더',job:'간호사',income:3800,mbti:'ENFP',hobby:'카페, 하이킹',bio:'明るい性格',matrix:pickMatrix(['의사소통:재미있는,조력적인','자기개발:야심만만한,열정적인','리더십:매력적인'])}},
          {email:'jp2@demo',nick:'Aoi',profile:{gender:'female',realname:'Aoi',age:29,height:168,body:'보통',job:'디자이너',income:4200,mbti:'INFJ',hobby:'사진, 미술관',bio:'落ち着き',matrix:pickMatrix(['의사소통:공감을 잘하는,센스 있는','직업윤리:꼼꼼한'])}},
          {email:'jp3@demo',nick:'Hana',profile:{gender:'female',realname:'Hana',age:31,height:170,body:'보통',job:'엔지니어',income:6000,mbti:'INTJ',hobby:'게임, 카페',matrix:pickMatrix(['문제해결:관찰력이 뛰어난,끈기 있는','리더십:결단력 있는'])}},
          {email:'krf1@demo',nick:'민지',profile:{gender:'female',realname:'민지',age:26,height:165,body:'슬렌더',job:'교사',income:3600,mbti:'ISFJ',hobby:'독서, 요가',matrix:pickMatrix(['팀워크:우호적인,위트 있는','직업윤리:반듯한'])}},
          {email:'krm1@demo',nick:'현수',profile:{gender:'male',realname:'현수',age:30,height:177,body:'보통',job:'개발자',income:6500,mbti:'INTP',hobby:'게임, 등산',matrix:pickMatrix(['문제해결:객관적인,기발한','리더십:침착한'])}},
          {email:'krm2@demo',nick:'도윤',profile:{gender:'male',realname:'도윤',age:28,height:181,body:'슬렌더',job:'마케터',income:4800,mbti:'ENFJ',hobby:'런닝, 커피',matrix:pickMatrix(['의사소통:설득력 있는,재미있는','팀워크:우호적인'])}},
          {email:'krm3@demo',nick:'지호',profile:{gender:'male',realname:'지호',age:33,height:175,body:'살집 있음',job:'간호사',income:4200,mbti:'ISFP',hobby:'사진, 캠핑',matrix:pickMatrix(['자기개발:부지런한,야심만만한','리더십:온화한'])}},
          {email:'jp4@demo',nick:'Rin',profile:{gender:'female',realname:'Rin',age:25,height:158,body:'보통',job:'학생',income:2200,mbti:'ESFP',hobby:'여행, 카페',matrix:pickMatrix(['팀워크:놀기 좋아하는,느긋한'])}},
          {email:'jp5@demo',nick:'Noa',profile:{gender:'female',realname:'Noa',age:28,height:172,body:'보통',job:'연구원',income:7000,mbti:'ENFP',hobby:'러닝, 보드게임',matrix:pickMatrix(['리더십:영감을 주는,매력적인'])}},
          {email:'jp6@demo',nick:'Mio',profile:{gender:'female',realname:'Mio',age:27,height:169,body:'슬렌더',job:'번역가',income:3900,mbti:'INFP',hobby:'영화, 독서',matrix:pickMatrix(['의사소통:공감을 잘하는,예의 바른'])}}
        ];
        store.set('demoUsers',pool);
        toast('데모 프로필 10명 생성됨');
      }
    };
    function pickMatrix(hints){const m={"의사소통":[],"자기개발":[],"문제해결":[],"팀워크":[],"리더십":[],"직업윤리":[]};(hints||[]).forEach(h=>{const [c,ts]=h.split(':');(ts||'').split(',').forEach(t=>t&&m[c].push(t.trim()))});return m}

    // ---- Init ----
    function init(){
      fillMBTI();
      buildMatrix('#matrix','self');
      buildMatrix('#matrixPref','pref');
      ui.badge();
      ui.refreshNav();
      ui.go('home');
    }
    document.addEventListener('DOMContentLoaded', init);
  </script>
</body>
</html>
