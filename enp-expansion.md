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
    <input type="password" id="password" placeholder="••••••••" style="width: 100%; padding: 8px; margin-top: 5px; box-sizing: border-box;">
  </div>
  <button type="button" id="login-btn" style="background-color: #0366d6; color: white; border: none; padding: 10px 15px; border-radius: 5px; cursor: pointer; width: 100%;">登入觀看</button>
  <p id="error-msg" style="color: red; margin-top: 10px; display: none;"></p>
</div>

<!-- 2. 受保護內容 (預設直接加上內聯隱藏 style="display: none;") -->
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

<!-- 3. Firebase 腳本 (記得更換金鑰) -->
<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getAuth, signInWithEmailAndPassword, signOut, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";

  // 請記得替換為您在 Firebase Console 取得的金鑰設定
  const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT_ID.appspot.com",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
  };

  const app = initializeApp(firebaseConfig);
  const auth = getAuth(app);

  const loginSection = document.getElementById('login-section');
  const protectedContent = document.getElementById('protected-content');
  const userInfo = document.getElementById('user-info');
  const errorMsg = document.getElementById('error-msg');

  // 監聽登入狀態
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

  // 綁定登入點擊事件
  document.getElementById('login-btn').addEventListener('click', () => {
    const email = document.getElementById('email').value;
    const password = document.getElementById('password').value;
    errorMsg.style.display = 'none';

    signInWithEmailAndPassword(auth, email, password)
      .catch((error) => {
        errorMsg.innerText = "登入失敗：請檢查帳號密碼";
        errorMsg.style.display = 'block';
      });
  });

  // 綁定登出點擊事件
  document.getElementById('logout-btn').addEventListener('click', () => {
    signOut(auth);
  });
</script>
