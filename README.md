<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pixel Move | Professional</title>
    <style>
        :root {
            --primary: #00f2fe;
            --secondary: #4facfe;
            --bg: #0b0f19;
            --glass: rgba(255, 255, 255, 0.07);
            --card-bg: rgba(15, 22, 36, 0.9);
        }

        body {
            font-family: 'Segoe UI', sans-serif;
            background: var(--bg);
            background-image: radial-gradient(circle at 50% 0%, #1e293b 0%, #0b0f19 100%);
            color: white;
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .app-container {
            width: 100%;
            max-width: 400px;
            height: 700px;
            background: var(--card-bg);
            border-radius: 40px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            position: relative;
            overflow: hidden;
            box-shadow: 0 50px 100px rgba(0,0,0,0.8);
        }

        .page { display: none; padding: 30px; height: 100%; box-sizing: border-box; }
        .active { display: block; animation: fadeIn 0.5s ease; }

        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* Login UI */
        .login-box { text-align: center; margin-top: 50px; }
        .logo-icon { font-size: 50px; margin-bottom: 10px; }
        
        /* Dashboard UI */
        .bal-card {
            background: linear-gradient(135deg, var(--secondary), var(--primary));
            padding: 30px;
            border-radius: 25px;
            text-align: center;
            margin-bottom: 25px;
            box-shadow: 0 15px 30px rgba(79, 172, 254, 0.3);
        }

        input {
            width: 100%; padding: 15px; margin: 10px 0; border-radius: 15px;
            border: 1px solid rgba(255,255,255,0.1); background: rgba(255,255,255,0.05);
            color: white; outline: none; box-sizing: border-box;
        }

        button {
            width: 100%; padding: 16px; border-radius: 15px; border: none;
            font-weight: bold; cursor: pointer; transition: 0.3s; margin-top: 10px;
        }

        .btn-main { background: white; color: var(--bg); }
        .btn-outline { background: var(--glass); color: white; border: 1px solid rgba(255,255,255,0.1); }

        .history-item {
            background: rgba(255,255,255,0.03);
            padding: 15px; border-radius: 15px; margin-bottom: 10px;
            display: flex; justify-content: space-between; align-items: center;
        }

        .withdraw-text { color: #ff4d4d; font-weight: bold; }
        .earn-text { color: #00f2fe; font-weight: bold; }
    </style>
</head>
<body>

<div class="app-container">
    
    <div id="loginPage" class="page active">
        <div class="login-box">
            <div class="logo-icon">💠</div>
            <h1 style="letter-spacing: -1px;">Pixel Move</h1>
            <p style="opacity: 0.5;">Enter Credentials</p>
            <input type="text" id="u" placeholder="Username">
            <input type="password" id="p" placeholder="Password">
            <button class="btn-main" onclick="doLogin()">Secure Login</button>
        </div>
    </div>

    <div id="homePage" class="page">
        <div style="display:flex; justify-content: space-between; align-items:center;">
            <span>Wallet</span>
            <span style="font-size: 10px; opacity: 0.4;">ID: 000-PM</span>
        </div>
        
        <div class="bal-card">
            <p style="margin:0; opacity:0.8; font-size: 14px;">Current Balance</p>
            <h1 style="font-size: 45px; margin: 10px 0;">$<span id="displayBal">0.00</span></h1>
        </div>

        <div style="display: flex; gap: 10px; margin-bottom: 20px;">
            <div style="flex:1; background: var(--glass); padding:10px; border-radius:15px; text-align:center;">
                <small style="opacity:0.6;">Rate</small><br><strong>$1/USD</strong>
            </div>
            <div style="flex:1; background: var(--glass); padding:10px; border-radius:15px; text-align:center;">
                <small style="opacity:0.6;">Min Payout</small><br><strong>$100</strong>
            </div>
        </div>

        <button class="btn-main" onclick="showPage('sellPage')">Sell Pictures</button>
        <button class="btn-outline" onclick="showPage('withdrawPage')">Withdrawal</button>
        <button class="btn-outline" onclick="showPage('historyPage')">Sell History</button>
        
        <button onclick="showPage('secPage')" style="background:none; color:grey; font-size:9px; margin-top:40px;">H.P.L ACCESS</button>
    </div>

    <div id="sellPage" class="page">
        <h2>Marketplace</h2>
        <button class="btn-outline" onclick="prep('Normal', 1)">Normal Pictures (2 = $1)</button>
        <button class="btn-outline" onclick="prep('Sexual', 5)">Sexual Pictures (2 = $5)</button>
        
        <div id="upSection" style="display:none; margin-top:20px;">
            <p id="catName" style="color:var(--primary)"></p>
            <input type="file" id="f">
            <button class="btn-main" onclick="finishSell()">Confirm & Send</button>
        </div>
        <button onclick="showPage('homePage')" style="background:none; color:white; margin-top:20px;">Cancel</button>
    </div>

    <div id="withdrawPage" class="page">
        <h2>Withdraw</h2>
        <input type="number" id="wa" placeholder="Amount ($)">
        <input type="text" id="jn" placeholder="JazzCash Number">
        <button class="btn-main" onclick="checkW()">Transfer Now</button>
        <button onclick="showPage('homePage')" style="background:none; color:white;">Back</button>
    </div>

    <div id="historyPage" class="page">
        <h2>Activity</h2>
        <div id="hList" style="max-height: 400px; overflow-y: auto;"></div>
        <button class="btn-outline" onclick="showPage('homePage')" style="margin-top:20px;">Back</button>
    </div>

    <div id="secPage" class="page">
        <h2>Admin Access</h2>
        <input type="password" id="sc" placeholder="Secret Code">
        <button class="btn-main" onclick="checkS()">Unlock</button>
        <div id="adm" style="display:none; margin-top:20px;">
            <input type="number" id="aa" placeholder="Add Amount">
            <button class="btn-main" onclick="admUp()">Update Balance</button>
        </div>
        <button onclick="showPage('homePage')" style="background:none; color:white;">Exit</button>
    </div>

</div>

<script>
    // Set initial custom data as per instructions
    if (!localStorage.getItem('pm_init')) {
        localStorage.setItem('pm_bal', "442.00");
        localStorage.setItem('pm_hist', JSON.stringify([{type:'Withdrawal', amt: 379, style: 'withdraw-text'}]));
        localStorage.setItem('pm_init', "true");
    }

    let bal = parseFloat(localStorage.getItem('pm_bal'));
    let hist = JSON.parse(localStorage.getItem('pm_hist'));
    let curRate = 0;
    let curCat = "";

    function showPage(p) {
        document.querySelectorAll('.page').forEach(pg => pg.classList.remove('active'));
        document.getElementById(p).classList.add('active');
        updateUI();
    }

    function doLogin() {
        if(document.getElementById('u').value === "000" && document.getElementById('p').value === "0001") {
            showPage('homePage');
        } else { alert("Invalid Credentials"); }
    }

    function updateUI() {
        document.getElementById('displayBal').innerText = bal.toFixed(2);
        const l = document.getElementById('hList');
        l.innerHTML = "";
        hist.slice().reverse().forEach(i => {
            l.innerHTML += `<div class="history-item">
                <span>${i.type}</span>
                <span class="${i.style}">${i.style === 'withdraw-text' ? '-' : '+'}$${i.amt}</span>
            </div>`;
        });
        localStorage.setItem('pm_bal', bal);
        localStorage.setItem('pm_hist', JSON.stringify(hist));
    }

    function prep(c, r) {
        curCat = c; curRate = r;
        document.getElementById('catName').innerText = "Category: " + c;
        document.getElementById('upSection').style.display = "block";
    }

    function finishSell() {
        bal += curRate;
        hist.push({type: curCat + ' Sale', amt: curRate, style: 'earn-text'});
        window.location.href = `mailto:hafizgo879@gmail.com?subject=Pixel Move Sale&body=Category: ${curCat}. Earned: $${curRate}`;
        alert("Images Sent! Balance Updated.");
        showPage('homePage');
    }

    function checkW() {
        const amt = parseFloat(document.getElementById('wa').value);
        if(amt >= 100) { alert("For withdrawals over $100, please contact hafizgo879@gmail.com"); }
        else { prompt("Confirm Password:"); alert("System Error: Transfer Gateway Offline."); }
    }

    function checkS() {
        if(document.getElementById('sc').value === "5551") {
            document.getElementById('adm').style.display = "block";
        } else { alert("Access Denied"); }
    }

    function admUp() {
        const a = parseFloat(document.getElementById('aa').value);
        if(!isNaN(a)) {
            bal += a;
            updateUI();
            alert("Balance Changed.");
            showPage('homePage');
        }
    }

    updateUI();
</script>

</body>
</html>
