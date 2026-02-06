# sqwazzy-proxy
unblockable proxy
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sqwazzy Proxy</title>

<style>
body {
  margin: 0;
  font-family: system-ui, Arial, sans-serif;
  background: #0f172a;
  color: white;
  display: flex;
  justify-content: center;
  padding: 40px 20px;
}

.app {
  width: 100%;
  max-width: 800px;
}

h1 {
  color: #38bdf8;
}

.controls {
  display: flex;
  gap: 10px;
}

input {
  flex: 1;
  padding: 12px;
  border-radius: 8px;
  border: 1px solid #1e293b;
  background: #020617;
  color: white;
  font-size: 16px;
}

button {
  padding: 12px 18px;
  border-radius: 8px;
  border: none;
  background: #38bdf8;
  font-weight: bold;
  cursor: pointer;
}

#status {
  margin-top: 10px;
  opacity: 0.8;
}
</style>
</head>

<body>

<div class="app">
  <h1>⚡ Sqwazzy Search</h1>

  <div class="controls">
    <input id="inputBox" placeholder="Search or enter URL">
    <button onclick="go()">Go</button>
  </div>

  <div id="status">Type a website or search anything</div>
</div>

<script>
const input = document.getElementById("inputBox");
const status = document.getElementById("status");

// Detect URL vs search
function isLikelyUrl(text) {
  return text.includes(".") && !text.includes(" ");
}

function normalizeUrl(url) {
  if (!url.startsWith("http")) {
    return "https://" + url;
  }
  return url;
}

function go() {
  const value = input.value.trim();

  if (!value) {
    status.textContent = "Enter something first!";
    return;
  }

  let destination;

  if (isLikelyUrl(value)) {
    destination = normalizeUrl(value);
    status.textContent = "Opening website...";
  } else {
    destination =
      "https://duckduckgo.com/?q=" + encodeURIComponent(value);
    status.textContent = "Searching...";
  }

  window.open(destination, "_blank");
}

// Enter key support
input.addEventListener("keydown", e => {
  if (e.key === "Enter") go();
});
</script>

</body>
</html>
