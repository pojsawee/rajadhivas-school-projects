<html lang="th">
<head>
  <meta charset="utf-8" />
  <title>ระบบติดตามเอกสารโครงการ - Rajadhivas School</title>
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;600&display=swap" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>
  <style>
    body { font-family: 'Kanit', sans-serif; margin:0; padding:0; background:#f4f6f8; color:#222 }
    header { background:#0b5; color:#013; padding:18px; display:flex; align-items:center; justify-content:space-between }
    header h1 { margin:0; font-size:18px }
    .container { padding:18px; max-width:1100px; margin:18px auto; }
    .card { background:#fff; border-radius:8px; padding:16px; box-shadow:0 1px 4px rgba(0,0,0,0.08); margin-bottom:12px }
    .grid { display:grid; grid-template-columns: 240px 1fr; gap:12px; }
    nav { background:#fafafa; padding:12px; border-radius:8px; }
    nav button { display:block; width:100%; margin-bottom:8px; padding:8px; border:0; background:#e9f5ee; border-radius:6px; cursor:pointer; text-align:left }
    nav button.active { background:#d5f0d7; font-weight:600 }
    .topbar { display:flex; gap:8px; align-items:center }
    .btn { background:#1976d2; color:#fff; padding:8px 12px; border-radius:6px; border:0; cursor:pointer }
    .btn.secondary { background:#666 }
    .form-row { display:flex; gap:8px; margin-bottom:8px }
    input[type=text], input[type=password], textarea, select, input[type=number] { padding:8px; border-radius:6px; border:1px solid #d0d7de; width:100%; }
    .list { margin-top:12px }
    .item { padding:12px; border:1px solid #eef2f5; border-radius:8px; margin-bottom:8px; display:flex; justify-content:space-between; align-items:flex-start; gap:8px }
    .meta { font-size:12px; color:#555; margin-top:6px }
    .badge { padding:6px 8px; border-radius:999px; background:#eee; font-weight:600; font-size:12px }
    .status-Draft { background:#ddd }
    .status-Proposed { background:#ffecb3 }
    .status-Approved { background:#c8e6c9 }
    .status-InProgress { background:#b3e5fc }
    .status-RequestDisbursement { background:#ffe0b2 }
    .status-ProposedToAdmin { background:#ffd54f }
    .status-ApprovedDisbursement { background:#a5d6a7 }
    .status-PaymentCompleted { background:#90caf9 }
    .timestamp { font-size:12px; color:#666 }
    .history { margin-top:8px; font-size:13px; background:#fafafa; padding:8px; border-radius:6px; border:1px solid #eee }
    .public-view { display:flex; gap:12px; flex-wrap:wrap }
    .public-card { width:300px; }
    footer { text-align:center; padding:12px; color:#666; font-size:13px }

    /* simple modal */
    .modal { position:fixed; left:0; right:0; top:0; bottom:0; background:rgba(0,0,0,0.4); display:flex; align-items:center; justify-content:center; }
    .modal .card { width:600px; max-width:95%; }
    @media (max-width:800px) {
      .grid { grid-template-columns: 1fr; }
      nav { display:flex; gap:8px; overflow:auto }
      nav button { width:auto; flex:0 0 auto }
      .public-card { width:100% }
    }
  </style>
</head>
<body>
  <header>
    <h1>ระบบติดตามเอกสารโครงการ - โรงเรียนวัดราชาธิวาส</h1>
    <div class="topbar" id="topbar-area"></div>
  </header>

  <div class="container" id="app">
    <!-- app content mounts here -->
  </div>

  <footer>
    ตัวอย่างต้นแบบ (prototype) เก็บข้อมูลในเบราว์เซอร์ (localStorage) — นำไปต่อยอดเชื่อม backend ได้
  </footer>

<script>
mermaid.initialize({ startOnLoad: false });

/* ======= Data models + localStorage helpers ======= */
const LS_USERS_KEY = 'rds_users_v1';
const LS_REQ_KEY = 'rds_requests_v1';
const LS_SESS_KEY = 'rds_session';

const STATUS_FLOW = [
  { key:'Draft', label:'ร่าง' },
  { key:'Proposed', label:'เสนอ' },
  { key:'Approved', label:'อนุมัติกิจกรรม' },
  { key:'InProgress', label:'ดำเนินกิจกรรม' },
  { key:'RequestDisbursement', label:'ขอตั้งเบิก' },
  { key:'ProposedToAdmin', label:'เสนอผู้บริหาร' },
  { key:'ApprovedDisbursement', label:'อนุมัติเบิก' },
  { key:'PaymentCompleted', label:'จ่ายเงินเสร็จสิ้น' }
];

function nowLabel() {
  return new Date().toLocaleString('th-TH');
}

function loadUsers() {
  let raw = localStorage.getItem(LS_USERS_KEY);
  if (!raw) {
    const seed = [
      { id:'u_plan', name:'เจ้าหน้าที่แผนงาน', role:'plan', username:'plan', pwd:'plan123' },
      { id:'u_fin', name:'เจ้าหน้าที่การเงิน', role:'finance', username:'finance', pwd:'fin123' },
      { id:'u_proc', name:'เจ้าหน้าที่พัสดุ', role:'procure', username:'procure', pwd:'proc123' },
      { id:'u_admin', name:'ผู้ควบคุมระบบ', role:'admin', username:'admin', pwd:'admin123' }
    ];
    localStorage.setItem(LS_USERS_KEY, JSON.stringify(seed));
    return seed;
  }
  return JSON.parse(raw);
}
function saveUsers(u){ localStorage.setItem(LS_USERS_KEY, JSON.stringify(u)); }

function loadRequests() {
  let raw = localStorage.getItem(LS_REQ_KEY);
  if (!raw) {
    const seed = [
      {
        id: 'r-1',
        title: 'กิจกรรมทัศนศึกษา ป.4',
        description: 'ขอใช้งบประมาณสำหรับทัศนศึกษา ภาคเรียนที่ 1',
        amount: 12000,
        creatorId: 'u_plan',
        creatorName: 'เจ้าหน้าที่แผนงาน',
        status: 'Draft',
        history: [{ status:'Draft', by:'เจ้าหน้าที่แผนงาน', at: nowLabel(), note:'สร้างคำขอ' }]
      },
      {
        id: 'r-2',
        title: 'ซื้อวัสดุสำหรับกิจกรรมวิทยาศาสตร์',
        description: 'วัสดุการทดลอง',
        amount: 5000,
        creatorId: 'u_proc',
        creatorName: 'เจ้าหน้าที่พัสดุ',
        status: 'InProgress',
        history: [
          { status:'Draft', by:'เจ้าหน้าที่พัสดุ', at: nowLabel(), note:'สร้างคำขอ' },
          { status:'Proposed', by:'เจ้าหน้าที่พัสดุ', at: nowLabel(), note:'เสนอ' },
          { status:'Approved', by:'เจ้าหน้าที่แผนงาน', at: nowLabel(), note:'อนุมัติกิจกรรม' },
          { status:'InProgress', by:'เจ้าหน้าที่พัสดุ', at: nowLabel(), note:'ดำเนินกิจกรรม' }
        ]
      }
    ];
    localStorage.setItem(LS_REQ_KEY, JSON.stringify(seed));
    return seed;
  }
  return JSON.parse(raw);
}
function saveRequests(r){ localStorage.setItem(LS_REQ_KEY, JSON.stringify(r)); }

function sessionUser() {
  const raw = localStorage.getItem(LS_SESS_KEY);
  return raw ? JSON.parse(raw) : null;
}
function setSession(u){ localStorage.setItem(LS_SESS_KEY, JSON.stringify(u)); }
function clearSession(){ localStorage.removeItem(LS_SESS_KEY); }

/* ======= Helpers ======= */
function uid(prefix='id') {
  return prefix + '-' + Math.random().toString(36).slice(2,9);
}
function getStatusLabel(key) {
  const s = STATUS_FLOW.find(x=>x.key===key);
  return s ? s.label : key;
}

/* ======= Render / Routing ======= */
const app = document.getElementById('app');
const topbar = document.getElementById('topbar-area');

function seedIfNeeded() {
  loadUsers(); loadRequests();
}
seedIfNeeded();

function renderTopbar() {
  const user = sessionUser();
  topbar.innerHTML = '';
  const pubBtn = document.createElement('button');
  pubBtn.className='btn secondary';
  pubBtn.textContent='Public View';
  pubBtn.onclick = ()=> { renderPublicView(); };
  topbar.appendChild(pubBtn);

  if (user) {
    const who = document.createElement('div');
    who.textContent = user.name + ' (' + user.role + ')';
    who.style.marginRight='10px';
    topbar.appendChild(who);

    const logout = document.createElement('button');
    logout.className='btn';
    logout.textContent='ออกจากระบบ';
    logout.onclick = ()=>{ clearSession(); renderLogin(); };
    topbar.appendChild(logout);
  } else {
    const loginBtn = document.createElement('button');
    loginBtn.className='btn';
    loginBtn.textContent='เข้าสู่ระบบ';
    loginBtn.onclick = ()=>{ renderLogin(); };
    topbar.appendChild(loginBtn);
  }
}

function renderLogin(message='') {
  renderTopbar();
  app.innerHTML = '';
  const c = document.createElement('div');
  c.className='card';
  c.innerHTML = `
    <h2>เข้าสู่ระบบเจ้าหน้าที่</h2>
    <p>ใช้บัญชีทดสอบ: plan/plan123, finance/fin123, procure/proc123, admin/admin123</p>
    <div id="login-msg" style="color:red">${message}</div>
    <div style="display:flex;gap:8px;flex-wrap:wrap">
      <div style="flex:1;min-width:260px">
        <label>บัญชีผู้ใช้</label>
        <input id="login-username" type="text" />
      </div>
      <div style="flex:1;min-width:200px">
        <label>รหัสผ่าน</label>
        <input id="login-password" type="password" />
      </div>
    </div>
    <div style="margin-top:8px">
      <button id="login-btn" class="btn">เข้าสู่ระบบ</button>
      <button id="public-btn" class="btn secondary">ดูสาธารณะ</button>
    </div>
  `;
  app.appendChild(c);

  document.getElementById('login-btn').onclick = () => {
    const u = document.getElementById('login-username').value.trim();
    const p = document.getElementById('login-password').value;
    const users = loadUsers();
    const found = users.find(x=>x.username===u && x.pwd===p);
    if (found) {
      setSession({ id:found.id, name:found.name, role:found.role, username:found.username });
      renderDashboard();
    } else {
      renderLogin('ไม่พบผู้ใช้หรือรหัสผ่านไม่ถูกต้อง');
    }
  };
  document.getElementById('public-btn').onclick = ()=> renderPublicView();
}

function renderDashboard() {
  renderTopbar();
  app.innerHTML = '';
  const grid = document.createElement('div');
  grid.className='grid';

  const nav = document.createElement('nav');

  const btns = [
    { id:'btn-new', label:'สร้างคำขอ/กิจกรรม' },
    { id:'btn-list', label:'รายการคำขอ' },
    { id:'btn-public', label:'ดูสาธารณะ' },
    { id:'btn-staff', label:'จัดการเจ้าหน้าที่ (admin)' }
  ];
  const user = sessionUser();
  btns.forEach(b=>{
    const btn = document.createElement('button');
    btn.textContent = b.label;
    btn.id = b.id;
    // hide staff manager if not admin
    if (b.id==='btn-staff' && (!user || user.role!=='admin')) btn.style.display='none';
    btn.onclick = ()=> { nav.querySelectorAll('button').forEach(x=>x.classList.remove('active')); btn.classList.add('active'); if (b.id==='btn-new') renderNewRequestForm(); if (b.id==='btn-list') renderRequestsList(); if (b.id==='btn-public') renderPublicView(); if (b.id==='btn-staff') renderStaffManagement(); };
    nav.appendChild(btn);
  });

  const main = document.createElement('div');
  main.id='main-area';

  grid.appendChild(nav);
  grid.appendChild(main);
  app.appendChild(grid);

  // default view
  document.getElementById('btn-list').classList.add('active');
  renderRequestsList();
}

function renderRequestsList() {
  const main = document.getElementById('main-area');
  main.innerHTML = '';
  const c = document.createElement('div');
  c.className='card';
  c.innerHTML = `<h3>รายการคำขอ/กิจกรรม</h3>`;
  main.appendChild(c);

  const controls = document.createElement('div');
  controls.style.display='flex';
  controls.style.gap='8px';
  controls.style.marginBottom='12px';
  const addBtn = document.createElement('button');
  addBtn.className='btn'; addBtn.textContent='สร้างคำขอใหม่';
  addBtn.onclick = ()=> renderNewRequestForm();
  controls.appendChild(addBtn);

  const publicBtn = document.createElement('button');
  publicBtn.className='btn secondary'; publicBtn.textContent='ดูสาธารณะ';
  publicBtn.onclick = ()=> renderPublicView();
  controls.appendChild(publicBtn);

  c.appendChild(controls);

  const list = document.createElement('div');
  list.className='list';
  c.appendChild(list);

  const reqs = loadRequests();
  if (reqs.length===0) {
    list.innerHTML = '<div class="item">ไม่มีคำขอ</div>';
    return;
  }

  reqs.forEach(r=>{
    const it = document.createElement('div');
    it.className='item';
    const left = document.createElement('div');
    left.style.flex='1';
    left.innerHTML = `<strong>${r.title}</strong> <div class="meta">${r.description || ''}</div>
      <div class="meta">ผู้สร้าง: ${r.creatorName} | จำนวนเงิน: ${r.amount} บาท</div>
      <div class="history"><strong>ประวัติสถานะ:</strong>
        ${r.history.map(h=>`<div class="timestamp">[${h.at}] ${h.by} → ${getStatusLabel(h.status)} ${h.note?'- '+h.note:''}</div>`).join('')}
      </div>
    `;
    left.style.minWidth='0';
    it.appendChild(left);

    const right = document.createElement('div');
    right.style.width='260px';
    right.style.textAlign='right';
    const badge = document.createElement('div');
    badge.className = 'badge status-' + r.status;
    badge.textContent = getStatusLabel(r.status);
    right.appendChild(badge);

    right.appendChild(document.createElement('div')).style.height='8px';

    // action buttons depending on role & status
    const user = sessionUser();
    function addAction(label, fn, cls='btn') {
      const b = document.createElement('button');
      b.className = cls;
      b.style.display='block';
      b.style.marginBottom='6px';
      b.textContent = label;
      b.onclick = ()=>{ fn(); renderRequestsList(); };
      right.appendChild(b);
    }

    // everyone (logged in) can view details
    addAction('ดูรายละเอียด', ()=> showRequestModal(r.id), 'btn secondary');

    if (user) {
      const isCreator = user.id===r.creatorId;
      // allow edit/delete for creator or admin (only for non-finalized)
      if ((isCreator || user.role==='admin') && r.status !== 'PaymentCompleted') {
        addAction('แก้ไขคำขอ', ()=> renderEditRequestForm(r.id), 'btn');
        addAction('ลบคำขอ', ()=> { if (confirm('ลบคำขอนี้?')) { deleteRequest(r.id); renderRequestsList(); } }, 'btn secondary');
      }

      // Approval & status transitions - example rules (canปรับได้)
      // - plan/finance/procure/admin can approve initial Proposed -> Approved
      // - any staff can move Draft -> Proposed
      // - after Approved -> InProgress
      // - at InProgress, creator/staff can RequestDisbursement (ขอตั้งเบิก)
      // - at RequestDisbursement, finance/admin can change to ProposedToAdmin (เสนอผู้บริหาร)
      // - after ProposedToAdmin, admin can mark ApprovedDisbursement and then PaymentCompleted
      if (r.status === 'Draft') {
        if (user.role !== 'public') addAction('เสนอ (เปลี่ยนเป็น เสนอ)', ()=> changeStatus(r.id,'Proposed','เสนอคำขอ'), 'btn');
      }
      if (r.status === 'Proposed') {
        if (['plan','finance','procure','admin'].includes(user.role)) addAction('อนุมัติกิจกรรม', ()=> changeStatus(r.id,'Approved','อนุมัติกิจกรรม'), 'btn');
      }
      if (r.status === 'Approved') {
        addAction('เปลี่ยนเป็น ดำเนินกิจกรรม', ()=> changeStatus(r.id,'InProgress','เริ่มดำเนินกิจกรรม'), 'btn');
      }
      if (r.status === 'InProgress') {
        if (['finance','procure','plan','admin'].includes(user.role)) addAction('ขอตั้งเบิก', ()=> changeStatus(r.id,'RequestDisbursement','ขอตั้งเบิก'), 'btn');
      }
      if (r.status === 'RequestDisbursement') {
        if (['finance','procure','plan','admin'].includes(user.role)) addAction('เสนอผู้บริหาร', ()=> changeStatus(r.id,'ProposedToAdmin','เสนอผู้บริหาร'), 'btn');
      }
      if (r.status === 'ProposedToAdmin') {
        if (['admin','finance'].includes(user.role)) addAction('อนุมัติเบิก', ()=> changeStatus(r.id,'ApprovedDisbursement','อนุมัติเบิก'), 'btn');
      }
      if (r.status === 'ApprovedDisbursement') {
        if (['admin','finance'].includes(user.role)) addAction('จ่ายเงินเสร็จสิ้น', ()=> changeStatus(r.id,'PaymentCompleted','จ่ายเงินเสร็จสิ้น'), 'btn');
      }
    } else {
      // not logged
      right.appendChild(document.createElement('div')).textContent = 'ล็อกอินเพื่อจัดการ';
    }

    it.appendChild(right);
    list.appendChild(it);
  });
}

/* ======= CRUD & status management ======= */
function createRequest(data) {
  const reqs = loadRequests();
  reqs.push(data);
  saveRequests(reqs);
}
function updateRequest(id, patch) {
  const reqs = loadRequests();
  const idx = reqs.findIndex(r=>r.id===id);
  if (idx>=0) {
    reqs[idx] = Object.assign(reqs[idx], patch);
    saveRequests(reqs);
  }
}
function deleteRequest(id) {
  let reqs = loadRequests();
  reqs = reqs.filter(r=>r.id!==id);
  saveRequests(reqs);
}

function changeStatus(id, newStatus, note='') {
  const reqs = loadRequests();
  const r = reqs.find(x=>x.id===id);
  if (!r) return;
  const user = sessionUser();
  const by = user ? user.name : 'ผู้ใช้ไม่ทราบ';
  r.status = newStatus;
  r.history = r.history || [];
  r.history.push({ status:newStatus, by:by, at: nowLabel(), note: note || '' });
  saveRequests(reqs);
  alert('เปลี่ยนสถานะเป็น: ' + getStatusLabel(newStatus));
}

/* ======= Forms & Modals ======= */
function renderNewRequestForm() {
  const main = document.getElementById('main-area');
  main.innerHTML = '';
  const c = document.createElement('div'); c.className='card';
  c.innerHTML = `<h3>สร้างคำขอ/กิจกรรมใหม่</h3>`;
  const form = document.createElement('div');
  form.innerHTML = `
    <div class="form-row">
      <div style="flex:2"><label>หัวข้อ</label><input id="f-title" type="text" /></div>
      <div style="flex:1"><label>จำนวนเงิน (บาท)</label><input id="f-amount" type="number" min="0" /></div>
    </div>
    <div><label>รายละเอียด</label><textarea id="f-desc" rows="4"></textarea></div>
    <div style="margin-top:8px"><button id="f-save" class="btn">บันทึก</button> <button id="f-cancel" class="btn secondary">ยกเลิก</button></div>
  `;
  c.appendChild(form);
  main.appendChild(c);

  document.getElementById('f-cancel').onclick = ()=> renderRequestsList();
  document.getElementById('f-save').onclick = ()=> {
    const user = sessionUser();
    if (!user) { alert('ต้องเข้าสู่ระบบ'); return; }
    const title = document.getElementById('f-title').value.trim();
    const desc = document.getElementById('f-desc').value.trim();
    const amount = Number(document.getElementById('f-amount').value || 0);
    if (!title) { alert('กรุณากรอกหัวข้อ'); return; }
    const newReq = {
      id: uid('r'),
      title, description: desc, amount,
      creatorId: user.id, creatorName: user.name,
      status: 'Draft',
      history: [{ status:'Draft', by:user.name, at: nowLabel(), note:'สร้างคำขอ' }]
    };
    createRequest(newReq);
    alert('สร้างคำขอสำเร็จ');
    renderRequestsList();
  };
}

function renderEditRequestForm(id) {
  const reqs = loadRequests();
  const r = reqs.find(x=>x.id===id);
  if (!r) { alert('ไม่พบคำขอ'); return; }
  const main = document.getElementById('main-area');
  main.innerHTML = '';
  const c = document.createElement('div'); c.className='card';
  c.innerHTML = `<h3>แก้ไขคำขอ</h3>`;
  const form = document.createElement('div');
  form.innerHTML = `
    <div class="form-row">
      <div style="flex:2"><label>หัวข้อ</label><input id="e-title" type="text" value="${escapeHtml(r.title)}" /></div>
      <div style="flex:1"><label>จำนวนเงิน (บาท)</label><input id="e-amount" type="number" value="${r.amount}" min="0" /></div>
    </div>
    <div><label>รายละเอียด</label><textarea id="e-desc" rows="4">${escapeHtml(r.description)}</textarea></div>
    <div style="margin-top:8px"><button id="e-save" class="btn">บันทึก</button> <button id="e-cancel" class="btn secondary">ยกเลิก</button></div>
  `;
  c.appendChild(form);
  main.appendChild(c);

  document.getElementById('e-cancel').onclick = ()=> renderRequestsList();
  document.getElementById('e-save').onclick = ()=> {
    const title = document.getElementById('e-title').value.trim();
    const desc = document.getElementById('e-desc').value.trim();
    const amount = Number(document.getElementById('e-amount').value || 0);
    if (!title) { alert('กรุณากรอกหัวข้อ'); return; }
    updateRequest(id, { title, description: desc, amount });
    alert('บันทึกเรียบร้อย');
    renderRequestsList();
  };
}

function showRequestModal(id) {
  const reqs = loadRequests();
  const r = reqs.find(x=>x.id===id);
  if (!r) return;
  const modal = document.createElement('div'); modal.className='modal';
  const card = document.createElement('div'); card.className='card';
  card.innerHTML = `<h3>${r.title}</h3>
    <div><strong>รายละเอียด:</strong> ${escapeHtml(r.description || '')}</div>
    <div><strong>จำนวนเงิน:</strong> ${r.amount} บาท</div>
    <div><strong>สถานะปัจจุบัน:</strong> <span class="badge status-${r.status}">${getStatusLabel(r.status)}</span></div>
    <div class="history"><strong>ประวัติ:</strong>
      ${r.history.map(h=>`<div class="timestamp">[${h.at}] ${h.by} → ${getStatusLabel(h.status)} ${h.note?'- '+escapeHtml(h.note):''}</div>`).join('')}
    </div>
    <div style="margin-top:8px"><button id="m-close" class="btn">ปิด</button></div>
    <div id="m-diagram" style="margin-top:12px"></div>
  `;
  modal.appendChild(card);
  document.body.appendChild(modal);
  document.getElementById('m-close').onclick = ()=> document.body.removeChild(modal);

  // render mermaid diagram of this request's progress
  const nodes = STATUS_FLOW.map(s=>{
    const found = r.history.find(h=>h.status===s.key);
    const label = found ? `${s.label}\\n${found.at}` : s.label;
    return { key:s.key, label };
  });
  let mermaidSrc = 'graph LR\\n';
  for (let i=0;i<nodes.length-1;i++) {
    mermaidSrc += `${nodes[i].key}[ "${nodes[i].label}" ] --> ${nodes[i+1].key}[ "${nodes[i+1].label}" ]\\n`;
  }
  // highlight current node
  mermaidSrc += `classDef current fill:#fffbcc,stroke:#f39c12; class ${r.status} current;`;
  const mdiv = document.getElementById('m-diagram');
  mdiv.innerHTML = '<div class="mermaid">' + mermaidSrc + '</div>';
  mermaid.init(undefined, mdiv);
}

/* ======= Public View (view-only) ======= */
function renderPublicView() {
  renderTopbar();
  app.innerHTML = '';
  const c = document.createElement('div'); c.className='card';
  c.innerHTML = `<h3>มุมมองสาธารณะ — สถานะงานทั้งระบบ</h3>
    <p>ผู้ใช้งานสาธารณะสามารถดูสถานะของงานแต่ละรายการเป็นแผนผังและรายการได้</p>
    <div style="display:flex;gap:12px;flex-wrap:wrap">
      <div style="flex:1;min-width:320px" id="pub-list-area"></div>
      <div style="flex:1;min-width:320px" id="pub-diagram-area"></div>
    </div>
  `;
  app.appendChild(c);

  const reqs = loadRequests();
  const listArea = document.getElementById('pub-list-area');
  const diagArea = document.getElementById('pub-diagram-area');

  listArea.innerHTML = '<h4>รายการงาน</h4>';
  const pview = document.createElement('div'); pview.className='public-view';
  reqs.forEach(r=>{
    const pc = document.createElement('div'); pc.className='card public-card';
    pc.innerHTML = `<strong>${r.title}</strong>
      <div class="meta">${r.description || ''}</div>
      <div class="meta">จำนวนเงิน: ${r.amount} บาท</div>
      <div style="margin-top:6px"><span class="badge status-${r.status}">${getStatusLabel(r.status)}</span></div>
      <div class="timestamp" style="margin-top:6px">ล่าสุด: ${r.history[r.history.length-1].at} โดย ${r.history[r.history.length-1].by}</div>
      <div style="margin-top:6px"><button class="btn" onclick='(function(){ const id="${r.id}"; const ev = new CustomEvent("rds_open_public", { detail:id }); window.dispatchEvent(ev); })()'>ดูแผนผัง</button></div>
    `;
    pview.appendChild(pc);
  });
  listArea.appendChild(pview);

  diagArea.innerHTML = '<h4>แผนผังรวม (คลิกงานเพื่อดูรายละเอียด)</h4><div id="pub-merged-diagram"></div>';
  // merged diagram: show all requests on a board grouped by status
  let diagSrc = 'flowchart LR\\n';
  // create status nodes
  STATUS_FLOW.forEach(s => {
    diagSrc += `${s.key}["${s.label}"]\\n`;
  });
  // connect statuses
  for (let i=0;i<STATUS_FLOW.length-1;i++){
    diagSrc += `${STATUS_FLOW[i].key} --> ${STATUS_FLOW[i+1].key}\\n`;
  }
  // add subnodes: for each request add a small node under its current status
  reqs.forEach((r, idx)=>{
    const nodeId = `p${idx}`;
    const label = `${escapeForMermaid(r.title)}\\n(${r.amount} บาท)`;
    diagSrc += `${nodeId}["${label}"]\\n`;
    diagSrc += `${STATUS_FLOW.find(s=>s.key===r.status).key} --> ${nodeId}\\n`;
  });
  const pm = document.getElementById('pub-merged-diagram');
  pm.innerHTML = '<div class="mermaid">' + diagSrc + '</div>';
  mermaid.init(undefined, pm);

  // listen for open specific request
  window.rds_open_public_listener = function(e){
    const id = e.detail;
    showRequestModal(id);
  };
  window.addEventListener('rds_open_public', window.rds_open_public_listener);
}

/* ======= Staff Management (admin) ======= */
function renderStaffManagement() {
  const main = document.getElementById('main-area');
  main.innerHTML = '';
  const c = document.createElement('div'); c.className='card';
  c.innerHTML = `<h3>จัดการเจ้าหน้าที่ (ผู้ควบคุมระบบ)</h3>`;
  const users = loadUsers();
  const list = document.createElement('div');
  list.className='list';
  users.forEach(u=>{
    const it = document.createElement('div'); it.className='item';
    it.innerHTML = `<div><strong>${u.name}</strong> <div class="meta">บัญชี: ${u.username} | บทบาท: ${u.role}</div></div>`;
    const right = document.createElement('div');
    right.style.textAlign='right';
    const edit = document.createElement('button'); edit.className='btn'; edit.textContent='แก้ไข';
    edit.onclick = ()=> showEditUserModal(u.id);
    const reset = document.createElement('button'); reset.className='btn secondary'; reset.textContent='รีเซ็ตรหัส';
    reset.onclick = ()=> { const np = prompt('รหัสใหม่สำหรับ '+u.username, 'changeme'); if (np) { u.pwd=np; saveUsers(users); alert('เปลี่ยนรหัสแล้ว'); renderStaffManagement(); } };
    const del = document.createElement('button'); del.className='btn secondary'; del.textContent='ลบ';
    del.onclick = ()=> { if (confirm('ต้องการลบผู้ใช้ '+u.username+' ?')) { const arr = loadUsers().filter(x=>x.id!==u.id); saveUsers(arr); renderStaffManagement(); } };
    right.appendChild(edit); right.appendChild(reset); right.appendChild(del);
    it.appendChild(right);
    list.appendChild(it);
  });

  c.appendChild(list);
  const createBtn = document.createElement('button'); createBtn.className='btn'; createBtn.textContent='เพิ่มเจ้าหน้าที่ใหม่';
  createBtn.onclick = ()=> showCreateUserModal();
  c.appendChild(createBtn);

  main.appendChild(c);
}
function showCreateUserModal(){
  const modal = document.createElement('div'); modal.className='modal';
  const card = document.createElement('div'); card.className='card';
  card.innerHTML = `<h3>เพิ่มเจ้าหน้าที่</h3>
    <div><label>ชื่อ</label><input id="u-name" type="text" /></div>
    <div class="form-row"><div style="flex:1"><label>บัญชี</label><input id="u-user" type="text" /></div><div style="flex:1"><label>รหัสผ่าน</label><input id="u-pwd" type="password" /></div></div>
    <div><label>บทบาท</label>
      <select id="u-role"><option value="plan">plan</option><option value="finance">finance</option><option value="procure">procure</option><option value="admin">admin</option></select>
    </div>
    <div style="margin-top:8px"><button id="u-save" class="btn">บันทึก</button> <button id="u-cancel" class="btn secondary">ยกเลิก</button></div>
  `;
  modal.appendChild(card);
  document.body.appendChild(modal);
  document.getElementById('u-cancel').onclick = ()=> document.body.removeChild(modal);
  document.getElementById('u-save').onclick = ()=>{
    const name = document.getElementById('u-name').value.trim();
    const username = document.getElementById('u-user').value.trim();
    const pwd = document.getElementById('u-pwd').value;
    const role = document.getElementById('u-role').value;
    if (!name||!username||!pwd) { alert('กรุณากรอกข้อมูลให้ครบ'); return; }
    const users = loadUsers();
    if (users.find(x=>x.username===username)) { alert('ชื่อบัญชีมีอยู่แล้ว'); return; }
    users.push({ id: uid('u'), name, username, pwd, role });
    saveUsers(users);
    document.body.removeChild(modal);
    renderStaffManagement();
  };
}
function showEditUserModal(id) {
  const users = loadUsers();
  const u = users.find(x=>x.id===id);
  if (!u) return;
  const modal = document.createElement('div'); modal.className='modal';
  const card = document.createElement('div'); card.className='card';
  card.innerHTML = `<h3>แก้ไขเจ้าหน้าที่</h3>
    <div><label>ชื่อ</label><input id="eu-name" type="text" value="${escapeHtml(u.name)}" /></div>
    <div class="form-row"><div style="flex:1"><label>บัญชี</label><input id="eu-user" type="text" value="${escapeHtml(u.username)}" /></div><div style="flex:1"><label>รหัสผ่าน (เว้นว่างไม่เปลี่ยน)</label><input id="eu-pwd" type="password" /></div></div>
    <div><label>บทบาท</label>
      <select id="eu-role"><option value="plan">plan</option><option value="finance">finance</option><option value="procure">procure</option><option value="admin">admin</option></select>
    </div>
    <div style="margin-top:8px"><button id="eu-save" class="btn">บันทึก</button> <button id="eu-cancel" class="btn secondary">ยกเลิก</button></div>
  `;
  modal.appendChild(card);
  document.body.appendChild(modal);
  document.getElementById('eu-role').value = u.role;
  document.getElementById('eu-cancel').onclick = ()=> document.body.removeChild(modal);
  document.getElementById('eu-save').onclick = ()=>{
    const name = document.getElementById('eu-name').value.trim();
    const username = document.getElementById('eu-user').value.trim();
    const pwd = document.getElementById('eu-pwd').value;
    const role = document.getElementById('eu-role').value;
    if (!name||!username) { alert('กรุณากรอกข้อมูลให้ครบ'); return; }
    const other = users.filter(x=>x.id!==u.id);
    if (other.find(x=>x.username===username)) { alert('ชื่อบัญชีมีอยู่แล้ว'); return; }
    u.name = name; u.username = username; if (pwd) u.pwd = pwd; u.role = role;
    saveUsers(users);
    document.body.removeChild(modal);
    renderStaffManagement();
  };
}

/* ======= Utilities ======= */
function escapeHtml(s) { if (!s) return ''; return s.replace(/[&<>"']/g, function(m){ return {'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[m]; }); }
function escapeForMermaid(s){ if (!s) return ''; return s.replace(/"/g, '\\"').replace(/\n/g,'\\n'); }

/* ======= Init ======= */
(function init(){
  const user = sessionUser();
  if (user) renderDashboard(); else renderLogin();
})();
</script>
</body>
</html>
