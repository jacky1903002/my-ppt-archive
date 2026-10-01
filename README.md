<!-- 引入 FontAwesome 企業圖示庫 -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

<style>
  /* 全域深色企業主題設定 */
  .enterprise-body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
    color: #f8fafc;
    margin: 0;
    padding: 10px 0;
  }

  /* 登入卡片樣式 */
  .login-card {
    max-width: 420px;
    margin: 40px auto;
    background: #1e293b;
    border: 1px solid #334155;
    border-radius: 12px;
    padding: 30px;
    box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.3);
  }

  .login-card h3 {
    margin-top: 0;
    color: #38bdf8;
    font-size: 20px;
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .form-group {
    margin-bottom: 18px;
  }

  .form-group label {
    display: block;
    font-size: 14px;
    color: #94a3b8;
    margin-bottom: 6px;
  }

  .form-control {
    width: 100%;
    padding: 10px 12px;
    background: #0f172a;
    border: 1px solid #475569;
    border-radius: 6px;
    color: #f8fafc;
    font-size: 14px;
    box-sizing: border-box;
    outline: none;
    transition: border-color 0.2s;
  }

  .form-control:focus {
    border-color: #38bdf8;
  }

  .btn-primary {
    width: 100%;
    padding: 11px;
    background: #0284c7;
    color: white;
    border: none;
    border-radius: 6px;
    font-weight: 600;
    cursor: pointer;
    font-size: 15px;
    transition: background 0.2s;
  }

  .btn-primary:hover {
    background: #0369a1;
  }

  /* 登入後 Portal 介面樣式 */
  .portal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #1e293b;
    border: 1px solid #334155;
    border-radius: 10px;
    padding: 15px 20px;
    margin-bottom: 25px;
  }

  .user-badge {
    color: #38bdf8;
    font-weight: 600;
    font-size: 14px;
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .btn-danger {
    background: #ef4444;
    color: white;
    border: none;
    padding: 7px 14px;
    border-radius: 6px;
    font-size: 13px;
    cursor: pointer;
    font-weight: 500;
    transition: background 0.2s;
  }

  .btn-danger:hover {
    background: #dc2626;
  }

  /* 簡報列表卡片 */
  .section-title {
    font-size: 18px;
    font-weight: bold;
    color: #e2e8f0;
    margin-bottom: 15px;
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .doc-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
    gap: 20px;
  }

  .doc-card {
    background: #1e293b;
    border: 1px solid #334155;
    border-radius: 12px;
    padding: 20px;
    transition: transform 0.2s, border-color 0.2s;
    text-decoration: none;
    color: inherit;
    display: block;
  }

  .doc-card:hover {
    transform: translateY(-3px);
    border-color: #38bdf8;
  }

  .doc-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-bottom: 12px;
  }

  .doc-icon {
    font-size: 24px;
    color: #38bdf8;
  }

  .doc-status {
    background: rgba(16, 185, 129, 0.15);
    color: #10b981;
    font-size: 11px;
    font-weight: 600;
    padding: 3px 8px;
    border-radius: 12px;
    border: 1px solid rgba(16, 185, 129, 0.3);
  }

  .doc-title {
    font-size: 16px;
    font-weight: 600;
    color: #f1f5f9;
    margin: 0 0 8px 0;
    line-height: 1.4;
  }

  .doc-desc {
    font-size: 13px;
    color: #94a3b8;
    margin: 0;
    line-height: 1.5;
  }
</style>

