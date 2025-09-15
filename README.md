<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Login | Kantamxs</title>
<style>
* { margin: 0; padding: 0; box-sizing: border-box; }

body {
  font-family: 'Comic Sans MS', cursive, sans-serif;
  background: url('https://i.postimg.cc/ZKppQytj/20250806-180912.jpg') no-repeat center center fixed;
  background-size: cover;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.center-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  max-width: 500px;
}

.login-box {
  background: rgba(255, 240, 245, 0.6);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  padding: 30px;
  border-radius: 20px;
  text-align: center;
  width: 100%;
  box-shadow: 0 0 20px rgba(0,0,0,0.1);
  transition: transform 0.8s ease, opacity 0.8s ease;
}

h2 { color: #ff69b4; margin-bottom: 20px; }

input[type="text"], input[type="password"] {
  padding: 17px;
  margin: 15px 0;
  width: 100%;
  border: 2px solid #ffb6c1;
  border-radius: 10px;
  font-size: 16px;
  outline: none;
}

button {
  padding: 15px 25px;
  background-color: #ff69b4;
  color: white;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  font-size: 16px;
}

/* กล่องล็อกอิน/ข้อความเลื่อนออก */
.login-box.slide-out { transform: translateX(-150%); opacity: 0; }
#bottomRightBox.hidden-bottom { opacity: 0; pointer-events: none; transition: opacity 0.8s ease; }

/* กล่องรูปภาพ */
#imageContainer {
  display: none;
  opacity: 0;
  transform: translateX(150%);
  transition: transform 0.8s ease, opacity 0.8s ease;
}

#imageContainer.show { opacity: 1; transform: translateX(0); }

.image-container img {
  max-width: 100%;
  border-radius: 15px;
  margin-top: 20px;
  box-shadow: 0 0 15px rgba(0,0,0,0.2);
}

/* กล่องแจ้งเตือน */
#errorBox {
  position: fixed; top: 50%; left: 50%;
  transform: translate(-50%, -50%);
  background: white;
  padding: 20px 30px;
  border-radius: 15px;
  box-shadow: 0 0 20px rgba(0,0,0,0.3);
  text-align: center;
  z-index: 9999;
}

#errorBox p { margin-bottom: 15px; color: #ff69b4; font-weight: bold; }
#errorBox button { padding: 10px 20px; background: #ff69b4; color: white; border: none; border-radius: 10px; cursor: pointer; }

#bottomRightBox {
  position: fixed; bottom: 20px; right: 20px;
  background: rgba(255, 182, 193, 0.9);
  color: white;
  padding: 15px 20px;
  border-radius: 12px;
  font-weight: bold;
  font-size: 13px;
  z-index: 10000;
}
</style>
</head>
<body id="pageBody">

<!-- กล่องล็อกอิน -->
<div class="center-container" id="loginContainer">
  <div class="login-box" id="loginForm">
    <h2>Hello everyone who entered. 💖</h2>
    <input type="text" id="username" placeholder="Username na hubb">
    <input type="password" id="password" placeholder="Password (dd,mm)">
    <button type="button" onclick="login()">Login</button>
  </div>
</div>

<!-- กล่องรูปแสดง -->
<div class="center-container" id="imageContainer">
  <div class="login-box" id="imageBox">
    <h2>Hi na hub you!! 🌸</h2>
    <div class="image-container">
      <img src="https://i.postimg.cc/FHhLwWpG/how-You-20250914-233456-0000.png" alt="My Image">
    </div>
  </div>
</div>

<!-- กล่องมุมขวาล่าง -->
<div id="bottomRightBox">ดีฮ่ะ สำหรับคนที่เข้ามาลองดูก็นี่ฮับ Username **korawit** Password **0301** 💖</div>

<!-- กล่องแจ้งเตือน -->
<div id="errorBox" class="hidden">
  <p>❌ Username หรือ Password ไม่ถูกต้อง</p>
  <button onclick="closeError()">ตกลง</button>
</div>

<script>
// ผู้ใช้
const users = [
  {
    username: 'korawit', password: '0301',
    background: 'https://i.postimg.cc/ZR3vQCC6/8b57589a-f721-4045-a41f-cdce91ef30e5.jpg',
    image: 'https://i.postimg.cc/FHhLwWpG/how-You-20250914-233456-0000.png',
    greeting: 'Hi na hub you!! 🌸'
  },
  {
    username: 'kantamxs', password: '2606',
    background: 'https://i.postimg.cc/7Pjzx1M8/1-Clearnote.jpg',
    image: 'https://i.postimg.cc/1tRJJw5X/20250915-031854-0000.png',
    greeting: 'Hi na hub JuneNae~ Kantamxs! 🌸'
  }
];

function login() {
  const usernameInput = document.getElementById('username').value.trim();
  const passwordInput = document.getElementById('password').value.trim();
  const user = users.find(u => u.username.toLowerCase() === usernameInput.toLowerCase() && u.password === passwordInput);

  if (user) {
    const loginBox = document.getElementById('loginForm');
    const bottomBox = document.getElementById('bottomRightBox');

    // เลื่อนออกพร้อมกัน
    loginBox.classList.add('slide-out');
    bottomBox.classList.add('hidden-bottom');

    setTimeout(() => {
      document.getElementById('loginContainer').style.display = 'none';

      const imageContainer = document.getElementById('imageContainer');
      imageContainer.style.display = 'flex';
      setTimeout(() => imageContainer.classList.add('show'), 50);

      // เปลี่ยนพื้นหลังและรูปตาม user
      const body = document.getElementById('pageBody');
      body.style.backgroundImage = `url('${user.background}')`;

      const imageBox = document.getElementById('imageBox');
      imageBox.querySelector('h2').textContent = user.greeting;
      imageBox.querySelector('img').src = user.image;
    }, 800);
  } else {
    document.getElementById('errorBox').classList.remove('hidden');
  }
}

function closeError() {
  document.getElementById('errorBox').classList.add('hidden');
}

// กด Enter
['username','password'].forEach(id => {
  document.getElementById(id).addEventListener('keydown', e => {
    if (e.key === 'Enter') login();
  });
});
</script>

</body>
</html>
