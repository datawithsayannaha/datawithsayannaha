<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sayan Naha — Data Analyst Portfolio</title>

<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet">

<style>
:root {
  --violet: #7c3aed;
  --pink: #ec4899;
  --bg: #08080f;
  --bg3: #110f22;
  --border: #1e1a38;
  --text: #e8e6ff;
  --muted: #6b7280;
}

* { margin:0; padding:0; box-sizing:border-box; }

body {
  background: var(--bg);
  color: var(--text);
  font-family: 'Syne', sans-serif;
}

/* NAV */
nav {
  position: fixed;
  width:100%;
  padding:15px 20px;
  display:flex;
  justify-content:space-between;
  background:rgba(0,0,0,0.8);
}
nav a {
  color:var(--muted);
  text-decoration:none;
  margin-left:20px;
}
nav a:hover { color:white; }

/* HERO */
.hero {
  text-align:center;
  padding:120px 20px 60px;
}
.hero h1 {
  font-size:60px;
  background:linear-gradient(135deg,#a78bfa,#ec4899);
  -webkit-background-clip:text;
  -webkit-text-fill-color:transparent;
}
.hero p {
  margin-top:10px;
  color:#c4bbf0;
}

/* SECTION */
.section {
  max-width:800px;
  margin:60px auto;
  padding:0 20px;
}

/* CARD */
.card {
  background:var(--bg3);
  border:1px solid var(--border);
  padding:20px;
  border-radius:12px;
  margin-bottom:15px;
}

/* SKILLS */
.skills {
  display:grid;
  grid-template-columns:repeat(2,1fr);
  gap:15px;
}

/* BUTTON */
.btn {
  display:inline-block;
  margin-top:20px;
  padding:10px 20px;
  border-radius:30px;
  background:linear-gradient(135deg,var(--violet),var(--pink));
  color:white;
  text-decoration:none;
}

/* FOOTER */
footer {
  text-align:center;
  padding:40px;
  color:var(--muted);
}
</style>
</head>

<body>

<!-- NAV -->
<nav>
  <div>Sayan Naha</div>
  <div>
    <a href="#about">About</a>
    <a href="#skills">Skills</a>
    <a href="#projects">Projects</a>
  </div>
</nav>

<!-- HERO -->
<section class="hero">
  <h1>Sayan Naha</h1>
  <p>Data Analyst | SQL · Python · Power BI · Excel</p>
  <p>Turning raw data into meaningful insights 📊</p>

  <a href="https://github.com/YOUR_USERNAME" class="btn">GitHub</a>
</section>

<!-- ABOUT -->
<section class="section" id="about">
  <h2>About Me</h2>
  <div class="card">
    <p>
      I am an aspiring Data Analyst focused on SQL, Python, Power BI, and Excel.
      My goal is to secure a Work From Home or private sector role.
    </p>
  </div>
</section>

<!-- SKILLS -->
<section class="section" id="skills">
  <h2>Skills</h2>

  <div class="skills">
    <div class="card">🐍 Python (Pandas, NumPy, Matplotlib)</div>
    <div class="card">🗄️ SQL (PostgreSQL, Joins, CTEs)</div>
    <div class="card">📊 Power BI (DAX, Dashboards)</div>
    <div class="card">📗 Excel (Pivot, VLOOKUP)</div>
  </div>
</section>

<!-- PROJECTS -->
<section class="section" id="projects">
  <h2>Projects</h2>

  <div class="card">
    <h3>Sales Dashboard</h3>
    <p>Power BI dashboard with KPI tracking and trend analysis.</p>
  </div>

  <div class="card">
    <h3>SQL Data Analysis</h3>
    <p>Exploratory data analysis using SQL + Python.</p>
  </div>
</section>

<!-- CONTACT -->
<section class="section">
  <h2>Connect</h2>
  <div class="card">
    <p>Email: youremail@gmail.com</p>
    <p>LinkedIn: linkedin.com/in/YOUR_USERNAME</p>
  </div>
</section>

<!-- FOOTER -->
<footer>
  © 2026 Sayan Naha · Data Analyst
</footer>

</body>
</html>
