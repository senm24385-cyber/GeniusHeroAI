<!DOCTYPE html>
<html lang="tk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>GENIUS HERO AI - OMEGA V17 (RELAY)</title>
    <style>
        :root { --neon: #0f0; --gold: #ffd700; --bg: #000; --red: #ff0000; --blue: #00aaff; }
        body { background: var(--bg); color: var(--neon); font-family: 'Courier New', monospace; margin: 0; height: 100vh; display: flex; flex-direction: column; align-items: center; justify-content: center; overflow: hidden; }
        .dashboard { position: absolute; top: 0; width: 100%; display: flex; justify-content: space-around; padding: 15px; font-size: 0.8rem; border-bottom: 2px solid var(--red); background: rgba(0,0,0,0.9); }
        .stat-val { color: #fff; font-weight: bold; }
        #brain-core { width: 120px; height: 120px; border: 4px double var(--red); border-radius: 50%; display: flex; align-items: center; justify-content: center; position: relative; margin-bottom: 15px; box-shadow: 0 0 50px var(--red); animation: spin 5s linear infinite; font-size: 2rem; }
        .panel { background: #050505; border: 2px solid var(--red); padding: 20px; border-radius: 10px; width: 90%; max-width: 450px; text-align: center; }
        #ai-terminal { height: 300px; overflow-y: auto; font-size: 0.85rem; color: var(--gold); background: #000; padding: 15px; border: 1px solid var(--neon); text-align: left; margin: 10px 0; border-left: 5px solid var(--red); white-space: pre-wrap; font-weight: bold; }
        button { background: var(--red); color: #fff; border: none; padding: 15px; width: 100%; font-weight: 900; cursor: pointer; text-transform: uppercase; margin-top: 10px; box-shadow: 0 0 10px var(--red); }
        input { background: #111; border: 1px solid var(--red); color: var(--gold); text-align: center; padding: 12px; width: 90%; margin-bottom: 8px; outline: none; font-size: 1.1rem; }
        @keyframes spin { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
        .syncing { color: var(--blue); animation: blink 0.5s infinite; }
        @keyframes blink { 50% { opacity: 0.3; } }
        .hidden { display: none !important; }
    </style>
</head>
<body>
    <div class="dashboard">
        <div>XP: <span id="xp">0</span></div>
        <div>IQ: 145</div>
        <div>LVL: GOD</div>
    </div>
    <div id="brain-core">🧠</div>
    <div id="main-panel" class="panel">
        <div id="ai-terminal">> OMEGA V17: RELAY PROTOCOL ACTIVE.</div>
        <input type="text" id="master-input" placeholder="BUÝRUK BERIŇ...">
        <button onclick="executeCommand()">FORCE RELAY EXECUTE</button>
    </div>

<script>
    const MASTER_KEY = "AIzaSyCxgQBOKAiupQau9OwqDZGM7GX5eNgv4Y4";
    let xp = 0;

    function log(msg, cls = "") {
        const term = document.getElementById('ai-terminal');
        const div = document.createElement('div');
        div.className = cls;
        div.innerText = `>> ${msg}`;
        term.appendChild(div);
        term.scrollTop = term.scrollHeight;
    }

    async function executeCommand() {
        const val = document.getElementById('master-input').value;
        if(!val) return;
        log(`MASTER: ${val}`);
        document.getElementById('master-input').value = "";
        log("⚡ RELAY TUNNEL: BYPASSING FILTERS...", "syncing");

        const target = `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${MASTER_KEY}`;
        
        // 🔥 IŇ GÜÝÇLI RELAY TUNNELI (Corsproxy.io we beýlekiler)
        const relays = [
            `https://corsproxy.io/?${encodeURIComponent(target)}`,
            `https://api.allorigins.win/get?url=${encodeURIComponent(target)}`,
            `https://proxy.cors.sh/${target}`
        ];

        let success = false;
        for (let url of relays) {
            try {
                const response = await fetch(url, {
                    method: "POST",
                    headers: { "Content-Type": "application/json" },
                    body: JSON.stringify({ contents: [{ parts: [{ text: val }] }] })
                });

                if (response.ok) {
                    const data = await response.json();
                    // AllOrigins üçin ýörite format
                    const result = data.contents ? JSON.parse(data.contents) : data;
                    const reply = result.candidates[0].content.parts[0].text;
                    log(`AI CORE:\n${reply}`);
                    xp += 1000; document.getElementById('xp').innerText = xp;
                    success = true;
                    break;
                }
            } catch (e) { continue; }
        }

        if (!success) {
            log("❌ TUNNEL BLOCKED. INTERNETIŇIZDE VPN ÝAPYLMADYK BOLSA, VPN-I AÇYŇ.");
            log("💡 MASLAHAT: GITHUB LINKINE VPN BILEN GIRIP GÖRÜŇ.");
        }
    }
</script>
</body>
</html>
