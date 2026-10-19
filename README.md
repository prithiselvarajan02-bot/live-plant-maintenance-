
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Live Plant Maintenance</title>
<style>
:root {
  --green: #286747;
  --light: #eaf4e9;
  --cream: #f8faf5;
  --text: #253b2d;
}
* { box-sizing: border-box; }
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: var(--cream);
  color: var(--text);
}
header {
  background: var(--green);
  color: white;
  padding: 24px 18px;
}
header h1 { margin: 0 0 8px; font-size: 25px; }
header p { margin: 0; font-size: 14px; }
nav {
  display: flex; gap: 8px; padding: 12px;
  background: white; overflow-x: auto;
  position: sticky; top: 0; z-index: 2;
  border-bottom: 1px solid #e1e9df;
}
nav a {
  color: var(--green); text-decoration: none;
  padding: 9px 12px; border-radius: 8px;
  white-space: nowrap; font-size: 13px;
  font-weight: bold;
}
nav a:hover { background: var(--light); }
main { max-width: 1050px; margin: auto; padding: 20px 14px 40px; }
h2 { font-size: 21px; margin-top: 0; }
h3 { margin: 0 0 10px; }
.muted { color: #68796b; font-size: 13px; }
.stats {
  display: grid; grid-template-columns: repeat(3, 1fr);
  gap: 12px; margin-bottom: 28px;
}
.stat, .panel, .plant-card {
  background: white; border: 1px solid #e2eae0;
  border-radius: 14px; padding: 16px;
}
.stat strong { display: block; font-size: 26px; color: var(--green); margin-top: 8px; }
.stat span { font-size: 13px; }
.section { margin: 30px 0; scroll-margin-top: 70px; }
.plant-grid {
  display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 14px;
}
.plant-icon {
  background: var(--light); border-radius: 10px;
  font-size: 46px; text-align: center; padding: 17px;
  margin-bottom: 12px;
}
.plant-card h3 { font-size: 18px; }
.tag {
  display: inline-block; padding: 5px 8px; border-radius: 20px;
  background: var(--light); color: var(--green); font-size: 12px;
  margin: 5px 0 12px;
}
button {
  background: var(--green); color: white; border: 0;
  padding: 10px 13px; border-radius: 8px; cursor: pointer;
  font-size: 13px; margin: 4px 4px 4px 0;
}
button:hover { opacity: .88; }
button.secondary { background: #e6eee5; color: var(--green); }
button.danger { background: #f8e8e4; color: #9a3e2e; }
form { display: grid; gap: 12px; }
label { display: grid; gap: 6px; font-size: 13px; font-weight: bold; }
input, select, textarea {
  width: 100%; padding: 11px; border: 1px solid #d5e0d3;
  border-radius: 8px; font: inherit; background: white;
}
.form-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
table { width: 100%; border-collapse: collapse; font-size: 13px; }
th, td { padding: 12px 8px; border-bottom: 1px solid #e4eae2; text-align: left; }
th { color: var(--green); }
.table-wrap { overflow-x: auto; }
.empty { padding: 18px 0; color: #68796b; font-size: 14px; }
footer { text-align: center; padding: 22px; color: #68796b; font-size: 12px; }
@media (max-width: 520px) {
  .stats { grid-template-columns: 1fr 1fr; }
  .stat:last-child { grid-column: span 2; }
  .form-grid { grid-template-columns: 1fr; }
  header h1 { font-size: 22px; }
}
</style>
</head>
<body>

<header>
  <h1>🌿 Live Plant Maintenance</h1>
  <p>Grow healthy plants with simple, organised care.</p>
</header>

<nav>
  <a href="#dashboard">Dashboard</a>
  <a href="#plants">My Plants</a>
  <a href="#add-plant">Add Plant</a>
  <a href="#schedule">Care Schedule</a>
  <a href="#tasks">Maintenance Tasks</a>
</nav>

<main>
  <section class="section" id="dashboard">
    <h2>Welcome to Your Green Space 🌱</h2>
    <p class="muted">Keep track of your plants and their daily care.</p>
    <div class="stats">
      <div class="stat"><span>🌱 Total Plants</span><strong id="totalPlants">0</strong></div>
      <div class="stat"><span>💧 Water Today</span><strong id="waterToday">0</strong></div>
      <div class="stat"><span>✅ Tasks Completed</span><strong id="completedTasks">0</strong></div>
    </div>
  </section>

  <section class="section" id="plants">
    <h2>My Plants</h2>
    <p class="muted">View your collection and record watering.</p>
    <div class="plant-grid" id="plantList"></div>
  </section>

  <section class="section" id="add-plant">
    <div class="panel">
      <h2>Add a New Plant</h2>
      <form id="plantForm">
        <label>Plant Name
          <input id="plantName" placeholder="e.g. Money Plant" required>
        </label>
        <div class="form-grid">
          <label>Plant Type
            <select id="plantType">
              <option>Indoor</option>
              <option>Outdoor</option>
              <option>Flowering</option>
              <option>Herb</option>
              <option>Succulent</option>
            </select>
          </label>
          <label>Plant Icon
            <select id="plantIcon">
              <option value="🪴">Potted Plant</option>
              <option value="🌵">Cactus</option>
              <option value="🌻">Sunflower</option>
              <option value="🌿">Green Leaves</option>
              <option value="🌷">Tulip</option>
              <option value="🌱">Seedling</option>
              <option value="🌴">Palm Tree</option>
            </select>
          </label>
        </div>
        <div class="form-grid">
          <label>Watering Interval (days)
            <input id="waterInterval" type="number" min="1" max="365" value="3" required>
          </label>
          <label>Last Watered
            <input id="lastWatered" type="date">
          </label>
        </div>
        <label>Plant Notes
          <textarea id="plantNotes" rows="2" placeholder="Sunlight, location or other notes"></textarea>
        </label>
        <button type="submit">＋ Add Plant</button>
      </form>
    </div>
  </section>

  <section class="section" id="schedule">
    <h2>Watering Schedule 💧</h2>
    <div class="panel table-wrap">
      <table>
        <thead><tr><th>Plant</th><th>Next Watering</th><th>Status</th></tr></thead>
        <tbody id="scheduleList"></tbody>
      </table>
    </div>
  </section>

  <section class="section" id="tasks">
    <div class="panel">
      <h2>Maintenance Tasks ✅</h2>
      <form id="taskForm">
        <label>Task Description
          <input id="taskName" placeholder="e.g. Check soil moisture" required>
        </label>
        <label>Due Date
          <input id="taskDate" type="date" required>
        </label>
        <button type="submit">＋ Add Task</button>
      </form>
      <div id="taskList" style="margin-top:18px"></div>
    </div>
  </section>
</main>

<footer>🌿 Live Plant Maintenance · Care for plants, grow a greener world.</footer>

<script>
const $ = id => document.getElementById(id);
const today = () => {
  const d = new Date();
  return `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(d.getDate()).padStart(2,'0')}`;
};
const shiftDate = (date, days) => {
  const d = new Date(date + 'T12:00:00');
  d.setDate(d.getDate() + days);
  return `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(d.getDate()).padStart(2,'0')}`;
};
const fmt = date => date ? new Date(date+'T12:00:00').toLocaleDateString() : 'Not set';
const safe = text => String(text).replace(/[&<>"']/g, c => ({
  '&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'
}[c]));

let plants = [];
let tasks = [];
try {
  plants = JSON.parse(localStorage.getItem('plantMaintenancePlants') || '[]');
  tasks = JSON.parse(localStorage.getItem('plantMaintenanceTasks') || '[]');
  if (!Array.isArray(plants)) plants = [];
  if (!Array.isArray(tasks)) tasks = [];
} catch(e) { plants = []; tasks = []; }

function save() {
  localStorage.setItem('plantMaintenancePlants', JSON.stringify(plants));
  localStorage.setItem('plantMaintenanceTasks', JSON.stringify(tasks));
  render();
}

function nextDate(p) {
  return shiftDate(p.lastWatered || today(), Number(p.interval || 3));
}

function render() {
  $('totalPlants').textContent = plants.length;
  $('waterToday').textContent = plants.filter(p => nextDate(p) <= today()).length;
  $('completedTasks').textContent = tasks.filter(t => t.done).length;

  $('plantList').innerHTML = plants.length ? plants.map(p => `
    <article class="plant-card">
      <div class="plant-icon">${safe(p.icon)}</div>
      <h3>${safe(p.name)}</h3>
      <span class="tag">${safe(p.type)}</span>
      <p class="muted">💧 Every ${p.interval} day(s)</p>
      <p class="muted">Last watered: ${fmt(p.lastWatered)}</p>
      ${p.notes ? `<p>${safe(p.notes)}</p>` : ''}
      <button onclick="waterPlant('${p.id}')">💧 Water Now</button>
      <button class="danger" onclick="deletePlant('${p.id}')">Delete</button>
    </article>`).join('') : '<p class="empty">No plants yet. Use the form below to add your first plant.</p>';

  $('scheduleList').innerHTML = plants.length ? plants.map(p => {
    const due = nextDate(p);
    const status = due < today() ? 'Overdue' : due === today() ? 'Due today' : 'Upcoming';
    return `<tr><td>${safe(p.icon)} ${safe(p.name)}</td><td>${fmt(due)}</td><td><span class="tag">${status}</span></td></tr>`;
  }).join('') : '<tr><td colspan="3">Add a plant to see its schedule.</td></tr>';

  $('taskList').innerHTML = tasks.length ? tasks.map(t => `
    <div style="padding:12px 0;border-bottom:1px solid #e4eae2">
      <label style="display:flex;align-items:center;gap:8px">
        <input type="checkbox" style="width:auto" ${t.done ? 'checked' : ''}
          onchange="toggleTask('${t.id}',this.checked)">
        <span style="font-weight:normal;${t.done ? 'text-decoration:line-through;color:#788578' : ''}">
          ${safe(t.name)} — ${fmt(t.date)}
        </span>
      </label>
      <button class="danger" onclick="deleteTask('${t.id}')">Delete task</button>
    </div>`).join('') : '<p class="empty">No tasks yet. Add a maintenance task above.</p>';
}

$('plantForm').addEventListener('submit', e => {
  e.preventDefault();
  plants.push({
    id: String(Date.now()) + Math.random().toString(16).slice(2),
    name: $('plantName').value.trim(),
    type: $('plantType').value,
    icon: $('plantIcon').value,
    interval: Number($('waterInterval').value),
    lastWatered: $('lastWatered').value || today(),
    notes: $('plantNotes').value.trim()
  });
  save();
  e.target.reset();
  $('waterInterval').value = 3;
  $('lastWatered').value = '';
  $('plants').scrollIntoView({behavior:'smooth'});
});

$('taskForm').addEventListener('submit', e => {
  e.preventDefault();
  tasks.push({
    id: String(Date.now()) + Math.random().toString(16).slice(2),
    name: $('taskName').value.trim(),
    date: $('taskDate').value,
    done: false
  });
  save();
  e.target.reset();
});

function waterPlant(id) {
  const p = plants.find(p => p.id === id);
  if (p) { p.lastWatered = today(); save(); }
}
function deletePlant(id) {
  if (confirm('Delete this plant?')) {
    plants = plants.filter(p => p.id !== id);
    save();
  }
}
function toggleTask(id, done) {
  const t = tasks.find(t => t.id === id);
  if (t) { t.done = done; save(); }
}
function deleteTask(id) {
  if (confirm('Delete this task?')) {
    tasks = tasks.filter(t => t.id !== id);
    save();
  }
}

$('lastWatered').value = today();
$('taskDate').value = today();
render();
</script>
</body>
</html>

