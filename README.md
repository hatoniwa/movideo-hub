<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<title>MOVIDEO Access Dashboard</title>
<style>
  body {
    background: #111; color: #fff;
    font-family: system-ui, sans-serif;
    padding: 20px;
  }
  table {
    width: 100%; border-collapse: collapse;
    margin-top: 20px;
  }
  th, td {
    border-bottom: 1px solid #555;
    padding: 10px;
  }
  th { color: #ffd54a; }
</style>
</head>
<body>

<h1>MOVIDEO — Access Dashboard</h1>
<p>Latest access counts for your games:</p>

<table>
  <thead>
    <tr><th>Game ID</th><th>Access Count</th><th>Last Access</th></tr>
  </thead>
  <tbody id="counterRows"></tbody>
</table>

<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js"></script>

<script>
  const firebaseConfig = {
    apiKey: "AIzaSyAF_uyMNSXucv75qdR01ron3eWlkIps0lo",
    authDomain: "movideo-web.firebaseapp.com",
    projectId: "movideo-web",
    storageBucket: "movideo-web.firebasestorage.app",
    messagingSenderId: "328585718940",
    appId: "1:328585718940:web:8870831f0755b41825d159",
    measurementId: "G-MB78677VDD"
  };

  firebase.initializeApp(firebaseConfig);
  const db = firebase.firestore();

  db.collection("counters").onSnapshot(snapshot => {
    const rows = document.getElementById("counterRows");
    rows.innerHTML = "";
    snapshot.forEach(doc => {
      const data = doc.data();
      rows.innerHTML += `
        <tr>
          <td>${doc.id}</td>
          <td>${data.count || 0}</td>
          <td>${data.lastAccess ? data.lastAccess.toDate().toLocaleString() : "-"}</td>
        </tr>
      `;
    });
  });
</script>

</body>
</html>
