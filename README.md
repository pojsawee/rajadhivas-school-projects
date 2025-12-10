<html lang="th">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Scaffold files for rajadhivas-school-projects — Copy & Paste</title>
  <style>
    body { font-family: system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial; margin: 20px; color:#111; }
    h1 { font-size:20px; margin-bottom:6px; }
    p { margin-top:6px; color:#333; }
    .file { border:1px solid #ddd; padding:12px; margin:14px 0; border-radius:6px; background:#fafafa; }
    .fname { font-weight:600; color:#0b66c3; margin-bottom:8px; display:block; }
    textarea { width:100%; height:240px; font-family: monospace; font-size:12px; white-space:pre; }
    .short { height:120px; }
    .controls { margin-top:8px; display:flex; gap:8px; align-items:center; }
    button { padding:6px 10px; border-radius:6px; border:1px solid #bbb; background:#fff; cursor:pointer; }
    button.copy-ok { background:#dff0d8; border-color:#8bc34a; }
    .hint { font-size:13px; color:#555; margin-top:6px; }
    .block { margin-top:12px; }
    summary { cursor:pointer; font-weight:600; }
    code.small { font-size:12px; color:#555; background:#f5f5f5; padding:3px 6px; border-radius:4px; }
  </style>
</head>
<body>
  <h1>Scaffold files for pojsawee/rajadhivas-school-projects</h1>
  <p>หน้า HTML นี้รวบรวมไฟล์ทั้งหมดของ scaffold ที่ผมเตรียมให้ — คุณสามารถกดปุ่ม "Copy" เพื่อคัดลอกเนื้อหาไฟล์แต่ละไฟล์ไปวางในไฟล์จริงบนเครื่องของคุณหรือใน editor บน GitHub</p>
  <p class="hint">คำแนะนำสั้น ๆ: แนะนำสร้างหรือ clone repository แล้วเพิ่มไฟล์เหล่านี้ (รักษาโครงสร้างโฟลเดอร์ backend/ และ frontend/) จากนั้น commit & push ขึ้น GitHub</p>

  <div class="file">
    <span class="fname">README.md</span>
    <textarea id="file-readme"># ระบบติดตามการจัดทำเอกสารโครงการกิจกรรม rajadhivas

สรุป: โปรเจกต์ตัวอย่างเป็น full-stack app (backend: Node.js + Express + SQLite, frontend: React) สำหรับจัดการการเสนอ/อนุมัติกิจกรรมและขอเบิกเงิน ตาม workflow ที่ขอไว้

โครงสร้าง:
- backend/  (API, DB)
- frontend/ (React SPA)

การติดตั้ง (เครื่องเดียว — ใช้ Node.js >= 16):
1. ติดตั้ง dependencies ทั้งสองส่วน
   - cd backend && npm install
   - cd ../frontend && npm install

2. สร้างฐานข้อมูลและ seed (backend):
   - cd backend
   - sqlite3 data.db < models.sql
   - sqlite3 data.db < seed.sql

3. ตั้งค่า environment (backend/.env)
   - ตัวอย่าง:
     JWT_SECRET=your_jwt_secret
     PORT=4000

4. รัน backend:
   - cd backend
   - npm start

5. รัน frontend:
   - cd frontend
   - npm start
   - แอปจะเปิดที่ http://localhost:3000 และเชื่อมกับ API ที่ http://localhost:4000/api

หมายเหตุ:
- โค้ดเป็น scaffold เพื่อใช้เป็นฐานพัฒนาต่อ (สิทธิ์/security ยังต้อง harden ก่อนใช้จริง)
- หากต้องการให้ผมทำให้เป็น repo บน GitHub พร้อม CI/CD/PR ให้บอกผมได้
</textarea>
    <div class="controls">
      <button onclick="copyText('file-readme')">Copy</button>
      <span id="ok-file-readme"></span>
    </div>
  </div>

  <div class="file">
    <span class="fname">LICENSE</span>
    <textarea id="file-license" class="short">MIT License

Copyright (c) 2025 pojsawee

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.</textarea>
    <div class="controls">
      <button onclick="copyText('file-license')">Copy</button>
      <span id="ok-file-license"></span>
    </div>
  </div>

  <div class="file">
    <span class="fname">.gitignore</span>
    <textarea id="file-gitignore" class="short">node_modules
.env
data.db</textarea>
    <div class="controls">
      <button onclick="copyText('file-gitignore')">Copy</button>
      <span id="ok-file-gitignore"></span>
    </div>
  </div>

  <!-- backend/package.json -->
  <div class="file">
    <span class="fname">backend/package.json</span>
    <textarea id="file-backend-package">{
  "name": "wr-project-backend",
  "version": "1.0.0",
  "main": "server.js",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  },
  "dependencies": {
    "bcrypt": "^5.1.0",
    "cors": "^2.8.5",
    "express": "^4.18.2",
    "jsonwebtoken": "^9.0.0",
    "sqlite3": "^5.1.6",
    "body-parser": "^1.20.2"
  },
  "devDependencies": {
    "nodemon": "^2.0.22"
  }
}</textarea>
    <div class="controls">
      <button onclick="copyText('file-backend-package')">Copy</button>
      <span id="ok-file-backend-package"></span>
    </div>
  </div>

  <div class="file">
    <span class="fname">backend/server.js</span>
    <textarea id="file-backend-server">// backend/server.js
// Entry point ของ API
const express = require('express');
const bodyParser = require('body-parser');
const cors = require('cors');
const authRoutes = require('./routes/auth');
const usersRoutes = require('./routes/users');
const projectsRoutes = require('./routes/projects');
const { initDb } = require('./db');

require('dotenv').config();

const app = express();
app.use(cors());
app.use(bodyParser.json());

initDb(); // ตรวจสอบ/สร้าง DB connection

app.use('/api/auth', authRoutes);
app.use('/api/users', usersRoutes);
app.use('/api/projects', projectsRoutes);

const PORT = process.env.PORT || 4000;
app.listen(PORT, () => {
  console.log(`Backend running on http://localhost:${PORT}`);
});</textarea>
    <div class="controls">
      <button onclick="copyText('file-backend-server')">Copy</button>
      <span id="ok-file-backend-server"></span>
    </div>
  </div>

  <div class="file">
    <span class="fname">backend/db.js</span>
    <textarea id="file-backend-db">// backend/db.js
const sqlite3 = require('sqlite3').verbose();
const path = require('path');
const dbFile = path.join(__dirname, 'data.db');
let db;

function initDb() {
  db = new sqlite3.Database(dbFile, (err) => {
    if (err) {
      console.error('Cannot open DB', err);
    } else {
      console.log('Connected to SQLite DB:', dbFile);
    }
  });
}

function getDb() {
  if (!db) {
    initDb();
  }
  return db;
}

module.exports = { initDb, getDb };</textarea>
    <div class="controls">
      <button onclick="copyText('file-backend-db')">Copy</button>
      <span id="ok-file-backend-db"></span>
    </div>
  </div>

  <div class="file">
    <span class="fname">backend/routes/auth.js</span>
    <textarea id="file-backend-routes-auth">// backend/routes/auth.js
const express = require('express');
const bcrypt = require('bcrypt');
const jwt = require('jsonwebtoken');
const { getDb } = require('../db');
const router = express.Router();

const JWT_SECRET = process.env.JWT_SECRET || 'dev_secret';

// ลงทะเบียน (สำหรับทดสอบ) - ใน production อาจจำกัดเฉพาะ admin เท่านั้น
router.post('/register', async (req, res) => {
  const { username, password, role, unit } = req.body;
  if (!username || !password || !role) return res.status(400).json({ error: 'missing fields' });
  const db = getDb();
  const hash = await bcrypt.hash(password, 10);
  db.run(
    'INSERT INTO users (username, password_hash, role, unit, created_at) VALUES (?, ?, ?, ?, datetime("now"))',
    [username, hash, role, unit || null],
    function (err) {
      if (err) return res.status(500).json({ error: err.message });
      res.json({ id: this.lastID, username, role, unit });
    }
  );
});

// เข้าสู่ระบบ
router.post('/login', (req, res) => {
  const { username, password } = req.body;
  const db = getDb();
  db.get('SELECT * FROM users WHERE username = ?', [username], async (err, user) => {
    if (err) return res.status(500).json({ error: err.message });
    if (!user) return res.status(401).json({ error: 'invalid credentials' });
    const ok = await bcrypt.compare(password, user.password_hash);
    if (!ok) return res.status(401).json({ error: 'invalid credentials' });
    const payload = { id: user.id, username: user.username, role: user.role, unit: user.unit };
    const token = jwt.sign(payload, JWT_SECRET, { expiresIn: '8h' });
    res.json({ token, user: payload });
  });
});

module.exports = router;</textarea>
    <div class="controls">
      <button onclick="copyText('file-backend-routes-auth')">Copy</button>
      <span id="ok-file-backend-routes-auth"></span>
    </div>
  </div>

  <div class="file">
    <span class="fname">backend/routes/users.js</span>
    <textarea id="file-backend-routes-users">// backend/routes/users.js
const express = require('express');
const { getDb } = require('../db');
const router = express.Router();
const bcrypt = require('bcrypt');
const jwt = require('jsonwebtoken');
const JWT_SECRET = process.env.JWT_SECRET || 'dev_secret';

// middleware ตรวจ JWT และแนบ user
function authMiddleware(req, res, next) {
  const auth = req.headers.authorization;
  if (!auth) return res.status(401).json({ error: 'no token' });
  const token = auth.split(' ')[1];
  try {
    const payload = jwt.verify(token, JWT_SECRET);
    req.user = payload;
    next();
  } catch (e) {
    res.status(401).json({ error: 'invalid token' });
  }
}

// ดึงรายชื่อผู้ใช้ (เฉพาะผู้ควบคุมระบบเท่านั้น)
router.get('/', authMiddleware, (req, res) => {
  if (req.user.role !== 'admin') return res.status(403).json({ error: 'forbidden' });
  const db = getDb();
  db.all('SELECT id, username, role, unit, created_at FROM users', [], (err, rows) => {
    if (err) return res.status(500).json({ error: err.message });
    res.json(rows);
  });
});

// แก้ไขรหัสผ่าน
router.put('/password', authMiddleware, async (req, res) => {
  const { userId, newPassword } = req.body;
  if (req.user.role !== 'admin' && req.user.id !== userId) {
    return res.status(403).json({ error: 'forbidden' });
  }
  const hash = await bcrypt.hash(newPassword, 10);
  const db = getDb();
  db.run('UPDATE users SET password_hash = ? WHERE id = ?', [hash, userId], function (err) {
    if (err) return res.status(500).json({ error: err.message });
    res.json({ success: true });
  });
});

// เพิ่ม/ลบ ผู้ใช้ (admin)
router.post('/', authMiddleware, async (req, res) => {
  if (req.user.role !== 'admin') return res.status(403).json({ error: 'forbidden' });
  const { username, password, role, unit } = req.body;
  const db = getDb();
  const hash = await bcrypt.hash(password, 10);
  db.run(
    'INSERT INTO users (username, password_hash, role, unit, created_at) VALUES (?, ?, ?, ?, datetime("now"))',
    [username, hash, role, unit || null],
    function (err) {
      if (err) return res.status(500).json({ error: err.message });
      res.json({ id: this.lastID, username, role, unit });
    }
  );
});

router.delete('/:id', authMiddleware, (req, res) => {
  if (req.user.role !== 'admin') return res.status(403).json({ error: 'forbidden' });
  const db = getDb();
  db.run('DELETE FROM users WHERE id = ?', [req.params.id], function (err) {
    if (err) return res.status(500).json({ error: err.message });
    res.json({ success: true });
  });
});

module.exports = router;</textarea>
    <div class="controls">
      <button onclick="copyText('file-backend-routes-users')">Copy</button>
      <span id="ok-file-backend-routes-users"></span>
    </div>
  </div>

  <div class="file">
    <span class="fname">backend/routes/projects.js</span>
    <textarea id="file-backend-routes-projects">// backend/routes/projects.js
const express = require('express');
const { getDb } = require('../db');
const router = express.Router();
const jwt = require('jsonwebtoken');
const JWT_SECRET = process.env.JWT_SECRET || 'dev_secret';

function authMiddleware(req, res, next) {
  const auth = req.headers.authorization;
  if (!auth) return res.status(401).json({ error: 'no token' });
  const token = auth.split(' ')[1];
  try {
    const payload = jwt.verify(token, JWT_SECRET);
    req.user = payload;
    next();
  } catch (e) {
    res.status(401).json({ error: 'invalid token' });
  }
}

// สถานะที่ใช้ในระบบ:
// proposed (เสนอกิจกรรม), approved (อนุมัติกิจกรรม),
// in_progress (ดำเนินกิจกรรม), returned (รอแก้ไข),
// request_withdrawal (ขอตั้งเบิก), proposed_to_manager (เสนอผู้บริหาร),
// approved_withdrawal (อนุมัติเบิก), paid (จ่ายเงินเสร็จสิ้น)

router.post('/', authMiddleware, (req, res) => {
  const { title, description, unit } = req.body;
  const db = getDb();
  const status = 'proposed';
  db.run(
    'INSERT INTO projects (title, description, unit, status, created_by, created_at) VALUES (?, ?, ?, ?, ?, datetime(\"now\"))',
    [title, description, unit || req.user.unit, status, req.user.id],
    function (err) {
      if (err) return res.status(500).json({ error: err.message });
      const projectId = this.lastID;
      // บันทึกประวัติสถานะ
      db.run(
        'INSERT INTO status_history (project_id, status, changed_by, changed_at, note) VALUES (?, ?, ?, datetime(\"now\"), ?)',
        [projectId, status, req.user.id, 'created'],
        function () {
          // แจ้งเตือนผู้เกี่ยวข้อง (เจ้าหน้าที่)
          // สำหรับต้นแบบ เราเพิ่ม notification ให้ admin/เจ้าหน้าที่ทั้งหมด
          db.run(
            'INSERT INTO notifications (user_id, project_id, message, read, created_at) SELECT id, ?, ?, 0, datetime(\"now\") FROM users WHERE role != \"user\"',
            [projectId, `โครงการใหม่ถูกสร้าง: ${title}`]
          );
          res.json({ id: projectId, title, status });
        }
      );
    }
  );
});

// ดึงรายการโครงการ — ผู้ใช้เห็นของหน่วยงานตัวเองเท่านั้น ยกเว้นเจ้าหน้าที่/ผู้ควบคุมระบบ (role != 'user')
router.get('/', authMiddleware, (req, res) => {
  const db = getDb();
  if (req.user.role === 'user') {
    db.all('SELECT * FROM projects WHERE unit = ?', [req.user.unit], (err, rows) => {
      if (err) return res.status(500).json({ error: err.message });
      res.json(rows);
    });
  } else {
    db.all('SELECT * FROM projects', [], (err, rows) => {
      if (err) return res.status(500).json({ error: err.message });
      res.json(rows);
    });
  }
});

// ดูรายละเอียดโครงการ รวม timeline
router.get('/:id', authMiddleware, (req, res) => {
  const db = getDb();
  const id = req.params.id;
  db.get('SELECT * FROM projects WHERE id = ?', [id], (err, project) => {
    if (err) return res.status(500).json({ error: err.message });
    if (!project) return res.status(404).json({ error: 'not found' });
    // ตรวจสิทธิ์: ถ้า user ต้องเป็นของหน่วยงานเดียวกันหรือไม่ใช่ user
    if (req.user.role === 'user' && project.unit !== req.user.unit) {
      return res.status(403).json({ error: 'forbidden' });
    }
    db.all('SELECT * FROM status_history WHERE project_id = ? ORDER BY changed_at', [id], (err2, history) => {
      if (err2) return res.status(500).json({ error: err2.message });
      res.json({ project, history });
    });
  });
});

// แก้ไขโครงการ (สร้างใหม่ หรือหลังถูกส่งคืน สามารถแก้ไข)
router.put('/:id', authMiddleware, (req, res) => {
  const id = req.params.id;
  const { title, description } = req.body;
  const db = getDb();
  // ตรวจสิทธิ์ผู้แก้ไข: ผู้ใช้ตามหน่วยงานของโครงการ หรือเจ้าหน้าที่
  db.get('SELECT * FROM projects WHERE id = ?', [id], (err, project) => {
    if (err) return res.status(500).json({ error: err.message });
    if (!project) return res.status(404).json({ error: 'not found' });
    if (req.user.role === 'user' && project.unit !== req.user.unit) return res.status(403).json({ error: 'forbidden' });
    db.run('UPDATE projects SET title = ?, description = ? WHERE id = ?', [title, description, id], function (err2) {
      if (err2) return res.status(500).json({ error: err2.message });
      // เพิ่ม history ว่าแก้ไข
      db.run('INSERT INTO status_history (project_id, status, changed_by, changed_at, note) VALUES (?, ?, ?, datetime(\"now\"), ?)', [id, project.status, req.user.id, 'edit'], () => {
        res.json({ success: true });
      });
    });
  });
});

// เปลี่ยนสถานะ (เจ้าหน้าที่มีปุ่มเปลี่ยนลำดับตาม workflow)
// body: { status: "approved" , note: "..." }
router.post('/:id/change-status', authMiddleware, (req, res) => {
  const id = req.params.id;
  const { status, note } = req.body;
  const db = getDb();
  db.get('SELECT * FROM projects WHERE id = ?', [id], (err, project) => {
    if (err) return res.status(500).json({ error: err.message });
    if (!project) return res.status(404).json({ error: 'not found' });

    // ตรวจสิทธิ์: ผู้ใช้ (role='user') สามารถทำบางอย่าง เช่น "request_withdrawal" (ขอเบิก) และแก้ไขจนเสร็จ
    // เจ้าหน้าที่ (role != 'user') สามารถกดลำดับถัดไป เช่น approve, propose_to_manager, approved_withdrawal, paid, return
    const userRole = req.user.role;
    const allowed = checkStatusChangeAllowed(project.status, status, userRole);
    if (!allowed) return res.status(403).json({ error: 'ไม่อนุญาตให้เปลี่ยนสถานะนี้' });

    db.run('UPDATE projects SET status = ? WHERE id = ?', [status, id], function (err2) {
      if (err2) return res.status(500).json({ error: err2.message });
      db.run('INSERT INTO status_history (project_id, status, changed_by, changed_at, note) VALUES (?, ?, ?, datetime(\"now\"), ?)', [id, status, req.user.id, note || null]);
      // สร้าง notification ให้เจ้าของคำขอหรือผู้เกี่ยวข้อง
      if (userRole === 'user') {
        // แจ้งเจ้าหน้าที่
        db.run('INSERT INTO notifications (user_id, project_id, message, read, created_at) SELECT id, ?, ?, 0, datetime(\"now\") FROM users WHERE role != \"user\"', [id, `ผู้ใช้งาน ${req.user.username} เปลี่ยนสถานะเป็น ${status}`]);
      } else {
        // แจ้งผู้สร้างโครงการ (owner)
        db.get('SELECT created_by FROM projects WHERE id = ?', [id], (err3, r) => {
          if (!err3 && r && r.created_by) {
            db.run('INSERT INTO notifications (user_id, project_id, message, read, created_at) VALUES (?, ?, ?, 0, datetime(\"now\"))', [r.created_by, id, `เจ้าหน้าที่เปลี่ยนสถานะเป็น ${status}`]);
          }
        });
      }
      res.json({ success: true, status });
    });
  });
});

// ฟังก์ชันตรวจสิทธิ์การเปลี่ยนสถานะ (สรุป workflow แบบง่าย)
function checkStatusChangeAllowed(current, target, role) {
  const transitions = {
    proposed: ['approved', 'returned', 'in_progress'], // เจ้าหน้าที่อนุมัติ -> approved
    approved: ['in_progress'],
    in_progress: ['request_withdrawal', 'returned', 'completed'],
    request_withdrawal: ['proposed_to_manager'],
    proposed_to_manager: ['approved_withdrawal', 'returned'],
    approved_withdrawal: ['paid'],
    paid: [],
    returned: ['proposed', 'in_progress'] // ผู้ใช้แก้ไขแล้วเสนอกลับ
  };
  // ผู้ใช้ธรรมดา (role === 'user') สามารถ:
  // - เมื่อโครงการเป็น in_progress หรือ approved หรือ proposed สามารถขอเบิก (target === 'request_withdrawal')
  // - สามารถแก้ไขและ set กลับเป็น proposed (หลัง returned)
  if (role === 'user') {
    if (target === 'request_withdrawal') return ['in_progress', 'approved', 'proposed'].includes(current);
    if (current === 'returned' && target === 'proposed') return true;
    // ผู้ใช้ไม่สามารถอนุมัติหรือจ่ายเงิน
    return false;
  } else {
    // เจ้าหน้าที่: อนุญาตตาม transitions
    const allowed = transitions[current] || [];
    return allowed.includes(target);
  }
}

// ดึงการแจ้งเตือนของผู้ใช้
router.get('/:id/notifications', authMiddleware, (req, res) => {
  const db = getDb();
  db.all('SELECT * FROM notifications WHERE user_id = ? ORDER BY created_at DESC', [req.user.id], (err, rows) => {
    if (err) return res.status(500).json({ error: err.message });
    res.json(rows);
  });
});

module.exports = router;</textarea>
    <div class="controls">
      <button onclick="copyText('file-backend-routes-projects')">Copy</button>
      <span id="ok-file-backend-routes-projects"></span>
    </div>
  </div>

  <div class="file">
    <span class="fname">backend/models.sql</span>
    <textarea id="file-backend-models">-- backend/models.sql
-- สร้างตารางหลัก ๆ
PRAGMA foreign_keys = ON;

CREATE TABLE IF NOT EXISTS users (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  username TEXT UNIQUE NOT NULL,
  password_hash TEXT NOT NULL,
  role TEXT NOT NULL, -- admin, finance, plan, procurement, user
  unit TEXT,
  created_at TEXT
);

CREATE TABLE IF NOT EXISTS projects (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  title TEXT NOT NULL,
  description TEXT,
  unit TEXT,
  status TEXT,
  created_by INTEGER,
  created_at TEXT,
  FOREIGN KEY (created_by) REFERENCES users(id)
);

CREATE TABLE IF NOT EXISTS status_history (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  project_id INTEGER,
  status TEXT,
  changed_by INTEGER,
  changed_at TEXT,
  note TEXT,
  FOREIGN KEY (project_id) REFERENCES projects(id),
  FOREIGN KEY (changed_by) REFERENCES users(id)
);

CREATE TABLE IF NOT EXISTS notifications (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  user_id INTEGER,
  project_id INTEGER,
  message TEXT,
  read INTEGER DEFAULT 0,
  created_at TEXT,
  FOREIGN KEY (user_id) REFERENCES users(id),
  FOREIGN KEY (project_id) REFERENCES projects(id)
);</textarea>
    <div class="controls">
      <button onclick="copyText('file-backend-models')">Copy</button>
      <span id="ok-file-backend-models"></span>
    </div>
  </div>

  <div class="file">
    <span class="fname">backend/seed.sql</span>
    <textarea id="file-backend-seed">-- backend/seed.sql
-- ข้อมูลตัวอย่าง: ผู้ใช้งาน (user), เจ้าหน้าที่ และ admin
INSERT INTO users (username, password_hash, role, unit, created_at) VALUES ('admin', '$2b$10$e0Nw0w5aA1mE4vPp0hX2ze0WqvF3sXbQxU6rJY2ZB6yqXf5s6dZy', 'admin', NULL, datetime('now'));
-- password sample: "adminpass" (bcrypt hash above is placeholder — ให้เรียก /register เหมาะกว่า)
INSERT INTO users (username, password_hash, role, unit, created_at) VALUES ('finance1', '$2b$10$e0Nw0w5aA1mE4vPp0hX2ze0WqvF3sXbQxU6rJY2ZB6yqXf5s6dZy', 'finance', NULL, datetime('now'));
INSERT INTO users (username, password_hash, role, unit, created_at) VALUES ('plan1', '$2b$10$e0Nw0w5aA1mE4vPp0hX2ze0WqvF3sXbQxU6rJY2ZB6yqXf5s6dZy', 'plan', NULL, datetime('now'));
INSERT INTO users (username, password_hash, role, unit, created_at) VALUES ('purch1', '$2b$10$e0Nw0w5aA1mE4vPp0hX2ze0WqvF3sXbQxU6rJY2ZB6yqXf5s6dZy', 'procurement', NULL, datetime('now'));
INSERT INTO users (username, password_hash, role, unit, created_at) VALUES ('unitA_user', '$2b$10$e0Nw0w5aA1mE4vPp0hX2ze0WqvF3sXbQxU6rJY2ZB6yqXf5s6dZy', 'user', 'งานหลักสูตร', datetime('now'));

-- ตัวอย่างโครงการ
INSERT INTO projects (title, description, unit, status, created_by, created_at) VALUES ('กิจกรรมวันวิชาการ', 'จัดการประกวดผลงาน', 'งานหลักสูตร', 'proposed', 5, datetime('now'));
INSERT INTO status_history (project_id, status, changed_by, changed_at, note) VALUES (1, 'proposed', 5, datetime('now'), 'created');</textarea>
    <div class="controls">
      <button onclick="copyText('file-backend-seed')">Copy</button>
      <span id="ok-file-backend-seed"></span>
    </div>
  </div>

  <!-- frontend -->
  <div class="file">
    <span class="fname">frontend/package.json</span>
    <textarea id="file-frontend-package">{
  "name": "wr-project-frontend",
  "version": "1.0.0",
  "private": true,
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-scripts": "5.0.1"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build"
  }
}</textarea>
    <div class="controls">
      <button onclick="copyText('file-frontend-package')">Copy</button>
      <span id="ok-file-frontend-package"></span>
    </div>
  </div>

  <div class="file">
    <span class="fname">frontend/src/index.js</span>
    <textarea id="file-frontend-index">import React from 'react';
import { createRoot } from 'react-dom/client';
import App from './App';

const root = createRoot(document.getElementById('root'));
root.render(<App />);</textarea>
    <div class="controls">
      <button onclick="copyText('file-frontend-index')">Copy</button>
      <span id="ok-file-frontend-index"></span>
    </div>
  </div>

  <div class="file">
    <span class="fname">frontend/src/App.js</span>
    <textarea id="file-frontend-app">import React, { useState, useEffect } from 'react';
import Login from './pages/Login';
import Dashboard from './pages/Dashboard';

function App() {
  const [token, setToken] = useState(localStorage.getItem('token') || null);
  const [user, setUser] = useState(JSON.parse(localStorage.getItem('user')) || null);

  useEffect(() => {
    if (token && user) {
      localStorage.setItem('token', token);
      localStorage.setItem('user', JSON.stringify(user));
    } else {
      localStorage.removeItem('token');
      localStorage.removeItem('user');
    }
  }, [token, user]);

  if (!token) {
    return <Login onLogin={(t, u) => { setToken(t); setUser(u); }} />;
  }
  return <Dashboard token={token} user={user} onLogout={() => { setToken(null); setUser(null); }} />;
}

export default App;</textarea>
    <div class="controls">
      <button onclick="copyText('file-frontend-app')">Copy</button>
      <span id="ok-file-frontend-app"></span>
    </div>
  </div>

  <div class="file">
    <span class="fname">frontend/src/api.js</span>
    <textarea id="file-frontend-api">// helper สำหรับเรียก API
const API_BASE = process.env.REACT_APP_API_BASE || 'http://localhost:4000/api';

export async function apiFetch(path, token, opts = {}) {
  const headers = opts.headers || {};
  if (token) headers['Authorization'] = `Bearer ${token}`;
  headers['Content-Type'] = 'application/json';
  const res = await fetch(`${API_BASE}${path}`, { ...opts, headers });
  const data = await res.json().catch(() => ({}));
  if (!res.ok) throw data;
  return data;
}</textarea>
    <div class="controls">
      <button onclick="copyText('file-frontend-api')">Copy</button>
      <span id="ok-file-frontend-api"></span>
    </div>
  </div>

  <div class="file">
    <span class="fname">frontend/src/pages/Login.js</span>
    <textarea id="file-frontend-login">import React, { useState } from 'react';
import { apiFetch } from '../api';

export default function Login({ onLogin }) {
  const [username, setUsername] = useState('');
  const [password, setPassword] = useState('');

  async function submit(e) {
    e.preventDefault();
    try {
      const data = await apiFetch('/auth/login', null, {
        method: 'POST',
        body: JSON.stringify({ username, password })
      });
      onLogin(data.token, data.user);
    } catch (err) {
      alert('Login failed: ' + (err.error || JSON.stringify(err)));
    }
  }

  return (
    <div style={{ padding: 20 }}>
      <h2>เข้าสู่ระบบ</h2>
      <form onSubmit={submit}>
        <div>
          <label>ผู้ใช้</label><br />
          <input value={username} onChange={e => setUsername(e.target.value)} />
        </div>
        <div>
          <label>รหัสผ่าน</label><br />
          <input type="password" value={password} onChange={e => setPassword(e.target.value)} />
        </div>
        <button type="submit">เข้าสู่ระบบ</button>
      </form>
    </div>
  );
}</textarea>
    <div class="controls">
      <button onclick="copyText('file-frontend-login')">Copy</button>
      <span id="ok-file-frontend-login"></span>
    </div>
  </div>

  <div class="file">
    <span class="fname">frontend/src/pages/Dashboard.js</span>
    <textarea id="file-frontend-dashboard">import React, { useEffect, useState } from 'react';
import { apiFetch } from '../api';
import ProjectForm from '../components/ProjectForm';
import ProjectList from '../components/ProjectList';

export default function Dashboard({ token, user, onLogout }) {
  const [projects, setProjects] = useState([]);
  const [notifications, setNotifications] = useState([]);

  async function load() {
    try {
      const ps = await apiFetch('/projects', token);
      setProjects(ps);
      // ดึง notification แบบง่าย (API endpoint notifications อยู่ใน projects/:id/notifications) — ในตัวอย่างนี้จะไม่ดึงทั้งหมด
    } catch (e) {
      console.error(e);
    }
  }

  useEffect(() => { load(); }, []);

  return (
    <div style={{ padding: 20 }}>
      <div style={{ display:'flex', justifyContent:'space-between' }}>
        <h2>Dashboard — ต้อนรับ {user.username} ({user.role})</h2>
        <div>
          <button onClick={onLogout}>Logout</button>
        </div>
      </div>

      <ProjectForm token={token} user={user} onCreated={() => load()} />
      <hr />
      <ProjectList token={token} user={user} projects={projects} onUpdated={() => load()} />
    </div>
  );
}</textarea>
    <div class="controls">
      <button onclick="copyText('file-frontend-dashboard')">Copy</button>
      <span id="ok-file-frontend-dashboard"></span>
    </div>
  </div>

  <div class="file">
    <span class="fname">frontend/src/components/ProjectForm.js</span>
    <textarea id="file-frontend-projectform">import React, { useState } from 'react';
import { apiFetch } from '../api';

export default function ProjectForm({ token, user, onCreated }) {
  const [title, setTitle] = useState('');
  const [description, setDescription] = useState('');
  const [unit, setUnit] = useState(user.unit || '');

  async function submit(e) {
    e.preventDefault();
    try {
      await apiFetch('/projects', token, { method: 'POST', body: JSON.stringify({ title, description, unit }) });
      setTitle(''); setDescription('');
      onCreated();
    } catch (err) {
      alert('Error: ' + (err.error || JSON.stringify(err)));
    }
  }

  return (
    <div>
      <h3>เสนอ/เพิ่มกิจกรรม</h3>
      <form onSubmit={submit}>
        <div>
          <input placeholder="ชื่อโครงการ" value={title} onChange={e=>setTitle(e.target.value)} required />
        </div>
        <div>
          <textarea placeholder="รายละเอียด" value={description} onChange={e=>setDescription(e.target.value)} />
        </div>
        <div>
          <input placeholder="หน่วยงาน" value={unit} onChange={e=>setUnit(e.target.value)} required />
        </div>
        <button type="submit">สร้างโครงการ</button>
      </form>
    </div>
  );
}</textarea>
    <div class="controls">
      <button onclick="copyText('file-frontend-projectform')">Copy</button>
      <span id="ok-file-frontend-projectform"></span>
    </div>
  </div>

  <div class="file">
    <span class="fname">frontend/src/components/ProjectList.js</span>
    <textarea id="file-frontend-projectlist">import React, { useState } from 'react';
import { apiFetch } from '../api';
import Timeline from './Timeline';

export default function ProjectList({ token, user, projects, onUpdated }) {
  const [selected, setSelected] = useState(null);

  async function changeStatus(id, status) {
    try {
      await apiFetch(`/projects/${id}/change-status`, token, { method: 'POST', body: JSON.stringify({ status }) });
      onUpdated();
    } catch (err) {
      alert('ไม่สามารถเปลี่ยนสถานะ: ' + (err.error || JSON.stringify(err)));
    }
  }

  return (
    <div>
      <h3>รายการโครงการ</h3>
      <ul>
        {projects.map(p => (
          <li key={p.id} style={{ marginBottom: 12 }}>
            <strong>{p.title}</strong> — <em>{p.unit}</em> — สถานะ: {p.status}
            <div>
              <button onClick={() => setSelected(p.id)}>ดู</button>
              {/* ปุ่มที่แสดงตาม role และสถานะ (ตัวอย่าง) */}
              {user.role !== 'user' && p.status === 'proposed' && <button onClick={() => changeStatus(p.id, 'approved')}>อนุมัติกิจกรรม</button>}
              {(user.role === 'user' || user.role !== 'user') && ['in_progress','approved','proposed'].includes(p.status) && <button onClick={() => changeStatus(p.id, 'request_withdrawal')}>ขอเบิก</button>}
              {user.role !== 'user' && p.status === 'request_withdrawal' && <button onClick={() => changeStatus(p.id, 'proposed_to_manager')}>เสนอผู้บริหาร</button>}
              {user.role !== 'user' && p.status === 'proposed_to_manager' && <button onClick={() => changeStatus(p.id, 'approved_withdrawal')}>อนุมัติเบิก</button>}
              {user.role !== 'user' && p.status === 'approved_withdrawal' && <button onClick={() => changeStatus(p.id, 'paid')}>จ่ายเงินเสร็จสิ้น</button>}
              {user.role !== 'user' && p.status !== 'returned' && <button onClick={() => changeStatus(p.id, 'returned')}>ส่งเอกสารคืน (รอแก้ไข)</button>}
            </div>
            {selected === p.id && <Timeline token={token} projectId={p.id} />}
          </li>
        ))}
      </ul>
    </div>
  );
}</textarea>
    <div class="controls">
      <button onclick="copyText('file-frontend-projectlist')">Copy</button>
      <span id="ok-file-frontend-projectlist"></span>
    </div>
  </div>

  <div class="file">
    <span class="fname">frontend/src/components/Timeline.js</span>
    <textarea id="file-frontend-timeline">import React, { useEffect, useState } from 'react';
import { apiFetch } from '../api';

export default function Timeline({ token, projectId }) {
  const [data, setData] = useState(null);
  useEffect(() => {
    apiFetch(`/projects/${projectId}`, token).then(d => setData(d)).catch(e => console.error(e));
  }, [projectId, token]);
  if (!data) return <div>Loading...</div>;
  return (
    <div style={{ marginTop: 8 }}>
      <h4>รายละเอียด</h4>
      <div>{data.project.description}</div>
      <h4>ประวัติสถานะ</h4>
      <ul>
        {data.history.map(h => (
          <li key={h.id}>{h.changed_at} — {h.status} — โดย user_id:{h.changed_by} {h.note ? ` — ${h.note}` : ''}</li>
        ))}
      </ul>
    </div>
  );
}</textarea>
    <div class="controls">
      <button onclick="copyText('file-frontend-timeline')">Copy</button>
      <span id="ok-file-frontend-timeline"></span>
    </div>
  </div>

  <div class="block hint">
    <strong>วิธีใช้งานสั้น ๆ</strong>
    <ol>
      <li>Clone repo ที่คุณสร้างไว้: <code class="small">git clone git@github.com:pojsawee/rajadhivas-school-projects.git</code> หรือใช้ HTTPS ตามที่คุณตั้งค่า</li>
      <li>สร้างโฟลเดอร์ backend/ และ frontend/ ตามโครงสร้าง แล้วคัดลอกเนื้อหาไฟล์จากช่องด้านบนไปวางเป็นไฟล์จริง (ไฟล์บางไฟล์อยู่ใน subfolders เช่น frontend/src/... , backend/routes/...)</li>
      <li>บนเครื่อง: cd ไปที่ repo แล้วรัน:
        <pre class="small">git add .
git commit -m "Initial scaffold for activity/project workflow"
git push origin main</pre>
      </li>
      <li>จากนั้นติดตั้ง dependencies:
        <pre class="small">cd backend && npm install
cd ../frontend && npm install</pre>
      </li>
      <li>สร้างฐานข้อมูลตัวอย่าง (บนเครื่องที่มี sqlite3):
        <pre class="small">cd backend
sqlite3 data.db &lt; models.sql
sqlite3 data.db &lt; seed.sql</pre>
      </li>
      <li>ตั้งค่า environment (backend/.env) เช่น:
        <pre class="small">JWT_SECRET=your_jwt_secret
PORT=4000</pre>
      </li>
      <li>รัน backend และ frontend:
        <pre class="small"># ใน terminal แยกสองหน้า
cd backend && npm start
cd frontend && npm start</pre>
      </li>
    </ol>
  </div>

  <script>
    function copyText(id) {
      const ta = document.getElementById(id);
      ta.select();
      try {
        document.execCommand('copy');
        const ok = document.getElementById('ok-' + id);
        if (ok) {
          ok.textContent = 'Copied ✓';
          ok.className = 'copy-ok';
          setTimeout(() => { ok.textContent = ''; ok.className = ''; }, 2200);
        }
      } catch (e) {
        alert('Copy failed. Select the text manually and copy (Ctrl/Cmd+C).');
      }
      // remove selection
      window.getSelection().removeAllRanges();
    }
  </script>
</body>
</html># rajadhivas-school-projects
