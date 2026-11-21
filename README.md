# digital-library-system
digital library system
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Digital Library Catalog Assessment System</title>

<style>
:root {
  --primary: #183b56;
  --accent: #2675b8;
  --bg: #f3f6fa;
  --white: #ffffff;
  --text: #263445;
  --muted: #64748b;
  --border: #dce4ed;
  --red: #c0392b;
  --green: #18845b;
}
* { box-sizing: border-box; }
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: var(--bg);
  color: var(--text);
}
button, input, select { font: inherit; }
button { cursor: pointer; }
.hidden { display: none !important; }

.login-page {
  min-height: 100vh;
  display: grid;
  place-items: center;
  padding: 20px;
}
.login-card {
  background: white;
  width: 100%;
  max-width: 400px;
  padding: 30px;
  border-radius: 14px;
  box-shadow: 0 8px 30px #183b5618;
}
.login-card h1 { color: var(--primary); }
input, select {
  width: 100%;
  padding: 11px;
  border: 1px solid var(--border);
  border-radius: 7px;
  margin: 6px 0 14px;
}
button {
  border: 0;
  border-radius: 7px;
  padding: 10px 14px;
}
.primary { background: var(--accent); color: white; }
.secondary { background: #e8eef5; color: var(--primary); }
.danger { background: #fce8e6; color: var(--red); }
.success { background: #dcfce7; color: #166534; }

.app { display: flex; min-height: 100vh; }
.sidebar {
  width: 245px;
  background: var(--primary);
  color: white;
  padding: 24px 14px;
  flex-shrink: 0;
}
.brand { font-size: 20px; font-weight: bold; margin: 0 8px 30px; }
.nav-button {
  display: block;
  width: 100%;
  text-align: left;
  margin: 6px 0;
  background: transparent;
  color: #e5edf5;
}
.nav-button:hover, .nav-button.active {
  background: #ffffff20;
}
.main { flex: 1; min-width: 0; }
.topbar {
  background: white;
  padding: 18px 25px;
  border-bottom: 1px solid var(--border);
  display: flex;
  justify-content: space-between;
  gap: 12px;
  align-items: center;
}
.content { padding: 25px; max-width: 1400px; margin: auto; }
h1, h2, h3 { margin-top: 0; }
.muted { color: var(--muted); }
.cards {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 16px;
  margin: 22px 0;
}
.card, .panel {
  background: white;
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 20px;
}
.card p { color: var(--muted); margin-bottom: 8px; }
.metric { font-size: 30px; font-weight: bold; color: var(--primary); }
.toolbar {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-bottom: 16px;
}
.toolbar input, .toolbar select {
  flex: 1;
  min-width: 170px;
  margin: 0;
}
.table-wrap { overflow-x: auto; }
table {
  width: 100%;
  border-collapse: collapse;
  background: white;
}
th, td {
  padding: 12px;
  border-bottom: 1px solid var(--border);
  text-align: left;
  font-size: 14px;
}
th { background: #edf2f7; }
td button { margin: 2px; }
.badge {
  display: inline-block;
  padding: 5px 8px;
  border-radius: 20px;
  font-size: 12px;
  background: #fef3c7;
}
.badge.resolved { background: #dcfce7; color: #166534; }
.badge.open { background: #fee2e2; color: #991b1b; }
.notice { margin: 12px 0; padding: 12px; border-radius: 7px; }
.notice.error { background: #fee2e2; color: #991b1b; }
.notice.info { background: #dbeafe; color: #1e40af; }
.form-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 12px;
}
.form-grid label { font-size: 14px; font-weight: bold; }
.form-grid input { display: block; }
footer { color: var(--muted); padding: 20px 0; font-size: 12px; }

@media (max-width: 850px) {
  .app { display: block; }
  .sidebar { width: 100%; padding: 14px; }
  .brand { margin-bottom: 12px; }
  .nav-button { display: inline-block; width: auto; }
  .cards { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .content { padding: 16px; }
}
@media (max-width: 480px) {
  .cards, .form-grid { grid-template-columns: 1fr; }
  .topbar { padding: 14px; }
}
@media print {
  .sidebar, .topbar button, .toolbar, .no-print, footer {
    display: none !important;
  }
  .app { display: block; }
  .content { padding: 0; }
  body { background: white; }
}
</style>
</head>

<body>

<!-- LOGIN -->
<section id="loginPage" class="login-page">
  <div class="login-card">
    <h1>Digital Library</h1>
    <p class="muted">Catalog Assessment System</p>
    <div id="loginMessage"></div>
    <form id="loginForm">
      <label for="username">Username</label>
      <input id="username" required placeholder="Enter username">
      <label for="password">Password</label>
      <input id="password" type="password" required placeholder="Enter password">
      <button class="primary" style="width:100%">Login</button>
    </form>
    <p class="muted">Demo login: admin / admin123</p>
    <p class="muted" style="font-size:12px">
      Demonstration only. This login does not provide real security.
    </p>
  </div>
</section>

<!-- MAIN APPLICATION -->
<div id="app" class="app hidden">
  <aside class="sidebar">
    <div class="brand">📚 Digital Library</div>
    <button class="nav-button active" data-page="dashboard">Dashboard</button>
    <button class="nav-button" data-page="catalog">Catalog Management</button>
    <button class="nav-button" data-page="scan">Anomaly Detection</button>
    <button class="nav-button" data-page="issues">Resolve Anomalies</button>
    <button class="nav-button" data-page="reports">Reports</button>
  </aside>

  <main class="main">
    <header class="topbar">
      <strong id="pageHeading">Dashboard</strong>
      <button class="secondary" id="logoutButton">Logout</button>
    </header>
    <div class="content">

      <!-- DASHBOARD -->
      <section id="dashboard" class="page">
        <h1>Dashboard</h1>
        <p class="muted">Overview of digital library catalog quality.</p>
        <div class="cards">
          <div class="card">
            <p>Total records</p><div class="metric" id="totalRecords">0</div>
          </div>
          <div class="card">
            <p>Issues detected</p><div class="metric" id="totalIssues">0</div>
          </div>
          <div class="card">
            <p>Open issues</p><div class="metric" id="openIssues">0</div>
          </div>
          <div class="card">
            <p>Resolved issues</p><div class="metric" id="resolvedIssues">0</div>
          </div>
        </div>
        <div class="panel">
          <h2>Recent catalog records</h2>
          <div class="table-wrap">
            <table>
              <thead>
                <tr><th>Title</th><th>Author</th><th>ISBN</th></tr>
              </thead>
              <tbody id="recentRecords"></tbody>
            </table>
          </div>
        </div>
      </section>

      <!-- CATALOG -->
      <section id="catalog" class="page hidden">
        <h1>Catalog Management</h1>
        <p class="muted">Search, add and edit bibliographic records.</p>

        <div class="panel">
          <h3 id="formHeading">Add a catalog record</h3>
          <form id="bookForm">
            <input type="hidden" id="recordId">
            <div class="form-grid">
              <label>Book ID
                <input id="bookId" placeholder="e.g. BK001" required>
              </label>
              <label>Book title
                <input id="title" placeholder="Enter title" required>
              </label>
              <label>Author
                <input id="author" placeholder="Enter author" required>
              </label>
              <label>ISBN
                <input id="isbn" placeholder="Enter ISBN" required>
              </label>
              <label>Publication year
                <input id="year" type="number" min="1000" max="9999"
                  placeholder="e.g. 2024">
              </label>
            </div>
            <button class="primary" id="saveBookButton">Save record</button>
            <button class="secondary" type="button" id="cancelEdit">Clear</button>
          </form>
          <div id="bookMessage"></div>
        </div>

        <div class="panel" style="margin-top:18px">
          <div class="toolbar">
            <input id="searchBooks" placeholder="Search title, author, ISBN or ID">
          </div>
          <div class="table-wrap">
            <table>
              <thead>
                <tr>
                  <th>Book ID</th><th>Title</th><th>Author</th>
                  <th>ISBN</th><th>Year</th><th>Actions</th>
                </tr>
              </thead>
              <tbody id="bookRows"></tbody>
            </table>
          </div>
        </div>
      </section>

      <!-- ANOMALY SCAN -->
      <section id="scan" class="page hidden">
        <h1>Anomaly Detection</h1>
        <p class="muted">
          Check records for missing fields, duplicate ISBNs and invalid values.
        </p>
        <div class="panel">
          <h3>Catalog quality scan</h3>
          <p>Run the scan to identify possible catalog data problems.</p>
          <button class="primary" id="scanButton">Scan catalog records</button>
          <div id="scanMessage"></div>
        </div>
        <div class="panel" style="margin-top:18px">
          <h3>Latest scan results</h3>
          <p class="muted">Run a new scan to refresh the detected issues.</p>
          <div class="table-wrap">
            <table>
              <thead>
                <tr><th>Book ID</th><th>Title</th><th>Issue</th><th>Status</th></tr>
              </thead>
              <tbody id="scanRows"></tbody>
            </table>
          </div>
        </div>
      </section>

      <!-- RESOLUTION -->
      <section id="issues" class="page hidden">
        <h1>Anomaly Resolution</h1>
        <p class="muted">Review detected issues and track their resolution.</p>
        <div class="toolbar">
          <select id="issueFilter">
            <option value="all">All issues</option>
            <option value="Open">Open issues</option>
            <option value="Resolved">Resolved issues</option>
          </select>
        </div>
        <div class="panel">
          <div class="table-wrap">
            <table>
              <thead>
                <tr>
                  <th>Book ID</th><th>Issue</th><th>Description</th>
                  <th>Status</th><th>Action</th>
                </tr>
              </thead>
              <tbody id="issueRows"></tbody>
            </table>
          </div>
        </div>
      </section>

      <!-- REPORTS -->
      <section id="reports" class="page hidden">
        <h1>Assessment Reports</h1>
        <p class="muted">Summary of the latest anomaly assessment.</p>
        <div class="cards">
          <div class="card"><p>Records assessed</p>
            <div class="metric" id="reportRecords">0</div></div>
          <div class="card"><p>Issues detected</p>
            <div class="metric" id="reportIssues">0</div></div>
          <div class="card"><p>Open issues</p>
            <div class="metric" id="reportOpen">0</div></div>
          <div class="card"><p>Resolved issues</p>
            <div class="metric" id="reportResolved">0</div></div>
        </div>
        <div class="panel">
          <h3>Issues by type</h3>
          <div class="table-wrap">
            <table>
              <thead><tr><th>Issue type</th><th>Count</th></tr></thead>
              <tbody id="reportTypes"></tbody>
            </table>
          </div>
          <p id="reportDate" class="muted"></p>
          <button class="primary no-print" id="printReport">Print report</button>
        </div>
      </section>

      <footer>
        Digital Library Catalog Assessment System · Academic project prototype
      </footer>
    </div>
  </main>
</div>

<script>
// ==========================================
// 1. SAMPLE DATA AND LOCAL STORAGE
// ==========================================

const SAMPLE_BOOKS = [
  {id:"1", bookId:"BK001", title:"Introduction to Computing",
   author:"Peter Norton", isbn:"9780133591620", year:"2022"},
  {id:"2", bookId:"BK002", title:"Database Systems",
   author:"Thomas Connolly", isbn:"9780132943260", year:"2021"},
  {id:"3", bookId:"BK003", title:"Computer Networks",
   author:"Andrew Tanenbaum", isbn:"9780132126953", year:"2020"}
];

function loadData(key, fallback) {
  try {
    const value = localStorage.getItem(key);
    return value ? JSON.parse(value) : fallback;
  } catch (error) {
    return fallback;
  }
}

let books = loadData("library_books", SAMPLE_BOOKS);
let issues = loadData("library_issues", []);
let lastScan = loadData("library_last_scan", null);

function saveData() {
  localStorage.setItem("library_books", JSON.stringify(books));
  localStorage.setItem("library_issues", JSON.stringify(issues));
  localStorage.setItem("library_last_scan", JSON.stringify(lastScan));
}

function escapeHTML(value) {
  return String(value ?? "").replace(/[&<>"']/g, char => ({
    "&":"&amp;", "<":"&lt;", ">":"&gt;",
    '"':"&quot;", "'":"&#39;"
  })[char]);
}

function showMessage(elementId, message, type="info") {
  document.getElementById(elementId).innerHTML =
    `<div class="notice ${type}">${escapeHTML(message)}</div>`;
}

// ==========================================
// 2. DEMO LOGIN
// ==========================================

document.getElementById("loginForm").addEventListener("submit", event => {
  event.preventDefault();

  const username = document.getElementById("username").value.trim();
  const password = document.getElementById("password").value;

  if (username === "admin" && password === "admin123") {
    sessionStorage.setItem("library_demo_login", "true");
    document.getElementById("loginPage").classList.add("hidden");
    document.getElementById("app").classList.remove("hidden");
    renderAll();
  } else {
    showMessage("loginMessage", "Invalid username or password.", "error");
  }
});

function logout() {
  sessionStorage.removeItem("library_demo_login");
  document.getElementById("app").classList.add("hidden");
  document.getElementById("loginPage").classList.remove("hidden");
  document.getElementById("loginForm").reset();
}

document.getElementById("logoutButton").addEventListener("click", logout);

// ==========================================
// 3. PAGE NAVIGATION
// ==========================================

const pageNames = {
  dashboard:"Dashboard",
  catalog:"Catalog Management",
  scan:"Anomaly Detection",
  issues:"Anomaly Resolution",
  reports:"Assessment Reports"
};

function showPage(page) {
  document.querySelectorAll(".page").forEach(section => {
    section.classList.toggle("hidden", section.id !== page);
  });

  document.querySelectorAll(".nav-button").forEach(button => {
    button.classList.toggle("active", button.dataset.page === page);
  });

  document.getElementById("pageHeading").textContent = pageNames[page];
  renderAll();
}

document.querySelectorAll(".nav-button").forEach(button => {
  button.addEventListener("click", () => showPage(button.dataset.page));
});

// ==========================================
// 4. CATALOG MANAGEMENT
// ==========================================

const bookForm = document.getElementById("bookForm");

bookForm.addEventListener("submit", event => {
  event.preventDefault();

  const id = document.getElementById("recordId").value;
  const book = {
    id: id || String(Date.now()),
    bookId: document.getElementById("bookId").value.trim(),
    title: document.getElementById("title").value.trim(),
    author: document.getElementById("author").value.trim(),
    isbn: document.getElementById("isbn").value.trim(),
    year: document.getElementById("year").value.trim()
  };

  const duplicateId = books.some(existing =>
    existing.bookId.toLowerCase() === book.bookId.toLowerCase()
    && existing.id !== id
  );

  if (duplicateId) {
    showMessage("bookMessage", "That Book ID already exists.", "error");
    return;
  }

  if (id) {
    books = books.map(existing => existing.id === id ? book : existing);
    // Re-scan after edits so issue records reflect current catalog data.
    lastScan = null;
    showMessage("bookMessage", "Record updated successfully.");
  } else {
    books.push(book);
    lastScan = null;
    showMessage("bookMessage", "Record added successfully.");
  }

  saveData();
  clearBookForm();
  renderAll();
});

function editBook(id) {
  const book = books.find(item => item.id === id);
  if (!book) return;

  document.getElementById("recordId").value = book.id;
  document.getElementById("bookId").value = book.bookId;
  document.getElementById("title").value = book.title;
  document.getElementById("author").value = book.author;
  document.getElementById("isbn").value = book.isbn;
  document.getElementById("year").value = book.year;

  document.getElementById("formHeading").textContent = "Edit catalog record";
  document.getElementById("saveBookButton").textContent = "Update record";
  window.scrollTo({top:0, behavior:"smooth"});
}

function deleteBook(id) {
  if (!confirm("Delete this catalog record?")) return;
  books = books.filter(book => book.id !== id);
  lastScan = null;
  saveData();
  renderAll();
}

function clearBookForm() {
  bookForm.reset();
  document.getElementById("recordId").value = "";
  document.getElementById("formHeading").textContent = "Add a catalog record";
  document.getElementById("saveBookButton").textContent = "Save record";
}

document.getElementById("cancelEdit").addEventListener("click", clearBookForm);

document.getElementById("searchBooks").addEventListener("input", renderBooks);

function renderBooks() {
  const query = document.getElementById("searchBooks").value.toLowerCase();

  const filtered = books.filter(book =>
    [book.bookId, book.title, book.author, book.isbn, book.year]
      .some(value => String(value).toLowerCase().includes(query))
  );

  document.getElementById("bookRows").innerHTML = filtered.map(book => `
    <tr>
      <td>${escapeHTML(book.bookId)}</td>
      <td>${escapeHTML(book.title)}</td>
      <td>${escapeHTML(book.author)}</td>
      <td>${escapeHTML(book.isbn)}</td>
      <td>${escapeHTML(book.year)}</td>
      <td>
        <button class="secondary" onclick="editBook('${book.id}')">Edit</button>
        <button class="danger" onclick="deleteBook('${book.id}')">Delete</button>
      </td>
    </tr>
  `).join("") || `<tr><td colspan="6">No records found.</td></tr>`;
}

// ==========================================
// 5. ANOMALY DETECTION
// ==========================================

// Checks ISBN format and checksum for ISBN-10 and ISBN-13.
function validISBN(value) {
  const isbn = String(value || "").replace(/[-\s]/g, "");

  if (/^\d{13}$/.test(isbn)) {
    let sum = 0;
    for (let i = 0; i < 13; i++) {
      sum += Number(isbn[i]) * (i % 2 === 0 ? 1 : 3);
    }
    return sum % 10 === 0;
  }

  if (/^\d{9}[\dX]$/.test(isbn)) {
    let sum = 0;
    for (let i = 0; i < 10; i++) {
      const digit = isbn[i] === "X" ? 10 : Number(isbn[i]);
      sum += digit * (10 - i);
    }
    return sum % 11 === 0;
  }

  return false;
}

function scanCatalog() {
  const found = [];

  function addIssue(book, type, description) {
    found.push({
      key: `${book.id}|${type}`,
      id: book.id,
      bookId: book.bookId || "(missing)",
      title: book.title || "(untitled)",
      type,
      description,
      status: "Open"
    });
  }

  const isbnCounts = {};

  books.forEach(book => {
    const isbn = String(book.isbn || "").replace(/[-\s]/g, "");
    if (isbn) {
      isbnCounts[isbn] = (isbnCounts[isbn] || 0) + 1;
    }
  });

  books.forEach(book => {
    if (!book.bookId.trim()) {
      addIssue(book, "Missing Book ID", "Book ID is empty.");
    }
    if (!book.title.trim()) {
      addIssue(book, "Missing title", "Book title is empty.");
    }
    if (!book.author.trim()) {
      addIssue(book, "Missing author", "Author field is empty.");
    }
    if (!book.isbn.trim()) {
      addIssue(book, "Missing ISBN", "ISBN field is empty.");
    } else {
      const isbn = book.isbn.replace(/[-\s]/g, "");
      if (!validISBN(isbn)) {
        addIssue(book, "Invalid ISBN", "ISBN format or checksum is invalid.");
      }
      if (isbnCounts[isbn] > 1) {
        addIssue(book, "Duplicate ISBN", "This ISBN occurs in multiple records.");
      }
    }

    if (book.year) {
      const year = Number(book.year);
      if (!Number.isInteger(year) || year < 1000 ||
          year > new Date().getFullYear()) {
        addIssue(book, "Invalid publication year",
          "Publication year is outside the permitted range.");
      }
    }
  });

  // Preserve the resolution status of issues that still exist.
  const previous = new Map(issues.map(issue => [issue.key, issue]));
  issues = found.map(issue => ({
    ...issue,
    status: previous.get(issue.key)?.status || "Open"
  }));

  lastScan = new Date().toISOString();
  saveData();
  renderAll();

  showMessage("scanMessage",
    `Scan complete. ${issues.length} issue(s) detected.`, "info");
}

document.getElementById("scanButton").addEventListener("click", scanCatalog);

// ==========================================
// 6. ANOMALY RESOLUTION
// ==========================================

function resolveIssue(key) {
  issues = issues.map(issue =>
    issue.key === key ? {...issue, status:"Resolved"} : issue
  );
  saveData();
  renderAll();
}

function reopenIssue(key) {
  issues = issues.map(issue =>
    issue.key === key ? {...issue, status:"Open"} : issue
  );
  saveData();
  renderAll();
}

document.getElementById("issueFilter").addEventListener("change", renderIssues);

function renderIssues() {
  const filter = document.getElementById("issueFilter").value;
  const filtered = issues.filter(issue =>
    filter === "all" || issue.status === filter
  );

  document.getElementById("issueRows").innerHTML = filtered.map(issue => `
    <tr>
      <td>${escapeHTML(issue.bookId)}</td>
      <td>${escapeHTML(issue.type)}</td>
      <td>${escapeHTML(issue.description)}</td>
      <td><span class="badge ${issue.status === "Resolved" ? "resolved":"open"}">
        ${escapeHTML(issue.status)}
      </span></td>
      <td>
        ${issue.status === "Open"
          ? `<button class="success" onclick="resolveIssue('${issue.key}')">Resolve</button>`
          : `<button class="secondary" onclick="reopenIssue('${issue.key}')">Reopen</button>`}
      </td>
    </tr>
  `).join("") || `<tr><td colspan="5">No issues to display. Run a scan first.</td></tr>`;
}

// ==========================================
// 7. DASHBOARD AND REPORTS
// ==========================================

function renderDashboard() {
  document.getElementById("totalRecords").textContent = books.length;
  document.getElementById("totalIssues").textContent = issues.length;
  document.getElementById("openIssues").textContent =
    issues.filter(issue => issue.status === "Open").length;
  document.getElementById("resolvedIssues").textContent =
    issues.filter(issue => issue.status === "Resolved").length;

  document.getElementById("recentRecords").innerHTML =
    books.slice(-5).reverse().map(book => `
      <tr>
        <td>${escapeHTML(book.title)}</td>
        <td>${escapeHTML(book.author)}</td>
        <td>${escapeHTML(book.isbn)}</td>
      </tr>
    `).join("") || `<tr><td colspan="3">No catalog records yet.</td></tr>`;
}

function renderReports() {
  const open = issues.filter(issue => issue.status === "Open").length;
  const resolved = issues.filter(issue => issue.status === "Resolved").length;

  document.getElementById("reportRecords").textContent =
    lastScan ? books.length : "—";
  document.getElementById("reportIssues").textContent =
    lastScan ? issues.length : "—";
  document.getElementById("reportOpen").textContent =
    lastScan ? open : "—";
  document.getElementById("reportResolved").textContent =
    lastScan ? resolved : "—";

  const counts = {};
  issues.forEach(issue => {
    counts[issue.type] = (counts[issue.type] || 0) + 1;
  });

  document.getElementById("reportTypes").innerHTML =
    Object.entries(counts).map(([type, count]) => `
      <tr><td>${escapeHTML(type)}</td><td>${count}</td></tr>
    `).join("") || `<tr><td colspan="2">No scan results available.</td></tr>`;

  document.getElementById("reportDate").textContent =
    lastScan ? "Last scan: " + new Date(lastScan).toLocaleString()
             : "Run an anomaly scan before generating an assessment report.";
}

document.getElementById("printReport").addEventListener("click", () => {
  if (!lastScan) {
    alert("Please scan the catalog before printing the report.");
    return;
  }
  window.print();
});

// ==========================================
// 8. RENDER APPLICATION
// ==========================================

function renderAll() {
  renderDashboard();
  renderBooks();
  renderIssues();
  renderReports();

  document.getElementById("scanRows").innerHTML =
    issues.map(issue => `
      <tr>
        <td>${escapeHTML(issue.bookId)}</td>
        <td>${escapeHTML(issue.title)}</td>
        <td>${escapeHTML(issue.type)}</td>
        <td><span class="badge ${issue.status === "Resolved" ? "resolved":"open"}">
          ${escapeHTML(issue.status)}
        </span></td>
      </tr>
    `).join("") || `<tr><td colspan="4">No scan results. Run a scan.</td></tr>`;
}

// Restore the demo session after refreshing the page.
if (sessionStorage.getItem("library_demo_login") === "true") {
  document.getElementById("loginPage").classList.add("hidden");
  document.getElementById("app").classList.remove("hidden");
  renderAll();
}
</script>

</body>
</html>
