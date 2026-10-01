# AMAT ENP Expansion & Capacity Report 2026

<!-- 1. Login Form -->
<div id="login-section" style="max-width: 400px; padding: 20px; border: 1px solid #ccc; border-radius: 8px; margin: 20px 0;">
  <h3 style="margin-top: 0;">🔒 Please sign in to view the presentation</h3>
  <div style="margin-bottom: 10px;">
    <label>Email Address:</label><br>
    <input type="email" id="email" placeholder="user@example.com" style="width: 100%; padding: 8px; margin-top: 5px; box-sizing: border-box;">
  </div>
  <div style="margin-bottom: 15px;">
    <label>Password:</label><br>
    <div style="position: relative; display: flex; align-items: center; margin-top: 5px;">
      <input type="password" id="password" placeholder="••••••••" style="width: 100%; padding: 8px 35px 8px 8px; box-sizing: border-box;">
      <button type="button" id="toggle-password-btn" style="position: absolute; right: 5px; background: none; border: none; cursor: pointer; font-size: 16px; padding: 4px;" title="Toggle Password Visibility">👁️</button>
    </div>
  </div>
  <button type="button" id="login-btn" style="background-color: #0366d6; color: white; border: none; padding: 10px 15px; border-radius: 5px; cursor: pointer; width: 100%;">Sign In</button>
  <p id="error-msg" style="color: red; margin-top: 10px; display: none;"></p>
</div>

<!-- 2. Protected Content -->
<div id="protected-content" style="display: none !important;">
  <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px; background: #f6f8fa; padding: 10px; border-radius: 5px;">
    <span id="user-info" style="color: #28a745; font-weight: bold;"></span>
    <button type="button" id="logout-btn" style="background-color: #d73a49; color: white; border: none; padding: 6px 12px; border-radius: 4px; cursor: pointer;">Sign Out</button>
  </div>

  <h2>Preview</h2>
  <iframe src="ENP_Expansion_Feedback%202026.pdf" width="100%" height="600px"></iframe>

  <h2>Key Notes</h2>
  <ul>
    <li><b>2026 Before Expansion Target</b>: Max capacity of 2,592 PCS. At 80% utilization, estimated output is 2,070 PCS/year (min).</li>
    <li><b>2026 Post-Expansion (Auto Pretreatment + 2 Tanks)</b>: Max capacity of 4,032 PCS. At 80% utilization, estimated output is 3,225 PCS/year (min).</li>
  </ul>
</div>

<!-- 3. Firebase Authentication Script -->
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

  // Toggle Password Visibility
  togglePasswordBtn.addEventListener('click', () => {
    const isPassword = passwordInput.type === 'password';
    passwordInput.type = isPassword ? 'text' : 'password';
    togglePasswordBtn.innerText = isPassword ? '🙈' : '👁️';
  });

  // Monitor Authentication State
  onAuthStateChanged(auth, (user) => {
    if (user) {
      loginSection.style.display = 'none';
      protectedContent.style.setProperty('display', 'block', 'important');
      userInfo.innerText = 'Signed in as: ' + user.email;
    } else {
      loginSection.style.display = 'block';
      protectedContent.style.setProperty('display', 'none', 'important');
    }
  });

  // Login Action
  document.getElementById('login-btn').addEventListener('click', () => {
    const email = document.getElementById('email').value;
    const password = passwordInput.value;
    errorMsg.style.display = 'none';

    signInWithEmailAndPassword(auth, email, password)
      .catch((error) => {
        console.error("Firebase Login Error:", error);
        errorMsg.innerText = "Login failed: Please verify your email and password.";
        errorMsg.style.display = 'block';
      });
  });

  // Logout Action
  document.getElementById('logout-btn').addEventListener('click', () => {
    signOut(auth);
  });
</script>
