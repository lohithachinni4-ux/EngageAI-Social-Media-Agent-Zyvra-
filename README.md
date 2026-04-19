# EngageAI-Social-Media-Agent-Zyvra-
AI-powered social media engagement agent for generating captions, replies, and analyzing user engagement.
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Zyvra - Social Media Engagement Agent</title>

<!-- Chart.js -->
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
body {
  margin: 0;
  font-family: Arial;
}
body {
  margin: 0;
  font-family: Arial;
}

/* SPLASH */
#splash {
  height: 100vh;
  background: #0a0f2c;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  color: white;
}

.logo {
  width: 100px;
  margin-bottom: 15px;
}

.welcome-btn {
  padding: 12px 40px;
  background: linear-gradient(to right, #8e2de2, #c471ed);
  color: white;
  border: none;
  border-radius: 5px;
}

/* LOGIN */
#login {
  display: none;
  height: 100vh;
  justify-content: center;
  align-items: center;
  background: #f2f2f2;
}

.login-container {
  background: white;
  padding: 20px;
  width: 300px;
  border-radius: 8px;
}

/* DASHBOARD FIX */
#dashboard {
  display: none;
  background: #f5f5f5;
  min-height: 100vh;
  display: flex;
  justify-content: center;
}

/* MAIN CONTENT WRAPPER */
.dashboard-container {
  width: 100%;
  max-width: 1000px;   /* 🔥 prevents stretching */
  padding: 20px;
}

/* CARDS */
.cards {
  display: flex;
  gap: 15px;
  margin-bottom: 20px;
  flex-wrap: wrap;
}

.card {
  flex: 1;
  min-width: 150px;
  background: white;
  padding: 15px;
  border-radius: 10px;
  text-align: center;
  font-weight: bold;
}

/* SECTIONS */
.section {
  background: white;
  padding: 15px;
  margin-top: 15px;
  border-radius: 10px;
}

/* INPUTS */
textarea {
  width: 100%;
  height: 70px;
}

button {
  padding: 8px;
  background: purple;
  color: white;
  border: none;
  margin-top: 10px;
  border-radius: 5px;
}

/* CHART FIX */
canvas {
  max-height: 300px;
}
/* SPLASH */
#splash {
  height: 100vh;
  background: #0a0f2c;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  color: white;
}

.logo {
  width: 120px;
  margin-bottom: 20px;
}

.welcome-btn {
  padding: 15px 60px;
  background: linear-gradient(to right, #8e2de2, #c471ed);
  color: white;
  border: none;
  border-radius: 5px;
}

/* LOGIN */
#login {
  display: none;
  height: 100vh;
  justify-content: center;
  align-items: center;
  background: #f2f2f2;
}

.login-container {
  background: white;
  padding: 25px;
  width: 320px;
  border-radius: 8px;
}

.input-box {
  background: #eee;
  padding: 10px;
  margin-bottom: 15px;
}

.input-box input {
  width: 100%;
  border: none;
  background: transparent;
  outline: none;
}

/* DASHBOARD */
#dashboard {
  display: none;
  padding: 20px;
  background: #f5f5f5;
}

.cards {
  display: flex;
  gap: 20px;
  margin-bottom: 20px;
}

.card {
  flex: 1;
  background: white;
  padding: 20px;
  border-radius: 10px;
  text-align: center;
  font-weight: bold;
}

.section {
  background: white;
  padding: 20px;
  margin-top: 20px;
  border-radius: 10px;
}

textarea {
  width: 100%;
  height: 80px;
}

button {
  padding: 10px;
  background: purple;
  color: white;
  border: none;
  margin-top: 10px;
}
</style>
</head>

<body>

<!-- SPLASH SCREEN -->
<div id="splash">
  <img src="assets/logo.png" class="logo">
  <h1>Zyvra</h1>
  <button class="welcome-btn">Welcome</button>
</div>

