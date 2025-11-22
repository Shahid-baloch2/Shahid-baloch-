
<!DOCTYPE html>
<html>
<head>
  <title>Shahid Baloch - Crypto Mining Apps</title>
  <style>
    body {
      margin: 0;
      padding: 15px;
      font-family: Arial, sans-serif;
      background: #0f1724;
      color: white;
    }

    h1 {
      text-align: center;
      margin-bottom: 20px;
      color: #00ffd5;
    }

    .apps {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
      gap: 15px;
    }

    .app-card {
      background: #1e293b;
      border-radius: 10px;
      padding: 10px;
      text-align: center;
      box-shadow: 0 5px 15px rgba(0,0,0,0.5);
      transition: 0.3s;
    }

    .app-card:hover {
      transform: translateY(-5px);
    }

    .app-card img {
      width: 100%;
      height: 120px;
      object-fit: cover;
      border-radius: 8px;
    }

    .app-card h3 {
      margin: 8px 0 5px;
      font-size: 16px;
    }

    .app-card p {
      font-size: 13px;
      color: #b0d7ff;
      min-height: 40px;
    }

    .app-card a {
      display: block;
      margin-top: 8px;
      padding: 8px;
      background: #00ffd5;
      color: black;
      text-decoration: none;
      border-radius: 5px;
      font-weight: bold;
    }

    .app-card a:hover {
      background: #00c8b0;
    }

    .empty {
      text-align:center;
      margin-top:50px;
      color:#aaa;
    }
  </style>
</head>
<body>

<h1>Shahid Baloch</h1>

<div class="apps" id="appsContainer"></div>

<script>
function loadApps() {
  let container = document.getElementById("appsContainer");
  container.innerHTML = "";

  let apps = JSON.parse(localStorage.getItem("miningApps")) || [];

  if (apps.length === 0) {
    container.innerHTML = "<div class='empty'>ابھی کوئی Mining App موجود نہیں</div>";
    return;
  }

  apps.forEach(app => {
    let div = document.createElement("div");
    div.className = "app-card";

    div.innerHTML = `
      <img src="${app.image}" onerror="this.src='https://via.placeholder.com/300x150?text=No+Image'">
      <h3>${app.title || app.name}</h3>
      <p>${app.description || ""}</p>
      <a href="${app.link}" target="_blank">Open App</a>
    `;

    container.appendChild(div);
  });
}

// Initial load
loadApps();

// Auto refresh when admin updates
window.addEventListener("storage", function(event) {
  if (event.key === "miningApps_updated_at") {
    loadApps();
  }
});
</script>

</body>
</html>
