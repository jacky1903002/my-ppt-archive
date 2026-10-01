# AMAT ENP Expansion & Capacity Report 2026

<!-- 1. 未登入表單 -->
<div id="login-section" style="max-width: 400px; padding: 20px; border: 1px solid #ccc; border-radius: 8px; margin: 20px 0;">
  <h3 style="margin-top: 0;">🔒 請先登入以檢視簡報</h3>
  <div style="margin-bottom: 10px;">
    <label>電子郵件：</label><br>
    <input type="email" id="email" placeholder="user@example.com" style="width: 100%; padding: 8px; margin-top: 5px; box-sizing: border-box;">
  </div>
  <div style="margin-bottom: 15px;">
    <label>密碼：</label><br>
    <div style="position: relative; display: flex; align-items: center; margin-top: 5px;">
      <input type="password" id="password" placeholder="••••••••" style="width: 100%; padding: 8px 35px 8px 8px; box-sizing: border-box;">
      <button type="button" id="toggle-password-btn" style="position: absolute; right: 5px; background: none; border: none; cursor: pointer; font-size: 16px; padding: 4px;" title="切換顯示密碼">👁️</button>
    </div>
  </div>
  <button type="button" id="login-btn" style="background-color: #0366d6; color: white; border: none; padding: 10px 15px; border-radius: 5px; cursor: pointer; width: 100%;">登入觀看</button>
  <p id="error-msg" style="color: red; margin-top: 10px; display: none;"></p>
</div>

<!-- 2. 受保護內容 (預設直接加上內聯隱藏) -->
<div id="protected-content" style="display: none !important;">
  <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px; background: #f6f8fa; padding: 10px; border-radius: 5px;">
    <span id="user-info" style="color: #28a745; font-weight: bold;"></span>
    <button type="button" id="logout-btn" style="background-color: #d73a49; color: white; border: none; padding: 6px 12px; border-radius: 4px; cursor: pointer;">登出</button>
  </div>

  <h2>Preview</h2>
  <iframe src="ENP_Expansion_Feedback%202026.pdf" width="100%" height="600px"></iframe>

  <h2>Key Notes</h2>
  <ul>
    <li><b>2026 Before Expansion Target</b>: Max capacity of 2,592 PCS. At 80% utilization, estimated output is 2,070 PCS/year (min).</li>
    <li><b>2026 Post-Expansion (Auto Pretreatment + 2 Tanks)</b>: Max capacity of 4,032 PCS. At 80% utilization, estimated output is 3,225 PCS/year (min).</li>
  </ul>
</div>

<!-- 3. Firebase 驗證邏輯 -->
<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getAuth, signInWithEmailAndPassword, signOut, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";

  // 您的 Firebase 真實設定
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

  // 初始化 Firebase 與 Authentication
  const app = initializeApp(firebaseConfig);
  const auth = getAuth(app);

  // 抓取頁面 DOM 元素
  const loginSection = document.getElementById('login-section');
  const protectedContent = document.getElementById('protected-content');
  const userInfo = document.getElementById('user-info');
  const errorMsg = document.getElementById('error-msg');
  const passwordInput = document.getElementById('password');
  const togglePasswordBtn = document.getElementById('toggle-password-btn');

  // 1. 切換密碼顯示/隱藏功能
  togglePasswordBtn.addEventListener('click', () => {
    const isPassword = passwordInput.type === 'password';
    passwordInput.type = isPassword ? 'text' : 'password';
    togglePasswordBtn.innerText = isPassword ? '🙈' : '👁️';
  });

  // 2. 監聽 Firebase 登入狀態變更
  onAuthStateChanged(auth, (user) => {
    if (user) {
      loginSection.style.display = 'none';
      protectedContent.style.setProperty('display', 'block', 'important');
      userInfo.innerText = '已登入：' + user.email;
    } else {
      loginSection.style.display = 'block';
      protectedContent.style.setProperty('display', 'none', 'important');
    }
  });

  // 3. 執行 Firebase 登入
  document.getElementById('login-btn').addEventListener('click', () => {
    const email = document.getElementById('email').value;
    const password = passwordInput.value;
    errorMsg.style.display = 'none';

    signInWithEmailAndPassword(auth, email, password)
      .catch((error) => {
        console.error("Firebase Login Error:", error);
        errorMsg.innerText = "登入失敗：請確認帳號密碼是否正確，或此帳號是否已於 Firebase Console 建立。";
        errorMsg.style.display = 'block';
      });
  });

  // 4. 執行登出
  document.getElementById('logout-btn').addEventListener('click', () => {
    signOut(auth);
  });
</script>