<!-- LOGIN PAGE -->
<div id="login">
  <div class="login-container">
    <h3>Login to your account</h3>

    <div class="input-box">
      <input type="text" placeholder="Email">
    </div>

    <div class="input-box">
      <input type="password" placeholder="Password">
    </div>

    <button onclick="goToDashboard()">Login</button>
  </div>
</div>

<!-- DASHBOARD -->
<div id="dashboard">

  <h2>📊 Zyvra Dashboard</h2>

  <!-- STATS -->
  <div class="cards">
    <div class="card">👍 Likes<br>12,430</div>
    <div class="card">💬 Comments<br>3,210</div>
    <div class="card">📈 Reach<br>45,000</div>
  </div>

  <!-- CHART -->
  <div class="section">
    <h3>Engagement Graph</h3>
    <canvas id="chart"></canvas>
  </div>

  <!-- CAPTION GENERATOR -->
  <div class="section">
    <h3>✍️ Caption Generator</h3>
    <textarea id="captionInput" placeholder="Enter topic..."></textarea>
    <button onclick="generateCaption()">Generate Caption</button>
    <p id="captionOutput"></p>
  </div>

  <!-- REPLY GENERATOR -->
  <div class="section">
    <h3>💬 Reply Generator</h3>
    <textarea id="replyInput" placeholder="Enter comment..."></textarea>
    <button onclick="generateReply()">Generate Reply</button>
    <p id="replyOutput"></p>
  </div>

</div>

<script>

// Splash → Login
setTimeout(() => {
  document.getElementById("splash").style.display = "none";
  document.getElementById("login").style.display = "flex";
}, 2000);

// Login → Dashboard
function goToDashboard() {
  document.getElementById("login").style.display = "none";
  document.getElementById("dashboard").style.display = "block";
  loadChart();
}

// Chart
function loadChart() {
  new Chart(document.getElementById("chart"), {
    type: 'line',
    data: {
      labels: ["Mon", "Tue", "Wed", "Thu", "Fri"],
      datasets: [{
        label: "Engagement",
        data: [10, 20, 15, 30, 25]
      }]
    }
  });
}

// Caption Generator
function generateCaption() {
  let input = document.getElementById("captionInput").value;
  document.getElementById("captionOutput").innerText =
    "🔥 " + input + " - Boost your engagement with Zyvra! #AI";
}

// Reply Generator
function generateReply() {
  document.getElementById("replyOutput").innerText =
    "Thanks for your comment! 😊 We appreciate your support!";
}

</script>

</body>
</html>
const UserSchema = new mongoose.Schema({
  username: { type: String, required: true },
  email: { type: String, unique: true },
  password: { type: String }, // Hashed with bcrypt
  googleId: { type: String },
  profileImg: String,
  socialStats: {
    totalPosts: Number,
    followers: Number,
    reach: Number
  }
});

const PostSchema = new mongoose.Schema({
  userId: { type: mongoose.Schema.Types.ObjectId, ref: 'User' },
  title: String,
  content: String, // Image URL or text
  scheduledAt: Date,
  status: { type: String, enum: ['Draft', 'Scheduled', 'Published'], default: 'Scheduled' },
  platform: String // Instagram, LinkedIn, etc.
});


// POST /api/posts/schedule
router.post('/schedule', async (req, res) => {
  const { title, date, time, imageUrl } = req.body;
  const scheduledDate = new Date(`${date}T${time}`);

  const post = await Post.create({
    userId: req.user.id,
    title,
    content: imageUrl,
    scheduledAt: scheduledDate,
    status: 'Scheduled'
  });
  res.status(201).json(post);
});
// GET /api/user/dashboard-summary
router.get('/dashboard-summary', async (req, res) => {
  const stats = await Post.aggregate([
    { $match: { userId: req.user.id } },
    { $group: { _id: null, totalPosts: { $sum: 1 }, avgEngagement: { $avg: "$engagement" } } }
  ]);
  res.json(stats[0]);
});
