<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>GitBase - Turn GitHub Into a Database</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">

<style>
*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:'Poppins',sans-serif;
}

body{
background:#f6f8fa;
color:#24292f;
line-height:1.7;
overflow-x: hidden;
}

@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

@keyframes pulseShadow {
  0% { box-shadow: 0 0 30px rgba(46,160,67,.2); }
  50% { box-shadow: 0 0 50px rgba(46,160,67,.4); }
  100% { box-shadow: 0 0 30px rgba(46,160,67,.2); }
}

.hero{
padding:80px 20px;
text-align:center;
background:linear-gradient(135deg,#ffffff,#f6f8fa);
border-bottom:1px solid #d0d7de;
animation: fadeInUp 0.8s ease-out;
}

.logo{
width:140px;
height:140px;
margin:auto;
border-radius:30px;
background:linear-gradient(135deg,#2ea043,#238636);
display:flex;
align-items:center;
justify-content:center;
font-size:70px;
margin-bottom:25px;
animation: pulseShadow 3s infinite ease-in-out, fadeInUp 0.6s ease-out;
}

.hero h1{
font-size:4rem;
font-weight:800;
margin-bottom:10px;
color:#24292f;
}

.hero p{
font-size:1.2rem;
color:#57606a;
max-width:900px;
margin:auto;
}

.badges{
margin-top:25px;
display:flex;
justify-content:center;
gap:15px;
flex-wrap:wrap;
}

.badge{
background:#ffffff;
padding:12px 20px;
border-radius:50px;
border:1px solid #d0d7de;
color:#24292f;
font-weight: 500;
transition: all 0.3s ease;
}

.badge:hover {
transform: scale(1.05);
background: #f0f3f6;
}

.container{
max-width:1300px;
margin:auto;
padding:60px 20px;
animation: fadeInUp 1s ease-out;
}

.section-title{
font-size:2.4rem;
margin-bottom:25px;
font-weight:700;
color:#24292f;
}

.cards{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
gap:25px;
margin-top:30px;
}

.card{
background:#ffffff;
padding:30px;
border-radius:20px;
border:1px solid #d0d7de;
transition: all .3s cubic-bezier(0.25, 0.8, 0.25, 1);
box-shadow: 0 2px 5px rgba(0,0,0,0.02);
}

.card:hover{
transform:translateY(-8px);
border-color:#2ea043;
box-shadow: 0 10px 20px rgba(0,0,0,0.05);
}

.card h3{
font-size:1.3rem;
margin-bottom:15px;
color:#24292f;
}

.card-icon{
font-size:50px;
margin-bottom:15px;
transition: transform 0.3s ease;
}

.card:hover .card-icon {
transform: scale(1.1);
}

.info-box{
background:#ffffff;
padding:30px;
border-radius:20px;
margin-top:25px;
border:1px solid #d0d7de;
box-shadow: 0 2px 5px rgba(0,0,0,0.02);
}

/* --- REPO-AS-A-DATABASE SETUP & CRUD UI STYLING --- */
.setup-banner {
background: #f1f8ff;
border: 1px dashed #0366d6;
padding: 20px;
border-radius: 12px;
margin-bottom: 25px;
}
.setup-banner h3 {
color: #0366d6;
margin-bottom: 10px;
display: flex;
align-items: center;
gap: 8px;
}
.setup-code-preview {
background: #24292e;
color: #e1e4e8;
padding: 10px 15px;
border-radius: 6px;
font-family: monospace;
font-size: 0.85rem;
margin: 8px 0;
}

.crud-grid {
display: grid;
grid-template-columns: 1fr 2fr;
gap: 30px;
margin-top: 20px;
}
@media(max-width: 900px) {
  .crud-grid { grid-template-columns: 1fr; }
}

.form-group {
margin-bottom: 15px;
}
.form-group label {
display: block;
font-weight: 600;
margin-bottom: 5px;
font-size: 0.9rem;
}
.form-group input {
width: 100%;
padding: 10px 15px;
border: 1px solid #d0d7de;
border-radius: 8px;
font-size: 0.95rem;
background: #fafafa;
}
.form-group input:focus {
outline: none;
border-color: #2ea043;
background: #fff;
}
.btn {
background: #2ea043;
color: white;
padding: 10px 20px;
border: none;
border-radius: 8px;
cursor: pointer;
font-weight: 600;
transition: background 0.2s;
display: inline-block;
}
.btn:hover { background: #238636; }
.btn-danger { background: #cf222e; }
.btn-danger:hover { background: #a40e18; }
.btn-secondary { background: #57606a; }
.btn-secondary:hover { background: #24292f; }

.status-log {
margin-top: 15px;
padding: 10px;
border-radius: 6px;
font-size: 0.85rem;
background: #f0f3f6;
border-left: 4px solid #57606a;
}

.code{
background:#1f2428;
padding:20px;
border-radius:15px;
overflow:auto;
margin-top:20px;
font-family:monospace;
white-space:pre-wrap;
color:#e1e4e8;
border:1px solid #24292f;
box-shadow: inset 0 2px 8px rgba(0,0,0,0.2);
}

.flow{
display:flex;
justify-content:center;
align-items:center;
gap:15px;
flex-wrap:wrap;
margin-top:25px;
}

.flow div:not(.arrow){
background:#ffffff;
padding:15px 20px;
border-radius:12px;
border:1px solid #d0d7de;
font-weight: 500;
transition: all 0.3s ease;
}

.flow div:not(.arrow):hover {
background: #f0f3f6;
transform: translateY(-3px);
}

.arrow{
font-size:24px;
color: #2ea043;
animation: walkRight 1.5s infinite ease-in-out;
}

@keyframes walkRight {
  0%, 100% { transform: translateX(0); }
  50% { transform: translateX(4px); }
}

table{
width:100%;
border-collapse:collapse;
margin-top:25px;
background: #ffffff;
border-radius: 12px;
overflow: hidden;
box-shadow: 0 2px 5px rgba(0,0,0,0.02);
border: 1px solid #d0d7de;
}

th{
background:#2ea043;
color: white;
padding:15px;
font-weight: 600;
text-align: left;
}

td{
padding:15px;
border:1px solid #d0d7de;
}

tr:nth-child(even) {
background: #f6f8fa;
}

.action-btns {
display: flex;
gap: 8px;
}

.footer{
text-align:center;
padding:60px 20px;
margin-top:60px;
border-top:1px solid #d0d7de;
background: #ffffff;
color:#57606a;
}

.highlight{
color:#2ea043;
font-weight:700;
background: #dafbe1;
padding: 2px 6px;
border-radius: 4px;
}

ul{
padding-left:25px;
margin-top:15px;
}

li{
margin-bottom:10px;
}

@media(max-width:768px){
.hero h1{ font-size:2.5rem; }
.section-title{ font-size:2rem; }
}
</style>
</head>
<body>

<section class="hero">

<div class="logo">🗄️</div>

<h1>GitBase</h1>

<p>
Turn Any GitHub Repository Into a Lightweight Database.
A professional demonstration project showing how GitHub repositories can store,
manage, and version application data without requiring a traditional database server.
</p>

<div class="badges">
<div class="badge">⚡ GitHub Database</div>
<div class="badge">📦 JSON Storage</div>
<div class="badge">🚀 Open Source</div>
<div class="badge">🔄 Version Controlled</div>
</div>

</section>

<div class="container">

<h2 class="section-title">⚙️ Build Your Own GitHub Database</h2>
<div class="info-box" style="border: 2px solid #0366d6;">
  <p style="font-size: 1.1rem; margin-bottom: 20px;">
    You can easily configure your own GitHub repository to act as a private or public database cluster using the companion web utility provided in this repository!
  </p>

<div class="setup-banner">
  <h3>📂 Step 1: Add Three Required Files to Your Target Repository</h3>
  <p>Initialize your personal database system by adding three raw configuration tracking files to the root directory of your repository:</p>
  
  <p style="margin-top: 15px;"><strong>1. <code>users.json</code></strong> (Maintains user collections data)</p>
  <p style="font-size:0.9rem; color:#57606a;">Create this file initialized with an empty array schema:</p>
  <div class="setup-code-preview">[]</div>

  <p style="margin-top: 15px;"><strong>2. <code>records.json</code></strong> (Holds structural dynamic data entries)</p>
  <p style="font-size:0.9rem; color:#57606a;">Create this file to track core records matrices:</p>
  <div class="setup-code-preview">[]</div>
  
  <p style="margin-top: 15px;"><strong>3. <code>logs.json</code></strong> (Tracks continuous automated transactional changes)</p>
  <p style="font-size:0.9rem; color:#57606a;">Create this history sheet file to map CRUD commits logs:</p>
  <div class="setup-code-preview">[]</div>
</div>

  <div class="setup-banner" style="background: #dafbe1; border-color: #2ea043;">
    <h3 style="color: #238636;">🖥️ Step 2: Access the Management App File</h3>
    <p>I have uploaded a functional standalone <strong>database dashboard web page</strong> directly inside this project repository.</p>
    <ul style="margin-top: 10px; padding-left: 20px;">
      <li>Download or open the provided web page interface utility locally in any browser.</li>
      <li>Securely input your personal target **GitHub Access Credentials** (Username, Target Repo Name, and a Personal Access Token with <code>repo</code> permissions) directly into the page's dashboard panel fields.</li>
      <li>The interface executes full operational <strong>CRUD features (Create, Read, Update, Delete)</strong> directly over your repository data arrays using asynchronous API transactions!</li>
    </ul>
  </div>
</div>

<div class="container" style="padding: 0;">
<h2 class="section-title" style="margin-top:70px;">📦 Use Cases</h2>

<div class="cards">

<div class="card">
<div class="card-icon">🌐</div>
<h3>Portfolio Websites</h3>
<p>
Store projects, achievements, certificates, skills, blogs, and personal profile information.
</p>
</div>

<div class="card">
<div class="card-icon">🤖</div>
<h3>Bots & Automation</h3>
<p>
Save bot settings, user preferences, logs, command configurations, and reports.
</p>
</div>

<div class="card">
<div class="card-icon">📊</div>
<h3>Dashboards</h3>
<p>
Maintain datasets and statistics without purchasing database hosting.
</p>
</div>

<div class="card">
<div class="card-icon">🧪</div>
<h3>Prototypes</h3>
<p>
Rapidly build MVPs and proof-of-concepts using GitHub as a backend.
</p>
</div>

</div>

<h2 class="section-title" style="margin-top:70px;">🤔 Why Use GitHub As A Database?</h2>

<div class="info-box">

<p>
Traditional databases are powerful, but for many small projects they are unnecessary.
GitHub already provides several core features needed for data storage:
</p>

<ul>
<li>✅ Cloud Storage</li>
<li>✅ Global Accessibility</li>
<li>✅ GitHub API Access</li>
<li>✅ Built-in Backups</li>
<li>✅ Version History</li>
<li>✅ Collaboration Features</li>
<li>✅ Free Hosting</li>
</ul>

<div class="code">
{
  "id": 1,
  "name": "Jai",
  "role": "Developer"
}
</div>

<p style="margin-top:20px;">
The above JSON can be stored inside a repository file such as:
<span class="highlight">data/users.json</span>
and accessed anywhere in the world.
</p>

</div>

<h2 class="section-title" style="margin-top:70px;">🏗️ How GitBase Works</h2>

<div class="info-box">

<p>
GitBase treats files as database tables or collections.
</p>

<div class="code">
GitHub Repository

├── users.json
├── products.json
├── notes.json
└── logs.json
</div>

<p style="margin-top:20px;">
Each file acts as a collection:
</p>

<div class="code">
users.json     → Users Collection
products.json  → Products Collection
notes.json     → Notes Collection
logs.json      → Logs Collection
</div>

</div>

<h2 class="section-title" style="margin-top:70px;">🔄 Data Flow</h2>

<div class="flow">
<div>📖 Read File</div>
<div class="arrow">➡️</div>
<div>✏️ Modify Data</div>
<div class="arrow">➡️</div>
<div>💾 Commit Changes</div>
<div class="arrow">➡️</div>
<div>🚀 Push To GitHub</div>
<div class="arrow">➡️</div>
<div>✅ Updated Database</div>
</div>

<h2 class="section-title" style="margin-top:70px;">📂 Repository Structure</h2>

<div class="code">
gitBase/
├── users.json          → Users Collection (Initialized as [])
├── records.json        → Dynamic Records Entries (Initialized as [])
├── logs.json           → Transaction History Log (Initialized as [])
│
├── data/
│   ├── products.json
│   ├── posts.json
│   └── settings.json
│
├── examples/
│   ├── javascript/
│   ├── python/
│   └── html/
│
├── docs/
│   └── architecture.md
│
├── README.md
└── LICENSE
</div>

<h2 class="section-title" style="margin-top:70px;">🔍 Reading Data</h2>

<div class="info-box">

<p>Example JavaScript:</p>

<div class="code">
fetch(
'https://raw.githubusercontent.com/username/gitBase/main/data/users.json'
)
.then(response => response.json())
.then(data => console.log(data));
</div>

</div>

<h2 class="section-title" style="margin-top:70px;">✍️ Writing Data</h2>

<div class="info-box">

<p>
Writing data is performed using the GitHub REST API.
</p>

<div class="flow">
<div>📖 Read</div>
<div class="arrow">➡️</div>
<div>✏️ Edit</div>
<div class="arrow">➡️</div>
<div>📦 Commit</div>
<div class="arrow">➡️</div>
<div>🚀 Push</div>
</div>

</div>

<h2 class="section-title" style="margin-top:70px;">🛠️ CRUD Operations</h2>

<table>

<tr>
<th>Operation</th>
<th>GitBase Method</th>
</tr>

<tr>
<td>Create</td>
<td>Add JSON Record</td>
</tr>

<tr>
<td>Read</td>
<td>Fetch JSON File</td>
</tr>

<tr>
<td>Update</td>
<td>Edit Record + Commit</td>
</tr>

<tr>
<td>Delete</td>
<td>Remove Record + Commit</td>
</tr>

</table>

<h2 class="section-title" style="margin-top:70px;">📜 Version History</h2>

<div class="info-box">

<p>
Every database update automatically becomes a Git commit.
</p>

<div class="code">
Commit #1 → Initial Database

Commit #2 → Added User

Commit #3 → Updated Profile

Commit #4 → Removed Record

Commit #5 → Added New Feature
</div>

<p style="margin-top:20px;">
Unlike many databases, every previous state can be restored.
</p>

</div>

<h2 class="section-title" style="margin-top:70px;">⚡ Advantages</h2>

<div class="cards">

<div class="card">
<h3>💸 Free</h3>
<p>No database hosting required.</p>
</div>

<div class="card">
<h3>📜 Version Control</h3>
<p>Every modification is tracked.</p>
</div>

<div class="card">
<h3>🔒 Backup History</h3>
<p>Rollback any change instantly.</p>
</div>

<div class="card">
<h3>🌍 Global Access</h3>
<p>Access data from anywhere.</p>
</div>

</div>

<h2 class="section-title" style="margin-top:70px;">⚠️ Limitations</h2>

<div class="info-box">

<ul>
<li>❌ Not suitable for banking applications</li>
<li>❌ Not ideal for real-time systems</li>
<li>❌ Not suitable for thousands of simultaneous writes</li>
<li>❌ API rate limits apply</li>
<li>❌ Slower than dedicated databases</li>
</ul>

</div>

<h2 class="section-title" style="margin-top:70px;">🎯 Best For</h2>

<div class="cards">

<div class="card">🌐 Personal Websites</div>
<div class="card">📂 Portfolios</div>
<div class="card">🎓 School Projects</div>
<div class="card">🧪 Experimental Projects</div>
<div class="card">🤖 Small Bots</div>
<div class="card">⚙️ Configuration Storage</div>

</div>

<h2 class="section-title" style="margin-top:70px;">🚀 Quick Start</h2>

<div class="info-box">

<div class="code">
git clone https://github.com/JaiServanaBhava/gitBase.git
</div>

<div class="code">
[
 {
   "id":1,
   "name":"Jai",
   "role":"Developer"
 }
]
</div>

<div class="code">
git add .

git commit -m "Added first user"

git push
</div>

<p style="margin-top:20px;">
Your GitHub repository is now functioning as a lightweight database.
</p>

</div>

<h2 class="section-title" style="margin-top:70px;">🧠 Project Goal</h2>

<div class="info-box">

<p>
GitBase demonstrates that Git repositories can be used as lightweight databases
by storing structured data files, leveraging GitHub APIs, and taking advantage of
Git's powerful version control system.
</p>

<p style="margin-top:20px;">
This project is intended for educational purposes and showcases an alternative
approach to storing application data.
</p>

</div>

</div>

<footer class="footer">

<h2>⭐ GitBase</h2>

<p>
Turn Any GitHub Repository Into A Lightweight Database
</p>

<br>

<p>
Made with ❤️ Jai Servana Bhava
</p>

</footer>

</body>
</html>
