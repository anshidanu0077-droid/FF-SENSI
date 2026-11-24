
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FF-SENSI | Free Fire Sensitivity</title>
<style>
*{box-sizing:border-box}
body{
 margin:0;background:#10111b;color:white;
 font-family:Arial,sans-serif;text-align:center;
}
header{padding:25px;background:#191b2b}
h1{color:#ffb52e;font-size:32px}
p{color:#bbb}
.card{
 background:#202236;margin:22px auto;padding:22px;
 border-radius:18px;max-width:440px;width:92%;
}
input,select,button{
 width:100%;padding:15px;margin:10px 0;
 border:0;border-radius:10px;font-size:16px;
}
button{background:#ffad22;font-weight:bold;color:#171717}
.result{
 background:#151727;padding:12px;
 margin:10px 0;border-radius:10px;
}
.value{color:#ffbd43;font-size:25px;font-weight:bold}
footer{padding:25px;color:#888}
</style>
</head>
<body>
<header>
<h1>🔥 FF-SENSI</h1>
<p>Find your Free Fire sensitivity settings</p>
</header>

<div class="card">
<h2>Select Your Device</h2>
<input id="device" placeholder="Enter phone or tablet model">

<select id="type">
<option value="phone">Android Phone</option>
<option value="iphone">iPhone</option>
<option value="tablet">Tablet</option>
</select>

<select id="style">
<option value="balanced">Balanced</option>
<option value="headshot">One Tap / Headshot</option>
<option value="smooth">Smooth Gameplay</option>
</select>

<button onclick="generate()">GENERATE SENSITIVITY</button>
</div>

<div class="card" id="results" style="display:none">
<h2>YOUR SENSITIVITY</h2>
<div id="settings"></div>
<button onclick="copySettings()">COPY SETTINGS</button>
<p>These are suggested starting settings. Adjust them in-game.</p>
</div>

<script>
function generate(){
 const device=document.getElementById("device").value.trim();
 if(!device){
 alert("Please enter your device model!");
 return;
 }

 const type=document.getElementById("type").value;
 const style=document.getElementById("style").value;

 let base=type==="tablet"?145:type==="iphone"?175:185;

 if(style==="headshot")base+=8;
 if(style==="smooth")base-=12;

 let values=[
 ["General",base],
 ["Red Dot",base-5],
 ["2x Scope",base-15],
 ["4x Scope",base-25],
 ["Sniper Scope",base-55],
 ["Free Look",base+5]
 ];

 let html="";
 values.forEach(item=>{
 let value=Math.max(0,Math.min(200,item[1]));
 html+=`<div class="result">
 ${item[0]}<div class="value">${value}</div>
 </div>`;
 });

 document.getElementById("settings").innerHTML=html;
 document.getElementById("results").style.display="block";
}

function copySettings(){
 const text=document.getElementById("settings").innerText;
 if(navigator.clipboard){
 navigator.clipboard.writeText(text).then(()=>{
 alert("Settings copied!");
 });
 }else{
 alert("Please copy the settings manually.");
 }
}
</script>
<footer>FF-SENSI © 2026 | Fan-made settings tool</footer>
</body>
</html>
