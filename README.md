<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Judiciary Records Management System</title>
  <style>
    :root{
      --bg:#0b1220;
      --panel:#111827;
      --card:#182235;
      --line:#2b3950;
      --text:#e5e7eb;
      --muted:#94a3b8;
      --accent:#22c55e;
      --accent2:#38bdf8;
      --warn:#f59e0b;
      --danger:#ef4444;
      --shadow:0 10px 30px rgba(0,0,0,.2);
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family:Segoe UI,Arial,sans-serif;
      background:linear-gradient(180deg,#08101f,#0b1220);
      color:var(--text);
    }
    header{
      padding:22px 20px;
      border-bottom:1px solid var(--line);
      position:sticky;
      top:0;
      background:rgba(11,18,32,.94);
      backdrop-filter:blur(10px);
      z-index:10;
    }
    h1{margin:0;font-size:24px}
    p{margin:6px 0 0;color:var(--muted)}
    .wrap{
      max-width:1440px;
      margin:0 auto;
      padding:20px;
      display:grid;
      grid-template-columns:380px 1fr;
      gap:18px;
    }
    .panel{
      background:rgba(17,24,39,.94);
      border:1px solid var(--line);
      border-radius:16px;
      padding:16px;
      box-shadow:var(--shadow);
    }
    .grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:12px}
    .grid3{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:12px}
    .split{display:grid;grid-template-columns:1fr 1fr;gap:12px}
    label{
      display:block;
      font-size:12px;
      color:var(--muted);
      margin:0 0 6px;
    }
    input,select,textarea,button{font:inherit}
    input,select,textarea{
      width:100%;
      background:#0b1220;
      border:1px solid var(--line);
      color:var(--text);
      border-radius:10px;
      padding:11px 12px;
      outline:none;
    }
    textarea{min-height:92px;resize:vertical}
    .full{grid-column:1/-1}
    .btns{
      display:flex;
      gap:10px;
      flex-wrap:wrap;
      margin-top:12px;
    }
    button{
      border:0;
      border-radius:10px;
      padding:11px 14px;
      font-weight:700;
      cursor:pointer;
    }
    .primary{background:var(--accent);color:#052e16}
    .secondary{background:#1d4ed8;color:#eff6ff}
    .ghost{background:#334155;color:#e2e8f0}
    .danger{background:var(--danger);color:#fff}
    .stats{
      display:grid;
      grid-template-columns:repeat(4,1fr);
      gap:12px;
      margin-bottom:16px;
    }
    .stat{
      background:var(--card);
      border:1px solid var(--line);
      border-radius:14px;
      padding:14px;
    }
    .k{font-size:12px;color:var(--muted)}
    .v{font-size:24px;font-weight:800;margin-top:4px}
    table{
      width:100%;
      border-collapse:collapse;
      background:rgba(11,18,32,.8);
      border:1px solid var(--line);
      border-radius:14px;
      overflow:hidden;
    }
    th,td{
      padding:12px;
      border-bottom:1px solid var(--line);
      text-align:left;
      font-size:14px;
    }
    th{
      position:sticky;
      top:92px;
      background:#111827;
      color:#cbd5e1;
    }
    tr:hover td{background:rgba(56,189,248,.06)}
    .tag{
      padding:4px 8px;
      border-radius:999px;
      font-size:12px;
      font-weight:800;
      display:inline-block;
    }
    .open{background:#052e16;color:#86efac}
    .hold{background:#3b0764;color:#e879f9}
    .closed{background:#3f1d0a;color:#fdba74}
    .timeline{display:grid;gap:10px}
    .item{
      border-left:3px solid var(--accent2);
      padding:10px 12px;
      background:#0b1220;
      border-radius:10px;
    }
    .item small{color:var(--muted)}
    .toolbar{
      display:flex;
      gap:10px;
      align-items:center;
      justify-content:space-between;
      margin-bottom:10px;
      flex-wrap:wrap;
    }
    .hint{font-size:12px;color:var(--muted)}
    .jsonbox{
      width:100%;
      min-height:280px;
      background:#08101f;
      border:1px solid var(--line);
      border-radius:12px;
      color:#dbeafe;
      padding:12px;
      font-family:Consolas,monospace;
      font-size:12px;
      line-height:1.45;
      resize:vertical;
    }
    @media (max-width:1200px){
      .wrap{grid-template-columns:1fr}
      .stats,.grid3,.split{grid-template-columns:1fr 1fr}
    }
    @media (max-width:760px){
      .grid,.grid3,.stats,.split{grid-template-columns:1fr}
      th{top:0}
    }
  </style>
</head>
<body>
<header>
  <h1>Judiciary Records Management System</h1>
  <p>Single-file HTML + JavaScript prototype with editable JSON config and Power Automate-ready payloads.</p>
</header>

<div class="wrap">
  <aside class="panel">
    <h2 style="margin:0 0 12px">New File Entry</h2>
    <form id="caseForm">
      <div class="grid">
        <div><label>File No.</label><input id="fileNo" required placeholder="JRMS-2026-001"></div>
        <div><label>Priority</label><select id="priority"></select></div>

        <div class="full"><label>Title / Subject</label><input id="title" required placeholder="Application for bail review"></div>

        <div><label>Origin Department</label><select id="originDept"></select></div>
        <div><label>Current Department</label><select id="currentDept"></select></div>

        <div><label>Assigned Officer</label><input id="officer" placeholder="Officer name"></div>
        <div><label>Status</label><select id="status"></select></div>

        <div><label>Date Opened</label><input id="dateOpened" type="date"></div>
        <div class="full"><label>Description</label><textarea id="description" placeholder="Brief summary of the file."></textarea></div>
        <div class="full"><label>Remarks / Movement Notes</label><textarea id="remarks" placeholder="Reason for transfer, approval notes, handover details."></textarea></div>
      </div>

      <div class="btns">
        <button type="submit" class="primary">Save Record</button>
        <button type="button" class="secondary" id="addMovement">Add Movement</button>
        <button type="button" class="ghost" id="exportJson">Export JSON</button>
        <button type="button" class="danger" id="resetDemo">Reset Demo</button>
      </div>

      <p class="hint">This prototype stores data in browser memory and can later POST JSON to Power Automate.</p>
    </form>
  </aside>

  <main>
    <section class="stats">
      <div class="stat"><div class="k">Total Files</div><div class="v" id="totalFiles">0</div></div>
      <div class="stat"><div class="k">Open</div><div class="v" id="openFiles">0</div></div>
      <div class="stat"><div class="k">On Hold</div><div class="v" id="holdFiles">0</div></div>
      <div class="stat"><div class="k">Closed</div><div class="v" id="closedFiles">0</div></div>
    </section>

    <section class="panel" style="margin-bottom:18px">
      <div class="toolbar">
        <h2 style="margin:0">Case Register</h2>
        <input id="search" placeholder="Search file no., title, officer..." style="max-width:320px">
      </div>
      <table>
        <thead>
          <tr>
            <th>File No.</th>
            <th>Title</th>
            <th>Department</th>
            <th>Officer</th>
            <th>Status</th>
            <th>Priority</th>
          </tr>
        </thead>
        <tbody id="caseTable"></tbody>
      </table>
    </section>

    <section class="grid3" style="margin-bottom:18px">
      <div class="panel">
        <h2 style="margin-top:0">Movement History</h2>
        <div class="timeline" id="movementLog"></div>
      </div>

      <div class="panel">
        <h2 style="margin-top:0">Workflow Map</h2>
        <div class="timeline">
          <div class="item"><b>Registry</b><br><small>Receive and log incoming files.</small></div>
          <div class="item"><b>Research</b><br><small>Review precedents and prepare notes.</small></div>
          <div class="item"><b>Registrar</b><br><small>Approve transfers and sign off.</small></div>
          <div class="item"><b>Archive</b><br><small>Close and store completed files.</small></div>
        </div>
      </div>

      <div class="panel">
        <h2 style="margin-top:0">Power Automate Hook</h2>
        <div class="timeline">
          <div class="item"><b>POST JSON</b><br><small>Send form data to your flow endpoint.</small></div>
          <div class="item"><b>Approval</b><br><small>Use the payload to start a department approval.</small></div>
          <div class="item"><b>File Move</b><br><small>Move document to the next SharePoint folder.</small></div>
          <div class="item"><b>Audit Log</b><br><small>Store each movement with timestamps.</small></div>
        </div>
      </div>
    </section>

    <section class="split">
      <div class="panel">
        <h2 style="margin-top:0">Editable JSON Configuration</h2>
        <textarea id="configJson" class="jsonbox"></textarea>
        <div class="btns"><button class="secondary" type="button" id="applyConfig">Apply Config</button></div>
      </div>

      <div class="panel">
        <h2 style="margin-top:0">Payload Preview</h2>
        <textarea id="payloadJson" class="jsonbox" readonly></textarea>
        <div class="btns"><button class="ghost" type="button" id="copyPayload">Copy Payload</button></div>
      </div>
    </section>
  </main>
</div>

<script>
  const state = {
    config: {
      appName: 'Judiciary Records Management System',
      departments: ['Registry','Research','Registrar','Archive','Courtroom','Clerk Office'],
      priorities: ['Normal','High','Urgent'],
      statuses: ['Open','On Hold','Closed'],
      powerAutomate: {
        enabled: true,
        endpoint: 'https://YOUR-FLOW-URL-HERE',
        authHeaderName: 'x-api-key',
        authHeaderValue: 'REPLACE_ME'
      }
    },
    cases: [
      {fileNo:'JRMS-2026-001',title:'Bail Review Application',dept:'Registry',officer:'A. Wanjiku',status:'Open',priority:'Urgent'},
      {fileNo:'JRMS-2026-002',title:'Appeal Record Filing',dept:'Research',officer:'P. Otieno',status:'On Hold',priority:'High'},
      {fileNo:'JRMS-2026-003',title:'Judgment Copy Request',dept:'Archive',officer:'M. Kariuki',status:'Closed',priority:'Normal'}
    ],
    movements: [
      {text:'JRMS-2026-001 moved from Registry to Registrar',time:'Today 09:10',note:'Awaiting approval.'},
      {text:'JRMS-2026-002 routed to Research',time:'Today 08:22',note:'Need citation verification.'},
      {text:'JRMS-2026-003 archived after closure',time:'Yesterday 16:45',note:'Finalized and stored.'}
    ]
  };

  const el = id => document.getElementById(id);
  const renderSelect = (id, items, selected='') => {
    el(id).innerHTML = items.map(v => `<option ${v===selected?'selected':''}>${v}</option>`).join('');
  };
  const badge = s => `<span class="tag ${s==='Open'?'open':s==='On Hold'?'hold':'closed'}">${s}</span>`;

  function currentPayload(extra={}) {
    return {
      meta: {
        appName: state.config.appName,
        generatedAt: new Date().toISOString()
      },
      record: {
        fileNo: el('fileNo').value.trim(),
        title: el('title').value.trim(),
        originDepartment: el('originDept').value,
        currentDepartment: el('currentDept').value,
        officer: el('officer').value.trim() || 'Unassigned',
        status: el('status').value,
        priority: el('priority').value,
        dateOpened: el('dateOpened').value,
        description: el('description').value.trim(),
        remarks: el('remarks').value.trim()
      },
      integration: {
        powerAutomate: state.config.powerAutomate
      },
      ...extra
    };
  }

  function refreshConfigEditor() {
    el('configJson').value = JSON.stringify(state.config, null, 2);
  }

  function refreshPayload() {
    el('payloadJson').value = JSON.stringify(currentPayload(), null, 2);
  }

  function render() {
    const q = el('search').value.toLowerCase();
    const rows = state.cases
      .filter(c => Object.values(c).join(' ').toLowerCase().includes(q))
      .map(c => `<tr><td>${c.fileNo}</td><td>${c.title}</td><td>${c.dept}</td><td>${c.officer}</td><td>${badge(c.status)}</td><td>${c.priority}</td></tr>`)
      .join('');
    el('caseTable').innerHTML = rows || `<tr><td colspan="6" style="color:#94a3b8">No matching records.</td></tr>`;
    el('movementLog').innerHTML = state.movements
      .map(m => `<div class="item"><b>${m.text}</b><br><small>${m.time} • ${m.note}</small></div>`)
      .join('');
    const counts = {Open:0,'On Hold':0,Closed:0};
    state.cases.forEach(c => counts[c.status]++);
    el('totalFiles').textContent = state.cases.length;
    el('openFiles').textContent = counts.Open;
    el('holdFiles').textContent = counts['On Hold'];
    el('closedFiles').textContent = counts.Closed;
    refreshPayload();
  }

  function init() {
    renderSelect('priority', state.config.priorities, 'Urgent');
    renderSelect('status', state.config.statuses, 'Open');
    renderSelect('originDept', state.config.departments, 'Registry');
    renderSelect('currentDept', state.config.departments, 'Registry');
    el('dateOpened').valueAsDate = new Date();
    refreshConfigEditor();
    render();
  }

  el('caseForm').addEventListener('submit', e => {
    e.preventDefault();
    const payload = currentPayload();
    state.cases.unshift({
      fileNo: payload.record.fileNo,
      title: payload.record.title,
      dept: payload.record.currentDepartment,
      officer: payload.record.officer,
      status: payload.record.status,
      priority: payload.record.priority
    });
    state.movements.unshift({
      text: `${payload.record.fileNo} created in ${payload.record.currentDepartment}`,
      time: 'Just now',
      note: payload.record.remarks || 'New file captured.'
    });
    if (state.config.powerAutomate.enabled) {
      console.log('POST to flow:', JSON.stringify(payload, null, 2));
    }
    e.target.reset();
    renderSelect('priority', state.config.priorities, 'Normal');
    renderSelect('status', state.config.statuses, 'Open');
    renderSelect('originDept', state.config.departments, 'Registry');
    renderSelect('currentDept', state.config.departments, 'Registry');
    el('dateOpened').valueAsDate = new Date();
    render();
  });

  el('addMovement').onclick = () => {
    const p = currentPayload();
    state.movements.unshift({
      text: `${p.record.fileNo || 'File'} transferred from ${p.record.originDepartment} to ${p.record.currentDepartment}`,
      time: 'Just now',
      note: p.record.remarks || 'Movement added.'
    });
    render();
  };

  el('applyConfig').onclick = () => {
    try {
      const parsed = JSON.parse(el('configJson').value);
      state.config = parsed;
      init();
    } catch (err) {
      alert('Invalid JSON configuration. Check syntax and try again.');
    }
  };

  el('exportJson').onclick = () => {
    const blob = new Blob([JSON.stringify({
      config: state.config,
      cases: state.cases,
      movements: state.movements
    }, null, 2)], {type:'application/json'});
    const a = document.createElement('a');
    a.href = URL.createObjectURL(blob);
    a.download = 'judiciary-records-export.json';
    a.click();
    URL.revokeObjectURL(a.href);
  };

  el('copyPayload').onclick = async () => {
    try {
      await navigator.clipboard.writeText(el('payloadJson').value);
      alert('Payload copied.');
    } catch {
      alert('Copy failed.');
    }
  };

  el('resetDemo').onclick = () => location.reload();
  el('search').oninput = render;

  ['fileNo','title','originDept','currentDept','officer','status','priority','dateOpened','description','remarks']
    .forEach(id => el(id).addEventListener('input', refreshPayload));

  init();
</script>
</body>
</html>
