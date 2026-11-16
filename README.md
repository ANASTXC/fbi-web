
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FBI RP Management</title>

<style>
* { box-sizing: border-box; }

body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: #0b1220;
    color: #fff;
}

header {
    background: #101e32;
    padding: 20px;
    text-align: center;
    border-bottom: 3px solid #c6a343;
}

header h1 {
    margin: 0;
    color: #d5b45b;
    letter-spacing: 3px;
}

header p { color: #9caec3; }

.layout {
    display: flex;
    min-height: 100vh;
}

nav {
    width: 230px;
    background: #111d30;
    padding: 20px;
}

nav button {
    width: 100%;
    padding: 13px;
    margin: 5px 0;
    background: #1c304b;
    color: white;
    border: 0;
    text-align: left;
    cursor: pointer;
    border-radius: 5px;
}

nav button:hover, nav button.active {
    background: #b38c36;
    color: #101820;
}

main {
    flex: 1;
    padding: 30px;
    min-width: 0;
}

.page { display: none; }
.page.active { display: block; }

h2 { color: #d5b45b; }

.cards {
    display: grid;
    grid-template-columns: repeat(auto-fit,minmax(160px,1fr));
    gap: 15px;
}

.card {
    background: #172840;
    border: 1px solid #304761;
    padding: 20px;
    border-radius: 8px;
}

.card strong {
    font-size: 28px;
    color: #d5b45b;
}

form {
    background: #172840;
    padding: 20px;
    border-radius: 8px;
    max-width: 600px;
}

input, select, textarea {
    width: 100%;
    padding: 12px;
    margin: 8px 0 15px;
    background: #0b1728;
    border: 1px solid #435773;
    color: white;
    border-radius: 5px;
}

label { color: #c3d0df; }

.action {
    background: #b38c36;
    color: #111;
    padding: 12px 18px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-weight: bold;
}

.delete {
    background: #a93636;
    color: white;
    border: 0;
    padding: 7px;
    cursor: pointer;
    border-radius: 4px;
}

table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
    background: #172840;
}

th, td {
    padding: 12px;
    border: 1px solid #344a64;
    text-align: left;
}

th { color: #d5b45b; }

.notice {
    color: #aebdd0;
    font-size: 12px;
    margin-top: 25px;
}

@media(max-width:700px) {
    .layout { flex-direction: column; }
    nav { width: 100%; display: grid; grid-template-columns: 1fr 1fr; }
    main { padding: 15px; }
}
</style>
</head>

<body>

<header>
    <h1>FEDERAL BUREAU OF INVESTIGATION</h1>
    <p>FBI ROLEPLAY MANAGEMENT SYSTEM</p>
    <small>FICTIONAL ROLEPLAY INTERFACE — NOT AN OFFICIAL FBI SYSTEM</small>
</header>

<div class="layout">

<nav>
    <button class="active" onclick="showPage('dashboard',this)">Dashboard</button>
    <button onclick="showPage('roster',this)">Roster</button>
    <button onclick="showPage('citation',this)">Citations</button>
    <button onclick="showPage('arrest',this)">Arrestations</button>
    <button onclick="showPage('wanted',this)">Wanted List</button>
    <button onclick="showPage('cases',this)">Case Files</button>
    <button onclick="showPage('reports',this)">Reports</button>
</nav>

<main>

<section id="dashboard" class="page active">
    <h2>Dashboard</h2>
    <div class="cards">
        <div class="card">Agents<br><strong id="countAgents">0</strong></div>
        <div class="card">Citations<br><strong id="countCitations">0</strong></div>
        <div class="card">Arrestations<br><strong id="countArrests">0</strong></div>
        <div class="card">Dossiers<br><strong id="countCases">0</strong></div>
        <div class="card">Wanted<br><strong id="countWanted">0</strong></div>
    </div>
    <p class="notice">Toutes les données sont destinées à un serveur de jeu de rôle.</p>
</section>

<section id="roster" class="page">
    <h2>FBI Roster</h2>
    <form onsubmit="addRecord(event,'roster')">
        <label>Nom de l'agent</label>
        <input name="name" required>
        <label>Matricule RP</label>
        <input name="badge" required>
        <label>Grade</label>
        <select name="rank">
            <option>Director</option>
            <option>Deputy Director</option>
            <option>Assistant Director</option>
            <option>Special Agent in Charge</option>
            <option>Supervisory Special Agent</option>
            <option>Senior Special Agent</option>
            <option>Special Agent</option>
            <option>Junior Special Agent</option>
            <option>Trainee</option>
        </select>
        <button class="action">Ajouter l'agent</button>
    </form>
    <div id="rosterList"></div>
</section>

<section id="citation" class="page">
    <h2>Web Citation – RP</h2>
    <form onsubmit="addRecord(event,'citations')">
        <label>Nom du citoyen</label>
        <input name="name" required>
        <label>Agent responsable</label>
        <input name="agent" required>
        <label>Infraction RP</label>
        <textarea name="reason" required></textarea>
        <label>Montant de l'amende ($)</label>
        <input name="amount" type="number" min="0" required>
        <label>Date</label>
        <input name="date" type="date" required>
        <button class="action">Générer la citation</button>
    </form>
    <div id="citationsList"></div>
</section>

<section id="arrest" class="page">
    <h2>Arrestation Report – RP</h2>
    <form onsubmit="addRecord(event,'arrests')">
        <label>Nom du suspect</label>
        <input name="name" required>
        <label>Agent responsable</label>
        <input name="agent" required>
        <label>Motif RP</label>
        <textarea name="reason" required></textarea>
        <label>Durée de peine RP (minutes)</label>
        <input name="sentence" type="number" min="0">
        <button class="action">Créer le rapport</button>
    </form>
    <div id="arrestsList"></div>
</section>

<section id="wanted" class="page">
    <h2>Wanted List – RP</h2>
    <form onsubmit="addRecord(event,'wanted')">
        <label>Nom du suspect</label>
        <input name="name" required>
        <label>Motif RP</label>
        <textarea name="reason" required></textarea>
        <label>Niveau de recherche</label>
        <select name="level">
            <option>Low</option>
            <option>Medium</option>
            <option>High</option>
            <option>Critical</option>
        </select>
        <button class="action">Ajouter à la liste</button>
    </form>
    <div id="wantedList"></div>
</section>

<section id="cases" class="page">
    <h2>Case Files – RP</h2>
    <form onsubmit="addRecord(event,'cases')">
        <label>Titre du dossier</label>
        <input name="name" required>
        <label>Agent responsable</label>
        <input name="agent" required>
        <label>Description</label>
        <textarea name="reason" required></textarea>
        <label>Statut</label>
        <select name="status">
            <option>Open</option>
            <option>Under Investigation</option>
            <option>Closed</option>
        </select>
        <button class="action">Créer le dossier</button>
    </form>
    <div id="casesList"></div>
</section>

<section id="reports" class="page">
    <h2>Agent Reports – RP</h2>
    <form onsubmit="addRecord(event,'reports')">
        <label>Nom de l'agent</label>
        <input name="agent" required>
        <label>Titre du rapport</label>
        <input name="name" required>
        <label>Contenu du rapport</label>
        <textarea name="reason" required></textarea>
        <button class="action">Envoyer le rapport</button>
    </form>
    <div id="reportsList"></div>
</section>

</main>
</div>

<script>
const types = [
    'roster','citations','arrests',
    'wanted','cases','reports'
];

let data = {};
types.forEach(type => data[type] = []);

function showPage(id,button) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');

    document.querySelectorAll('nav button').forEach(b => b.classList.remove('active'));
    button.classList.add('active');
}

function addRecord(event,type) {
    event.preventDefault();

    const form = event.target;
    const record = Object.fromEntries(new FormData(form).entries());

    record.id = Date.now();
    data[type].push(record);

    form.reset();
    render();
}

function escapeHTML(value) {
    return String(value ?? '').replace(/[&<>"']/g, char => ({
        '&':'&amp;',
        '<':'&lt;',
        '>':'&gt;',
        '"':'&quot;',
        "'":'&#39;'
    })[char]);
}

function render() {
    types.forEach(type => {
        const container = document.getElementById(type + 'List');

        container.innerHTML = `
        <table>
        <thead><tr><th>Informations</th><th>Action</th></tr></thead>
        <tbody>
        ${data[type].map(item => `
            <tr>
                <td>${Object.entries(item)
                    .filter(([key]) => key !== 'id')
                    .map(([key,value]) => `<b>${escapeHTML(key)}:</b> ${escapeHTML(value)}`)
                    .join('<br>')}</td>
                <td><button class="delete" onclick="removeRecord('${type}',${item.id})">Supprimer</button></td>
            </tr>
        `).join('')}
        </tbody>
        </table>`;
    });

    document.getElementById('countAgents').textContent = data.roster.length;
    document.getElementById('countCitations').textContent = data.citations.length;
    document.getElementById('countArrests').textContent = data.arrests.length;
    document.getElementById('countCases').textContent = data.cases.length;
    document.getElementById('countWanted').textContent = data.wanted.length;
}

function removeRecord(type,id) {
    data[type] = data[type].filter(item => item.id !== id);
    render();
}

render();
</script>

</body>
</html>
