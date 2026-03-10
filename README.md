<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>STRESSED CLAN SYSTEM</title>

<style>

body{
font-family:Arial;
background:#0f172a;
color:white;
text-align:center;
}

h1{
color:#38bdf8;
}

table{
margin:auto;
border-collapse:collapse;
width:90%;
}

th,td{
border:1px solid white;
padding:10px;
}

button{
padding:8px 15px;
margin:5px;
border:none;
border-radius:8px;
background:#38bdf8;
cursor:pointer;
}

button:hover{
background:#0ea5e9;
}

input{
padding:8px;
margin:5px;
}

.section{
margin-top:40px;
}

</style>
</head>

<body>

<h1>STRESSED CLAN</h1>

<div class="section">

<h2>🔐 ยืนยันตัวตน</h2>

<input id="name" placeholder="ชื่อ">
<input id="code" placeholder="รหัส">

<br>

<button onclick="login()">เข้าสู่ระบบ</button>

<p id="loginStatus"></p>

</div>

<div class="section">

<h2>📊 ตารางคะแนน</h2>

<table id="scoreTable"></table>

</div>

<div class="section">

<h2>💰 ระบบแลกแต้ม</h2>

<button onclick="redeem(150,'QUICK Roll')">150 QUICK Roll</button>

<button onclick="redeem(400,'VIP')">400 VIP</button>

<button onclick="redeem(700,'Chroma Pack')">700 Chroma Pack</button>

<button onclick="redeem(900,'Starter Pack')">900 Starter Pack</button>

<button onclick="redeem(1100,'Water Doge Pack')">1100 Water Doge Pack</button>

<button onclick="redeem(1400,'Lucky Pack')">1400 Lucky Pack</button>

<button onclick="redeem(1800,'Gwa Pack')">1800 Gwa Pack</button>

<button onclick="redeem(2500,'Gubby Pack')">2500 Gubby Pack</button>

<button onclick="redeem(25000,'Secret Reward')">25000 Secret Reward 😈</button>

<p id="redeemResult"></p>

</div>

<div class="section">

<h2>📜 ประวัติการแลก</h2>

<ul id="history"></ul>

</div>

<div class="section">

<h2>👑 แอดมิน (หัวแคลน)</h2>

<input id="target" placeholder="ชื่อคน">

<input id="pointChange" placeholder="แต้ม (+ หรือ -)">

<br>

<button onclick="changePoint()">เปลี่ยนแต้ม</button>

</div>

<div class="section">

<h2>📜 กฎแคลน</h2>

<p>

🎮 กิจกรรมทุกวันศุกร์ 19:00 – 23:00 AFK รวมกัน

</p>

<p>

ไม่แจ้งล่วงหน้า = -5 แต้ม

</p>

<p>

แจ้งล่วงหน้า = ไม่ถูกหัก

</p>

<p>

Gamepass แลกได้ครั้งเดียวต่อบัญชี

</p>

<p>

Secret Reward

25000 แต้ม = หัวแคลนแต่งหญิง 1 วัน 😈

</p>

</div>

<script>

let admin="บิว"

let members=JSON.parse(localStorage.getItem("members"))||{

"ออม":770,

"ต้น":827,

"โอ๊ค":550,

"บิว":25000,
}

let codes={

"ออม":"k642mut",

"ต้น":"TONTONRODPAN",

"โอ๊ค":"tootuokj",

"บิว":"admin",
}

let currentUser=null

let history=JSON.parse(localStorage.getItem("history"))||[]

function save(){

localStorage.setItem("members",JSON.stringify(members))

localStorage.setItem("history",JSON.stringify(history))

}

function getRank(p){

if(p>=2000)return"👑 LEGEND"

if(p>=1000)return"💎 ELITE"

if(p>=700)return"🔥 PRO"

if(p>=300)return"⭐ MEMBER"

return"🌱 NEW"

}

function renderTable(){

let table=document.getElementById("scoreTable")

table.innerHTML="<tr><th>ชื่อ</th><th>แต้ม</th><th>Rank</th></tr>"

let sorted=Object.entries(members).sort((a,b)=>b[1]-a[1])

for(let m of sorted){

table.innerHTML+=`<tr>

<td>${m[0]}</td>

<td>${m[1]}</td>

<td>${getRank(m[1])}</td>

</tr>`

}

}

function renderHistory(){

let list=document.getElementById("history")

list.innerHTML=""

for(let h of history){

list.innerHTML+=`<li>${h}</li>`

}

}

function login(){

let name=document.getElementById("name").value

let code=document.getElementById("code").value

if(codes[name]==code){

currentUser=name

document.getElementById("loginStatus").innerText="✅ ล็อกอินสำเร็จ : "+name

}else{

document.getElementById("loginStatus").innerText="❌ รหัสผิด"

}

}

function redeem(cost,item){

if(!currentUser){

document.getElementById("redeemResult").innerText="❌ ต้องล็อกอินก่อน"

return

}

if(members[currentUser]>=cost){

members[currentUser]-=cost

history.push(currentUser+" แลก "+item)

document.getElementById("redeemResult").innerText="🎁 แลกสำเร็จ"

save()

renderTable()

renderHistory()

}else{

document.getElementById("redeemResult").innerText="❌ แต้มไม่พอ"

}

}

function changePoint(){

if(currentUser!=admin){

alert("เฉพาะหัวแคลนเท่านั้น")

return

}

let name=document.getElementById("target").value

let change=parseInt(document.getElementById("pointChange").value)

members[name]+=change

history.push("ADMIN เปลี่ยนแต้ม "+name+" "+change)

save()

renderTable()

renderHistory()

}

renderTable()

renderHistory()

</script>

</body>
</html>