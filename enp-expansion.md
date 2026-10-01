# AMAT ENP Expansion & Capacity Report 2026

<!-- 1. 未登入時顯示的登入表單 -->
<div id="login-section" style="max-width: 400px; padding: 20px; border: 1px solid #ccc; border-radius: 8px; margin: 20px 0;">
  <h3>🔒 請先登入以檢視簡報</h3>
  <div style="margin-bottom: 10px;">
    <label>電子郵件：</label><br>
    <input type="email" id="email" placeholder="user@example.com" style="width: 100%; padding: 8px; margin-top: 5px;">
  </div>
  <div style="margin-bottom: 15px;">
    <label>密碼：</label><br>
    <input type="password" id="password" placeholder="••••••••" style="width: 100%; padding: 8px; margin-top: 5px;">
  </div>
  <button id="login-btn" onclick="login()" style="background-color: #0366d6; color: white; border: none; padding: 10px 15px; border-radius: 5px; cursor: pointer; width: 100%;">登入觀看</button>
  <p id="error-msg" style="color: red; margin-top: 10px; display: none;"></p>
</div>

<!-- 2. 登入後才顯示的簡報內容區塊 (預設隱藏 display: none) -->
<div id="protected-content" style="display: none;">
  <div style="display: flex; justify: space-between; align-items: center; margin-bottom: 15px;">
    <span id="user-info" style="color: green; font-weight: bold;"></span>
    <button onclick="logout()" style="background-color: #d73a49; color: white; border: none; padding: 5px 10px; border-radius: 4px; cursor: pointer;">登出</button>
  </div>

  <h2>Preview</h2>
  <iframe src="ENP_Expansion_Feedback%202026.pdf" width="100%" height="600px"></iframe>

  <h2>Key Notes</h2>
  <ul>
    <li><b>2026 Before Expansion Target</b>: Max capacity of 2,592 PCS. At 80% utilization, estimated output is 2,070 PCS/year (min).</li>
    <li><b>2026 Post-Expansion (Auto Pretreatment + 2 Tanks)</b>: Max capacity of 4,032 PCS. At 80% utilization, estimated output is 3,225 PCS/year (min).</li>
  </ul>
</div>

<!-- 3. Firebase SDK 載入與驗證邏輯 -->
<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getAuth, signInWithEmailAndPassword, signOut, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";

  // 請填入您在 Firebase 步驟 2 取得的金鑰配置
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

  // 監聽登入狀態變更
  onAuthStateChanged(auth, (user) => {
    if (user) {
      document.getElementById('login-section').style.display = 'none';
      document.getElementById('protected-content').style.display = 'block';
      document.getElementById('user-info').innerText = '已登入：' + user.email;
    } else {
      document.getElementById('login-section').style.display = 'block';
      document.getElementById('protected-content').style.display = 'none';
    }
  });

  // 登入 Function
  window.login = function() {
    const email = document.getElementById('email').value;
    const password = document.getElementById('password').value;
    const errorMsg = document.getElementById('error-msg');

    errorMsg.style.display = 'none';

    signInWithEmailAndPassword(auth, email, password)
      .catch((error) => {
        errorMsg.innerText = "登入失敗：請檢查帳號密碼是否正確";
        errorMsg.style.display = 'block';
      });
  };

  // 登出 Function
  window.logout = function() {
    signOut(auth);
  };
</script>

## Preview
<iframe src="ENP_Expansion_Feedback%202026.pdf" width="100%" height="600px"></iframe>

## Key Notes
* **2026 Before Expansion Target**: Max capacity of 2,592 PCS. At 80% utilization, estimated output is 2,070 PCS/year (min).
* **2026 Post-Expansion (Auto Pretreatment + 2 Tanks)**: Max capacity of 4,032 PCS. At 80% utilization, estimated output is 3,225 PCS/year (min).
