# Customer_Details_page
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tech.Care – Patients</title>
<link href="https://fonts.googleapis.com/css2?family=Manrope:wght@400;500;600;700;800&family=DM+Sans:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --teal: #00c8a0;
    --teal-light: #e6faf6;
    --teal-dark: #00a884;
    --navy: #1a2c3d;
    --slate: #3d5166;
    --muted: #7b92a7;
    --border: #e3eaf0;
    --bg: #f4f7fb;
    --white: #ffffff;
    --red: #e74c3c;
    --amber: #f39c12;
    --green: #27ae60;
    --blue: #2980b9;
    --pink: #e91e8c;
    --purple: #8b5cf6;
    --card-shadow: 0 2px 16px rgba(0,80,80,0.07);
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: 'DM Sans', sans-serif; background: var(--bg); color: var(--navy); height: 100vh; overflow: hidden; }

  /* HEADER */
  header {
    display: flex; align-items: center; justify-content: space-between;
    background: var(--white); padding: 0 32px; height: 64px;
    border-bottom: 1px solid var(--border); position: sticky; top: 0; z-index: 100;
    box-shadow: 0 1px 8px rgba(0,0,0,0.04);
  }
  .logo { display: flex; align-items: center; gap: 10px; font-family: 'Manrope', sans-serif; font-weight: 800; font-size: 1.15rem; color: var(--navy); text-decoration: none; }
  .logo-icon { width: 32px; height: 32px; }
  nav { display: flex; gap: 4px; }
  nav a {
    display: flex; align-items: center; gap: 7px; padding: 8px 18px;
    border-radius: 50px; font-size: 0.875rem; font-weight: 500; color: var(--slate);
    text-decoration: none; transition: all 0.18s;
  }
  nav a:hover { background: var(--teal-light); color: var(--teal-dark); }
  nav a.active { background: var(--teal); color: #fff; font-weight: 600; }
  nav a svg { width: 16px; height: 16px; flex-shrink: 0; }
  .header-right { display: flex; align-items: center; gap: 16px; }
  .doc-info { display: flex; align-items: center; gap: 10px; }
  .doc-avatar { width: 38px; height: 38px; border-radius: 50%; background: linear-gradient(135deg,#00c8a0,#2980b9); display:flex;align-items:center;justify-content:center;font-weight:700;color:#fff;font-size:0.9rem; }
  .doc-text { text-align: right; }
  .doc-text .name { font-weight: 700; font-size: 0.875rem; color: var(--navy); }
  .doc-text .role { font-size: 0.75rem; color: var(--muted); }
  .icon-btn { background: none; border: none; cursor: pointer; color: var(--muted); padding: 6px; border-radius: 8px; transition: background 0.15s; }
  .icon-btn:hover { background: var(--bg); }

  /* LAYOUT */
  .app-body { display: grid; grid-template-columns: 260px 1fr 280px; height: calc(100vh - 64px); overflow: hidden; }

  /* LEFT PANEL */
  .patients-panel { background: var(--white); border-right: 1px solid var(--border); display: flex; flex-direction: column; overflow: hidden; }
  .patients-header { display: flex; align-items: center; justify-content: space-between; padding: 20px 20px 12px; }
  .patients-header h2 { font-family: 'Manrope', sans-serif; font-size: 1.05rem; font-weight: 800; color: var(--navy); }
  .search-btn { background: none; border: none; cursor: pointer; color: var(--muted); padding: 4px; }
  .patients-list { overflow-y: auto; flex: 1; padding: 0 8px 16px; }
  .patients-list::-webkit-scrollbar { width: 4px; }
  .patients-list::-webkit-scrollbar-thumb { background: var(--border); border-radius: 4px; }
  .patient-item {
    display: flex; align-items: center; gap: 12px; padding: 10px 12px;
    border-radius: 12px; cursor: pointer; transition: all 0.15s; margin-bottom: 2px;
  }
  .patient-item:hover { background: var(--bg); }
  .patient-item.active { background: var(--teal-light); }
  .patient-avatar { width: 42px; height: 42px; border-radius: 50%; flex-shrink: 0; font-weight: 700; display:flex;align-items:center;justify-content:center;font-size:1rem; }
  .patient-info { flex: 1; min-width: 0; }
  .patient-info .pname { font-weight: 600; font-size: 0.875rem; color: var(--navy); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
  .patient-info .pmeta { font-size: 0.75rem; color: var(--muted); margin-top: 1px; }
  .more-btn { background: none; border: none; cursor: pointer; color: var(--muted); font-size: 1.1rem; padding: 2px 4px; border-radius: 6px; }
  .more-btn:hover { background: var(--border); }

  /* MIDDLE */
  .main-content { overflow-y: auto; padding: 24px; display: flex; flex-direction: column; gap: 20px; }
  .main-content::-webkit-scrollbar { width: 4px; }
  .main-content::-webkit-scrollbar-thumb { background: var(--border); border-radius: 4px; }
  .section-title { font-family: 'Manrope', sans-serif; font-size: 1.1rem; font-weight: 800; color: var(--navy); margin-bottom: 16px; }

  /* BP CHART CARD */
  .card { background: var(--white); border-radius: 16px; padding: 20px; box-shadow: var(--card-shadow); }
  .bp-header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 12px; }
  .bp-title { font-weight: 700; font-size: 0.95rem; color: var(--navy); }
  .bp-filter { display: flex; align-items: center; gap: 6px; background: var(--bg); border: none; border-radius: 8px; padding: 6px 12px; font-size: 0.8rem; color: var(--slate); cursor: pointer; font-family: inherit; }
  .chart-area { position: relative; height: 160px; }
  canvas#bpChart { width: 100% !important; height: 100% !important; }
  .bp-stats { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin-top: 16px; }
  .bp-stat { padding: 14px 16px; border-radius: 12px; background: var(--bg); }
  .bp-stat .label { font-size: 0.78rem; font-weight: 600; color: var(--muted); display: flex; align-items: center; gap: 6px; margin-bottom: 4px; }
  .bp-stat .dot { width: 10px; height: 10px; border-radius: 50%; }
  .bp-stat .value { font-family: 'Manrope', sans-serif; font-size: 1.6rem; font-weight: 800; color: var(--navy); }
  .bp-stat .trend { font-size: 0.75rem; color: var(--muted); margin-top: 4px; display: flex; align-items: center; gap: 4px; }
  .trend-up { color: var(--red); }
  .trend-down { color: var(--green); }

  /* VITALS */
  .vitals-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 14px; }
  .vital-card {
    background: var(--white); border-radius: 16px; padding: 18px; box-shadow: var(--card-shadow);
    transition: transform 0.15s, box-shadow 0.15s;
  }
  .vital-card:hover { transform: translateY(-2px); box-shadow: 0 6px 24px rgba(0,80,80,0.1); }
  .vital-card.selected { outline: 2.5px solid var(--teal); }
  .vital-icon { width: 48px; height: 48px; border-radius: 50%; display: flex; align-items: center; justify-content: center; margin-bottom: 12px; }
  .vital-icon.resp { background: #eaf7f7; }
  .vital-icon.temp { background: #fff3e8; }
  .vital-icon.heart { background: #ffeef2; }
  .vital-icon svg { width: 26px; height: 26px; }
  .vital-label { font-size: 0.78rem; font-weight: 600; color: var(--muted); margin-bottom: 4px; }
  .vital-value { font-family: 'Manrope', sans-serif; font-size: 1.5rem; font-weight: 800; color: var(--navy); }
  .vital-status { font-size: 0.75rem; color: var(--muted); margin-top: 4px; }

  /* DIAGNOSTIC TABLE */
  .diag-table { width: 100%; border-collapse: collapse; }
  .diag-table th { text-align: left; font-size: 0.78rem; font-weight: 700; color: var(--muted); text-transform: uppercase; letter-spacing: 0.04em; padding: 0 12px 10px; }
  .diag-table td { padding: 10px 12px; font-size: 0.855rem; border-top: 1px solid var(--border); }
  .diag-table tr:hover td { background: var(--bg); }
  .diagnosis-name { font-weight: 600; color: var(--navy); }
  .diagnosis-desc { color: var(--slate); }
  .status-badge { display: inline-flex; align-items: center; padding: 4px 10px; border-radius: 20px; font-size: 0.75rem; font-weight: 600; }
  .status-badge.observation { background: #fff8e6; color: #b07d00; }
  .status-badge.cured { background: #e8f8f0; color: #1a8a4a; }
  .status-badge.inactive { background: #f3f4f6; color: #6b7280; }
  .status-badge.active { background: #fee8e8; color: #c0392b; }

  /* RIGHT PANEL */
  .patient-detail { background: var(--white); border-left: 1px solid var(--border); overflow-y: auto; padding: 24px 20px; }
  .patient-detail::-webkit-scrollbar { width: 4px; }
  .patient-detail::-webkit-scrollbar-thumb { background: var(--border); border-radius: 4px; }
  .detail-avatar-wrap { text-align: center; margin-bottom: 12px; }
  .detail-avatar { width: 100px; height: 100px; border-radius: 50%; border: 3px solid var(--teal-light); display:block; margin:0 auto; font-size:2.5rem; font-weight:800; color:#fff; line-height:100px; text-align:center; }
  .detail-name { text-align: center; font-family: 'Manrope', sans-serif; font-size: 1.15rem; font-weight: 800; color: var(--navy); margin-bottom: 18px; }
  .detail-info-list { display: flex; flex-direction: column; gap: 14px; margin-bottom: 20px; }
  .detail-info-item { display: flex; align-items: flex-start; gap: 12px; }
  .detail-info-item .di-icon { width: 32px; height: 32px; border-radius: 50%; background: var(--bg); display: flex; align-items: center; justify-content: center; flex-shrink: 0; margin-top: 2px; }
  .detail-info-item .di-icon svg { width: 15px; height: 15px; color: var(--muted); }
  .detail-info-item .di-label { font-size: 0.75rem; color: var(--muted); margin-bottom: 2px; }
  .detail-info-item .di-value { font-size: 0.855rem; font-weight: 600; color: var(--navy); }
  .show-all-btn {
    display: block; width: 100%; background: var(--teal); color: #fff;
    border: none; border-radius: 50px; padding: 12px 20px; font-size: 0.875rem;
    font-weight: 700; cursor: pointer; font-family: inherit; transition: background 0.18s;
    margin-bottom: 20px;
  }
  .show-all-btn:hover { background: var(--teal-dark); }
  .lab-results-section h3 { font-family: 'Manrope', sans-serif; font-size: 1rem; font-weight: 800; color: var(--navy); margin-bottom: 12px; }
  .lab-item { display: flex; align-items: center; justify-content: space-between; padding: 10px 0; border-bottom: 1px solid var(--border); }
  .lab-item:last-child { border-bottom: none; }
  .lab-item span { font-size: 0.855rem; color: var(--slate); font-weight: 500; }
  .lab-dl { background: none; border: none; cursor: pointer; color: var(--teal); padding: 4px; border-radius: 6px; transition: background 0.15s; }
  .lab-dl:hover { background: var(--teal-light); }

  @keyframes fadeIn { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }
  .main-content > * { animation: fadeIn 0.3s ease both; }
  .main-content > *:nth-child(2) { animation-delay: 0.07s; }
  .main-content > *:nth-child(3) { animation-delay: 0.13s; }
  .main-content > *:nth-child(4) { animation-delay: 0.19s; }
</style>
</head>
<body>

<!-- HEADER -->
<header>
  <a href="#" class="logo">
    <svg class="logo-icon" viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg">
      <rect width="32" height="32" rx="8" fill="#00c8a0"/>
      <path d="M10 16h4v-6h4v6h4" stroke="#fff" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"/>
      <path d="M6 22c2-4 4-6 10-6s8 2 10 6" stroke="#fff" stroke-width="2" stroke-linecap="round" opacity="0.5"/>
    </svg>
    Tech.Care
  </a>
  <nav>
    <a href="#" class="nav-link">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="7" height="7" rx="1"/><rect x="14" y="3" width="7" height="7" rx="1"/><rect x="3" y="14" width="7" height="7" rx="1"/><rect x="14" y="14" width="7" height="7" rx="1"/></svg>
      Overview
    </a>
    <a href="#" class="nav-link active">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></svg>
      Patients
    </a>
    <a href="#" class="nav-link">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="4" width="18" height="18" rx="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg>
      Schedule
    </a>
    <a href="#" class="nav-link">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/></svg>
      Message
    </a>
    <a href="#" class="nav-link">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="2" y="5" width="20" height="14" rx="2"/><line x1="2" y1="10" x2="22" y2="10"/></svg>
      Transactions
    </a>
  </nav>
  <div class="header-right">
    <div class="doc-info">
      <div class="doc-text">
        <div class="name">Dr. Jose Simmons</div>
        <div class="role">General Practitioner</div>
      </div>
      <div class="doc-avatar">JS</div>
    </div>
    <button class="icon-btn">
      <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 1 1-2.83 2.83l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 1 1-4 0v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 1 1-2.83-2.83l.06-.06A1.65 1.65 0 0 0 4.68 15a1.65 1.65 0 0 0-1.51-1H3a2 2 0 1 1 0-4h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 1 1 2.83-2.83l.06.06A1.65 1.65 0 0 0 9 4.68a1.65 1.65 0 0 0 1-1.51V3a2 2 0 1 1 4 0v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 1 1 2.83 2.83l-.06.06A1.65 1.65 0 0 0 19.4 9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 1 1 0 4h-.09a1.65 1.65 0 0 0-1.51 1z"/></svg>
    </button>
  </div>
</header>

<!-- BODY -->
<div class="app-body">

  <!-- LEFT: Patients -->
  <aside class="patients-panel">
    <div class="patients-header">
      <h2>Patients</h2>
      <button class="search-btn">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/></svg>
      </button>
    </div>
    <div class="patients-list" id="patientsList"></div>
  </aside>

  <!-- MIDDLE: Diagnosis -->
  <main class="main-content" id="mainContent">
    <div class="card">
      <div class="bp-header">
        <span class="bp-title">Blood Pressure</span>
        <button class="bp-filter">Last 6 months ▾</button>
      </div>
      <div class="chart-area"><canvas id="bpChart"></canvas></div>
      <div class="bp-stats">
        <div class="bp-stat">
          <div class="label"><span class="dot" style="background:#e91e8c"></span> Systolic</div>
          <div class="value" id="sysVal">160</div>
          <div class="trend trend-up">▲ Higher than Average</div>
        </div>
        <div class="bp-stat">
          <div class="label"><span class="dot" style="background:#8b5cf6"></span> Diastolic</div>
          <div class="value" id="diasVal">78</div>
          <div class="trend trend-down">▼ Lower than Average</div>
        </div>
      </div>
    </div>

    <div class="vitals-grid">
      <div class="vital-card">
        <div class="vital-icon resp">
          <svg viewBox="0 0 24 24" fill="none" stroke="#00c8a0" stroke-width="1.8"><path d="M12 22c-4.97 0-9-4.03-9-9 0-1.82.55-3.53 1.49-4.94"/><path d="M12 22c4.97 0 9-4.03 9-9 0-1.82-.55-3.53-1.49-4.94"/><path d="M5.5 9S7 7 9 7s3.5 2 3.5 2V5a2 2 0 0 0-2-2h-2a2 2 0 0 0-2 2v4z"/><path d="M18.5 9S17 7 15 7s-3.5 2-3.5 2V5a2 2 0 0 1 2-2h2a2 2 0 0 1 2 2v4z"/></svg>
        </div>
        <div class="vital-label">Respiratory Rate</div>
        <div class="vital-value">20 bpm</div>
        <div class="vital-status">Normal</div>
      </div>
      <div class="vital-card">
        <div class="vital-icon temp">
          <svg viewBox="0 0 24 24" fill="none" stroke="#f39c12" stroke-width="1.8"><path d="M14 14.76V3.5a2.5 2.5 0 0 0-5 0v11.26a4.5 4.5 0 1 0 5 0z"/></svg>
        </div>
        <div class="vital-label">Temperature</div>
        <div class="vital-value">98.6°F</div>
        <div class="vital-status">Normal</div>
      </div>
      <div class="vital-card selected">
        <div class="vital-icon heart">
          <svg viewBox="0 0 24 24" fill="none" stroke="#e74c3c" stroke-width="1.8"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg>
        </div>
        <div class="vital-label">Heart Rate</div>
        <div class="vital-value">78 bpm</div>
        <div class="vital-status trend-down">▼ Lower than Average</div>
      </div>
    </div>

    <div class="card">
      <div class="section-title">Diagnostic List</div>
      <table class="diag-table">
        <thead>
          <tr>
            <th>Problem / Diagnosis</th>
            <th>Description</th>
            <th>Status</th>
          </tr>
        </thead>
        <tbody id="diagBody"></tbody>
      </table>
    </div>
  </main>

  <!-- RIGHT: Patient Detail -->
  <aside class="patient-detail" id="patientDetail">
    <div class="detail-avatar-wrap">
      <div class="detail-avatar" id="detailAvatar">JT</div>
    </div>
    <div class="detail-name" id="detailName">Jessica Taylor</div>
    <div class="detail-info-list" id="detailInfo"></div>
    <button class="show-all-btn">Show All Information</button>
    <div class="lab-results-section">
      <h3>Lab Results</h3>
      <div id="labResults"></div>
    </div>
  </aside>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
<script>
const patients = [
  { id:1, name:"Emily Williams", gender:"Female", age:18, color:"#f093fb", dob:"Mar 5, 2006", contact:"(312) 555-8821", emergency:"(312) 555-9900", insurance:"Blue Cross Shield", sys:[130,128,135,140,132,138], dias:[82,80,85,88,84,86], diagnoses:[{problem:"Anemia",desc:"Low hemoglobin levels",status:"active"},{problem:"Migraine",desc:"Recurrent severe headaches",status:"inactive"}] },
  { id:2, name:"Ryan Johnson", gender:"Male", age:45, color:"#4facfe", dob:"Oct 14, 1979", contact:"(415) 555-3302", emergency:"(415) 555-4411", insurance:"Aetna Health", sys:[145,150,155,148,152,149], dias:[90,92,95,88,93,91], diagnoses:[{problem:"High Cholesterol",desc:"Elevated LDL levels",status:"observation"},{problem:"Type 2 Diabetes",desc:"Insulin resistance",status:"cured"}] },
  { id:3, name:"Brandon Mitchell", gender:"Male", age:36, color:"#43e97b", dob:"Jun 22, 1988", contact:"(213) 555-6677", emergency:"(213) 555-7788", insurance:"Kaiser Permanente", sys:[120,118,122,125,119,121], dias:[75,73,78,76,74,77], diagnoses:[{problem:"Asthma",desc:"Bronchial constriction episodes",status:"inactive"}] },
  { id:4, name:"Jessica Taylor", gender:"Female", age:28, color:"#f5576c", dob:"Aug 23, 1996", contact:"(415) 555-1234", emergency:"(415) 555-5678", insurance:"Sunrise Health Assurance", sys:[120,118,160,150,155,158], dias:[110,102,65,68,70,72], diagnoses:[{problem:"Hypertension",desc:"Chronic high blood pressure",status:"observation"},{problem:"Type 2 Diabetes",desc:"Insulin resistance and elevated blood sugar",status:"cured"},{problem:"Asthma",desc:"Recurrent episodes of bronchial constriction",status:"inactive"},{problem:"Osteoarthritis",desc:"Degenerative joint disease",status:"observation"}] },
  { id:5, name:"Samantha Johnson", gender:"Female", age:56, color:"#fa709a", dob:"Jan 7, 1968", contact:"(650) 555-2200", emergency:"(650) 555-3311", insurance:"United Health", sys:[135,140,138,142,137,141], dias:[85,88,86,90,84,87], diagnoses:[{problem:"Osteoporosis",desc:"Reduced bone density",status:"observation"},{problem:"Hypertension",desc:"Chronic high blood pressure",status:"active"}] },
  { id:6, name:"Ashley Martinez", gender:"Female", age:54, color:"#ffd166", dob:"Mar 29, 1970", contact:"(510) 555-4455", emergency:"(510) 555-5566", insurance:"Cigna Health", sys:[128,130,125,132,129,127], dias:[80,82,78,84,81,79], diagnoses:[{problem:"Arthritis",desc:"Joint inflammation",status:"inactive"}] },
  { id:7, name:"Olivia Brown", gender:"Female", age:32, color:"#a18cd1", dob:"Sep 11, 1992", contact:"(408) 555-6677", emergency:"(408) 555-7788", insurance:"Blue Shield CA", sys:[115,117,118,116,119,114], dias:[72,74,73,75,71,73], diagnoses:[{problem:"Anxiety",desc:"Generalized anxiety disorder",status:"observation"},{problem:"Vitamin D Deficiency",desc:"Low serum vitamin D levels",status:"cured"}] },
  { id:8, name:"Tyler Davis", gender:"Male", age:19, color:"#56ccf2", dob:"Nov 2, 2005", contact:"(925) 555-8899", emergency:"(925) 555-9900", insurance:"Medicaid", sys:[110,112,108,115,111,109], dias:[68,70,67,72,69,71], diagnoses:[{problem:"Acne",desc:"Inflammatory skin condition",status:"cured"}] },
  { id:9, name:"Kevin Anderson", gender:"Male", age:30, color:"#96fbc4", dob:"Feb 18, 1994", contact:"(707) 555-1122", emergency:"(707) 555-2233", insurance:"Anthem Blue Cross", sys:[122,124,120,126,121,123], dias:[76,78,75,80,77,74], diagnoses:[{problem:"GERD",desc:"Gastroesophageal reflux disease",status:"observation"}] },
  { id:10, name:"Dylan Thompson", gender:"Male", age:36, color:"#fddb92", dob:"Jul 4, 1988", contact:"(831) 555-3344", emergency:"(831) 555-4455", insurance:"Oscar Health", sys:[118,120,122,116,119,121], dias:[74,76,73,78,75,77], diagnoses:[{problem:"Eczema",desc:"Chronic skin inflammation",status:"inactive"}] },
  { id:11, name:"Nathan Evans", gender:"Male", age:58, color:"#fbc2eb", dob:"Apr 25, 1966", contact:"(559) 555-5566", emergency:"(559) 555-6677", insurance:"Medicare", sys:[148,152,155,150,153,149], dias:[92,95,93,97,91,94], diagnoses:[{problem:"Coronary Artery Disease",desc:"Narrowing of arteries",status:"observation"},{problem:"Type 2 Diabetes",desc:"Insulin resistance",status:"observation"}] },
  { id:12, name:"Mike Nolan", gender:"Male", age:31, color:"#a1c4fd", dob:"Dec 15, 1993", contact:"(805) 555-7788", emergency:"(805) 555-8899", insurance:"Covered CA", sys:[116,118,120,114,117,119], dias:[72,74,71,76,73,75], diagnoses:[{problem:"Back Pain",desc:"Lumbar strain and discomfort",status:"inactive"}] }
];

const months = ["Oct 2023","Nov 2023","Dec 2023","Jan 2024","Feb 2024","Mar 2024"];
let activeId = 4;
let bpChartInstance = null;

function initials(name){ return name.split(" ").map(n=>n[0]).join("").substring(0,2).toUpperCase(); }

function statusClass(s){
  if(s==="observation") return "observation";
  if(s==="cured") return "cured";
  if(s==="inactive") return "inactive";
  return "active";
}
function statusLabel(s){
  if(s==="observation") return "Under Observation";
  if(s==="cured") return "Cured";
  if(s==="inactive") return "Inactive";
  return "Active";
}

function renderPatientsList(){
  const list = document.getElementById("patientsList");
  list.innerHTML = patients.map(p=>`
    <div class="patient-item${p.id===activeId?' active':''}" onclick="selectPatient(${p.id})">
      <div class="patient-avatar" style="background:${p.color}22;color:${p.color};">${initials(p.name)}</div>
      <div class="patient-info">
        <div class="pname">${p.name}</div>
        <div class="pmeta">${p.gender}, ${p.age}</div>
      </div>
      <button class="more-btn">⋯</button>
    </div>
  `).join("");
}

function renderDetail(p){
  document.getElementById("detailAvatar").textContent = initials(p.name);
  document.getElementById("detailAvatar").style.background = `linear-gradient(135deg, ${p.color}, ${p.color}99)`;
  document.getElementById("detailName").textContent = p.name;
  document.getElementById("detailInfo").innerHTML = `
    <div class="detail-info-item">
      <div class="di-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="4" width="18" height="18" rx="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg></div>
      <div><div class="di-label">Date Of Birth</div><div class="di-value">${p.dob}</div></div>
    </div>
    <div class="detail-info-item">
      <div class="di-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="8" r="4"/><path d="M4 20c0-4 3.6-7 8-7s8 3 8 7"/></svg></div>
      <div><div class="di-label">Gender</div><div class="di-value">${p.gender}</div></div>
    </div>
    <div class="detail-info-item">
      <div class="di-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07A19.5 19.5 0 0 1 4.69 12a19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 3.62 1.27h3a2 2 0 0 1 2 1.72c.127.96.361 1.903.7 2.81a2 2 0 0 1-.45 2.11L8.09 9a16 16 0 0 0 6.72 6.72l1.09-1.09a2 2 0 0 1 2.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0 1 22 16.92z"/></svg></div>
      <div><div class="di-label">Contact Info.</div><div class="di-value">${p.contact}</div></div>
    </div>
    <div class="detail-info-item">
      <div class="di-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07A19.5 19.5 0 0 1 4.69 12a19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 3.62 1.27h3a2 2 0 0 1 2 1.72c.127.96.361 1.903.7 2.81a2 2 0 0 1-.45 2.11L8.09 9a16 16 0 0 0 6.72 6.72l1.09-1.09a2 2 0 0 1 2.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0 1 22 16.92z"/></svg></div>
      <div><div class="di-label">Emergency Contacts</div><div class="di-value">${p.emergency}</div></div>
    </div>
    <div class="detail-info-item">
      <div class="di-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg></div>
      <div><div class="di-label">Insurance Provider</div><div class="di-value">${p.insurance}</div></div>
    </div>
  `;
  const labs = ["Blood Tests","CT Scans","Radiology Reports","X-Rays","Urine Test"];
  document.getElementById("labResults").innerHTML = labs.map(l=>`
    <div class="lab-item">
      <span>${l}</span>
      <button class="lab-dl" title="Download">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
      </button>
    </div>
  `).join("");
}

function renderDiagnoses(p){
  document.getElementById("diagBody").innerHTML = p.diagnoses.map(d=>`
    <tr>
      <td class="diagnosis-name">${d.problem}</td>
      <td class="diagnosis-desc">${d.desc}</td>
      <td><span class="status-badge ${statusClass(d.status)}">${statusLabel(d.status)}</span></td>
    </tr>
  `).join("");
}

function renderChart(p){
  const ctx = document.getElementById("bpChart").getContext("2d");
  if(bpChartInstance){ bpChartInstance.destroy(); }
  bpChartInstance = new Chart(ctx, {
    type:"line",
    data:{
      labels: months,
      datasets:[
        { label:"Systolic", data: p.sys, borderColor:"#e91e8c", borderWidth:2.5, tension:0.45, pointBackgroundColor:"#e91e8c", pointRadius:5, pointHoverRadius:7, fill:false },
        { label:"Diastolic", data: p.dias, borderColor:"#8b5cf6", borderWidth:2.5, tension:0.45, pointBackgroundColor:"#8b5cf6", pointRadius:5, pointHoverRadius:7, fill:false }
      ]
    },
    options:{
      responsive:true, maintainAspectRatio:false,
      plugins:{ legend:{ display:false }, tooltip:{ mode:"index", intersect:false } },
      scales:{
        x:{ grid:{ color:"rgba(0,0,0,0.05)" }, ticks:{ font:{ size:11 }, color:"#7b92a7" } },
        y:{ min:60, max:180, grid:{ color:"rgba(0,0,0,0.05)" }, ticks:{ font:{ size:11 }, color:"#7b92a7", stepSize:20 } }
      }
    }
  });
  document.getElementById("sysVal").textContent = p.sys[p.sys.length-1];
  document.getElementById("diasVal").textContent = p.dias[p.dias.length-1];
}

function selectPatient(id){
  activeId = id;
  const p = patients.find(x=>x.id===id);
  renderPatientsList();
  renderDetail(p);
  renderDiagnoses(p);
  renderChart(p);
}

renderPatientsList();
selectPatient(4);
</script>
</body>
</html>
