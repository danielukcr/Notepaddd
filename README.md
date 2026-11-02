<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PNC | Officer Infraction Management</title>
<style>
:root{--bg:#071321;--panel:#0d2033;--panel2:#102940;--line:#24435d;--text:#eaf2f8;--muted:#9bb0c2;--blue:#3b82c4;--blue2:#235f98;--red:#d65b61}
*{box-sizing:border-box}body{margin:0;background:radial-gradient(circle at 15% 0%,#12304a 0,transparent 36%),var(--bg);font-family:Arial,Helvetica,sans-serif;color:var(--text);min-height:100vh}
header{border-bottom:1px solid var(--line);background:#081827eF;padding:22px 5%;display:flex;align-items:center;gap:16px}
.crest{width:48px;height:48px;border:2px solid #6b9dc4;border-radius:12px;display:grid;place-items:center;font-weight:800;color:#b9d8f1;letter-spacing:1px}
.brand small{display:block;color:#8fa9bf;font-size:11px;letter-spacing:2px;margin-bottom:5px}.brand h1{font-size:19px;margin:0;letter-spacing:1.2px}
.status{margin-left:auto;color:#a9c4d9;font-size:12px;border:1px solid var(--line);padding:8px 11px;border-radius:20px}
main{max-width:920px;margin:38px auto;padding:0 20px 50px}
.intro{margin-bottom:22px}.intro h2{font-size:25px;margin:0 0 8px}.intro p{color:var(--muted);margin:0;line-height:1.5;font-size:14px}
.card{background:linear-gradient(145deg,var(--panel),#0a1a2a);border:1px solid var(--line);border-radius:15px;padding:25px;box-shadow:0 18px 45px #0003}
.card-head{display:flex;align-items:center;justify-content:space-between;gap:12px;margin-bottom:22px}.card-head h3{margin:0;font-size:16px}.tag{font-size:10px;color:#a9c8e2;border:1px solid #345b79;border-radius:20px;padding:6px 9px;letter-spacing:1px}
.grid{display:grid;grid-template-columns:1fr 1fr;gap:18px}.field{display:flex;flex-direction:column;gap:8px}.wide{grid-column:1/-1}label{font-size:12px;font-weight:700;color:#c4d4e1;letter-spacing:.4px}
input,select,textarea{width:100%;background:#071827;border:1px solid #29445b;border-radius:8px;padding:12px 13px;color:var(--text);font:14px Arial;outline:none}
input:focus,select:focus,textarea:focus{border-color:#68a6d8;box-shadow:0 0 0 3px #3b82c422}textarea{resize:vertical;min-height:100px;line-height:1.5}select option{background:#0d2033}
.hint{font-size:11px;color:#8199ad;margin-top:-3px}
.actions{display:flex;justify-content:flex-end;gap:10px;margin-top:22px}.btn{border:0;border-radius:8px;padding:12px 18px;font-weight:700;cursor:pointer;font-size:13px}.secondary{background:#19334a;color:#c6d8e7;border:1px solid #34516a}.primary{background:linear-gradient(135deg,var(--blue),var(--blue2));color:white}.btn:disabled{opacity:.55;cursor:wait}
#feedback{display:none;margin-top:16px;padding:12px;border-radius:8px;font-size:13px;line-height:1.5}#feedback.ok{display:block;background:#12382f;border:1px solid #286a56;color:#b9ead8}#feedback.err{display:block;background:#3b2025;border:1px solid #80414a;color:#ffd0d3}
.config{margin-top:18px;background:#0a1a29;border:1px solid var(--line);border-radius:12px;padding:17px 19px}.config summary{cursor:pointer;color:#b7cde0;font-size:13px;font-weight:700}.config p{font-size:12px;color:var(--muted);line-height:1.5}.config code{color:#d6e8f6}
footer{text-align:center;color:#668096;font-size:11px;margin-top:24px}
@media(max-width:640px){header{padding:17px 20px}.status{display:none}main{margin:25px auto}.card{padding:18px}.grid{grid-template-columns:1fr}.wide{grid-column:auto}.card-head{align-items:flex-start;flex-direction:column}.actions{flex-direction:column-reverse}.btn{width:100%}}
</style>
</head>
<body>
<header>
  <div class="crest">PNC</div>
  <div class="brand"><small>POLICE NATIONAL COMPUTER</small><h1>OFFICER INFRACTION SYSTEM</h1></div>
  <div class="status">● SYSTEM PORTAL</div>
</header>
<main>
  <div class="intro">
    <h2>Record an officer infraction</h2>
    <p>Complete the details below to submit an officer record to your designated Discord channel.</p>
  </div>
  <section class="card">
    <div class="card-head"><h3>Infraction submission</h3><span class="tag">INTERNAL RECORDS</span></div>
    <form id="infractionForm">
      <div class="grid">
        <div class="field">
          <label for="officerName">OFFICER NAME</label>
          <input id="officerName" name="officerName" placeholder="Enter officer's name" maxlength="100" required>
        </div>
        <div class="field">
          <label for="shoulder">OFFICER SHOULDER NUMBER</label>
          <input id="shoulder" name="shoulder" placeholder="e.g. 4721" maxlength="30" required>
        </div>
        <div class="field wide">
          <label for="type">INFRACTION TYPE</label>
          <select id="type" name="type" required>
            <option value="" disabled selected>Select an infraction type</option>
            <option>Warning 1</option><option>Warning 2</option><option>Suspension</option>
            <option>Termination</option><option>Under investigation</option><option>Blacklist</option>
          </select>
        </div>
        <div class="field wide">
          <label for="reason">REASON</label>
          <textarea id="reason" name="reason" placeholder="Explain the reason for this infraction..." maxlength="1500" required></textarea>
        </div>
        <div class="field wide">
          <label for="notes">NOTES</label>
          <textarea id="notes" name="notes" placeholder="Add any further information (optional)..." maxlength="1500"></textarea>
          <span class="hint">Include any relevant context or administrative notes.</span>
        </div>
      </div>
      <div class="actions">
        <button class="btn secondary" type="reset">CLEAR FORM</button>
        <button class="btn primary" id="submitBtn" type="submit">SUBMIT INFRACTION ↗</button>
      </div>
      <div id="feedback" role="status" aria-live="polite"></div>
    </form>
  </section>
  <details class="config">
    <summary>WEBHOOK CONFIGURATION &amp; SETUP</summary>
    <p>Set your Discord webhook in the JavaScript configuration near the bottom of this file, replacing the placeholder value.</p>
    <p><strong>Security:</strong> A webhook embedded in a public website can be viewed and misused by visitors. For a live/public deployment, keep the webhook URL on a private server and send submissions through a server-side endpoint. Do not publish a real webhook in client-side code.</p>
  </details>
  <footer>PNC OFFICER INFRACTION SYSTEM · ROLEPLAY ADMINISTRATION USE</footer>
</main>
<script>
// ============================================
// DISCORD WEBHOOK CONFIGURATION
// For private testing only. Do not expose a real
// webhook URL in a public website.
// ============================================
const DISCORD_WEBHOOK_URL = "PASTE_YOUR_DISCORD_WEBHOOK_URL_HERE";

const form = document.getElementById("infractionForm");
const submitBtn = document.getElementById("submitBtn");
const feedback = document.getElementById("feedback");

form.addEventListener("submit", async (event) => {
  event.preventDefault();

  if (!form.reportValidity()) return;
  if (!DISCORD_WEBHOOK_URL.startsWith("https://discord.com/api/webhooks/") &&
      !DISCORD_WEBHOOK_URL.startsWith("https://discordapp.com/api/webhooks/")) {
    showFeedback("Add your Discord webhook URL in the JavaScript configuration before submitting.", false);
    return;
  }

  const officerName = document.getElementById("officerName").value.trim();
  const shoulder = document.getElementById("shoulder").value.trim();
  const type = document.getElementById("type").value;
  const reason = document.getElementById("reason").value.trim();
  const notes = document.getElementById("notes").value.trim();

  if (!officerName || !shoulder || !type || !reason) {
    showFeedback("Please complete all required fields.", false);
    return;
  }

  const embed = {
    title: "📋 Officer Infraction Recorded",
    color: colorForType(type),
    fields: [
      { name: "Officer Name", value: safeField(officerName), inline: true },
      { name: "Shoulder Number", value: safeField(shoulder), inline: true },
      { name: "Infraction Type", value: safeField(type), inline: false },
      { name: "Reason", value: safeField(reason), inline: false },
      { name: "Notes", value: safeField(notes || "No additional notes provided."), inline: false }
    ],
    footer: { text: "PNC Officer Infraction System" },
    timestamp: new Date().toISOString()
  };

  submitBtn.disabled = true;
  submitBtn.textContent = "SUBMITTING...";
  try {
    const response = await fetch(DISCORD_WEBHOOK_URL, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ username: "PNC Infraction System", embeds: [embed] })
    });
    if (!response.ok) throw new Error("Discord returned HTTP " + response.status);
    showFeedback("Infraction submitted successfully to Discord.", true);
    form.reset();
  } catch (error) {
    showFeedback("Submission failed. Check the webhook URL and browser console. For a public site, use a server-side webhook endpoint. (" + error.message + ")", false);
  } finally {
    submitBtn.disabled = false;
    submitBtn.textContent = "SUBMIT INFRACTION ↗";
  }
});

function safeField(value) {
  // Discord embed field values have a 1024-character limit.
  return value.replace(/@/g, "@\u200b").slice(0, 1024);
}
function colorForType(type) {
  const colors = {
    "Warning 1": 0xD6B34A, "Warning 2": 0xE58A3A,
    "Suspension": 0xD66B42, "Termination": 0xC94752,
    "Under investigation": 0x4C83B8, "Blacklist": 0x713D83
  };
  return colors[type] || 0x3B82C4;
}
function showFeedback(message, success) {
  feedback.textContent = message;
  feedback.className = success ? "ok" : "err";
}
</script>
</body>
</html>