<div class="enterprise-body">

  <!-- 1. 未登入：企業級登入視窗 -->
  <div id="login-section" class="login-card">
    <h3><i class="fa-solid fa-shield-halved"></i> Enterprise Portal Authentication</h3>
    <p style="font-size: 13px; color: #94a3b8; margin-bottom: 20px;">Restricted Access: Please sign in with your corporate credentials to access confidential presentation archives.</p>

    <div class="form-group">
      <label><i class="fa-solid fa-envelope"></i> Email Address</label>
      <input type="email" id="email" class="form-control" placeholder="name@company.com">
    </div>

    <div class="form-group">
      <label><i class="fa-solid fa-key"></i> Password</label>
      <div style="position: relative; display: flex; align-items: center;">
        <input type="password" id="password" class="form-control" placeholder="••••••••" style="padding-right: 40px;">
        <button type="button" id="toggle-password-btn" style="position: absolute; right: 10px; background: none; border: none; cursor: pointer; color: #94a3b8; font-size: 14px;" title="Toggle Password Visibility">
          <i class="fa-solid fa-eye"></i>
        </button>
      </div>
    </div>

    <button type="button" id="login-btn" class="btn-primary">
      <i class="fa-solid fa-right-to-bracket"></i> Sign In to Portal
    </button>
    <p id="error-msg" style="color: #f87171; font-size: 13px; margin-top: 12px; display: none;"></p>
  </div>

  <!-- 2. 登入後：受保護的企業儀表板 (Dashboard) -->
  <div id="protected-content" style="display: none !important;">
    <div class="portal-header">
      <div class="user-badge">
        <i class="fa-solid fa-circle-user" style="font-size: 18px;"></i>
        <span id="user-info">Signed in</span>
      </div>
      <button type="button" id="logout-btn" class="btn-danger">
        <i class="fa-solid fa-right-from-bracket"></i> Sign Out
      </button>
    </div>

    <div class="section-title">
      <i class="fa-solid fa-folder-closed" style="color: #38bdf8;"></i> Corporate Executive Presentations
    </div>

    <!-- 卡片式檔案清單 -->
    <div class="doc-grid">

      <!-- 簡報 1：AMAT ENP 報告 -->
      <a href="./viewer.html?file=ENP_Expansion_Feedback%202026.pdf&title=AMAT%20ENP%20Pre-treatment%20%26%20Line%20Expansion%202026" class="doc-card">
        <div class="doc-header">
          <i class="fa-solid fa-file-powerpoint doc-icon"></i>
          <span class="doc-status">CONFIDENTIAL</span>
        </div>
        <div class="doc-title">AMAT ENP Pre-treatment & Line Expansion 2026</div>
        <p class="doc-desc">Capacity assessment, automated pre-treatment integration, and output forecasting.</p>
      </a>

      <!-- 簡報 2：Operation Meeting MFG 0922 -->
      <a href="./viewer.html?file=operation%20meeting%20mfg%200922.pdf&title=Operation%20Meeting%20MFG%20(2026-09-22)" class="doc-card">
        <div class="doc-header">
          <i class="fa-solid fa-file-powerpoint doc-icon"></i>
          <span class="doc-status">CONFIDENTIAL</span>
        </div>
        <div class="doc-title">Operation Meeting MFG (2026-09-22)</div>
        <p class="doc-desc">Manufacturing operation review, capacity metrics, and action items.</p>
      </a>
<!-- 簡報 3：Training Center 2026 -->
      <a href="./viewer.html?file=Training%20Center%202026.pdf&title=Training%20Center%202026" class="doc-card">
        <div class="doc-header">
          <i class="fa-solid fa-file-powerpoint doc-icon"></i>
          <span class="doc-status">CONFIDENTIAL</span>
        </div>
        <div class="doc-title">Training Center 2026</div>
        <p class="doc-desc">Training Center is a modern facility dedicated to professional development, skill enhancement, and expert-led learning tailored for individual and team growth.</p>
      </a>

    </div>
  </div>

</div>

<!-- 3. Firebase 驗證腳本 -->
<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getAuth, signInWithEmailAndPassword, signOut, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";

  const firebaseConfig = {
    apiKey: "AIzaSyAxz1tGF3ExWTH-KQKUq5IRvqEr6iwuVmQ",
    authDomain: "my-ppt-auth.firebaseapp.com",
    databaseURL: "https://my-ppt-auth-default-rtdb.firebaseio.com",
    projectId: "my-ppt-auth",
    storageBucket: "my-ppt-auth.firebasestorage.app",
    messagingSenderId: "986466126958",
    appId: "1:986466126958:web:31f4e24db18f18e347ea7f",
    measurementId: "G-51PC8DCJDM"
  };

  const app = initializeApp(firebaseConfig);
  const auth = getAuth(app);

  const loginSection = document.getElementById('login-section');
  const protectedContent = document.getElementById('protected-content');
  const userInfo = document.getElementById('user-info');
  const errorMsg = document.getElementById('error-msg');
  const passwordInput = document.getElementById('password');
  const togglePasswordBtn = document.getElementById('toggle-password-btn');

  // 切換眼睛/閉眼圖示
  togglePasswordBtn.addEventListener('click', () => {
    const isPassword = passwordInput.type === 'password';
    passwordInput.type = isPassword ? 'text' : 'password';
    togglePasswordBtn.innerHTML = isPassword ? '<i class="fa-solid fa-eye-slash"></i>' : '<i class="fa-solid fa-eye"></i>';
  });

  // 監聽 Firebase 登入狀態
  onAuthStateChanged(auth, (user) => {
    if (user) {
      loginSection.style.display = 'none';
      protectedContent.style.setProperty('display', 'block', 'important');
      userInfo.innerText = 'Authenticated User: ' + user.email;
    } else {
      loginSection.style.display = 'block';
      protectedContent.style.setProperty('display', 'none', 'important');
    }
  });

  // 點擊登入
  document.getElementById('login-btn').addEventListener('click', () => {
    const email = document.getElementById('email').value;
    const password = passwordInput.value;
    errorMsg.style.display = 'none';

    signInWithEmailAndPassword(auth, email, password)
      .catch((error) => {
        console.error("Firebase Login Error:", error);
        errorMsg.innerText = "Authentication Failed: Please check your corporate email and password.";
        errorMsg.style.display = 'block';
      });
  });

  // 點擊登出
  document.getElementById('logout-btn').addEventListener('click', () => {
    signOut(auth);
  });
</script>
