# Uzs
Bizda koʻp
<!DOCTYPE html>
<html lang="uz">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>QARZ PRO</title>
<style>
*{box-sizing:border-box}
body{margin:0;background:#080d19;color:#fff;font-family:Arial,sans-serif}
button,input{font:inherit}
button{cursor:pointer;border:0}
:root{--blue:#3978ff;--card:#131e32;--muted:#91a0b9}
.container{max-width:1100px;margin:auto;padding:20px}
header{display:flex;justify-content:space-between;align-items:center;padding:18px 0}
.logo{font-size:25px;font-weight:900;color:#62a0ff}
.panel{background:var(--card);padding:22px;border:1px solid #24334e;border-radius:17px;margin:15px 0}
h2{font-size:21px;margin-top:0}
input{width:100%;padding:14px;margin:7px 0 13px;background:#091326;border:1px solid #34435d;border-radius:10px;color:white;outline:none}
input:focus{border-color:#5790ff}
.btn{padding:13px 18px;border-radius:10px;background:var(--blue);color:white;font-weight:bold}
.btn2{padding:11px 15px;border-radius:10px;background:#263650;color:white}
.full{width:100%}
.muted{color:var(--muted);font-size:13px}
.hidden{display:none!important}
.stats{display:grid;grid-template-columns:repeat(3,1fr);gap:12px}
.stat{background:#0b172b;padding:18px;border-radius:13px}
.stat strong{display:block;font-size:23px;margin-top:10px}
nav{display:flex;gap:8px;flex-wrap:wrap;margin:20px 0}
nav button{background:#192840;color:#b8c9e4;padding:12px;border-radius:9px}
nav button.active{background:#2868e9;color:white}
.row{display:flex;justify-content:space-between;align-items:center;gap:10px}
table{width:100%;border-collapse:collapse;font-size:13px}
td,th{padding:12px 7px;border-bottom:1px solid #293850;text-align:left}
.badge{background:#183e32;color:#67e2ad;padding:5px 8px;border-radius:7px}
.auth{max-width:440px;margin:7vh auto}
.error{color:#ff7777;font-size:13px}
@media(max-width:600px){.stats{grid-template-columns:1fr 1fr}.stat strong{font-size:18px}.container{padding:13px}td,th{padding:9px 4px;font-size:11px}}
</style>
</head>
<body>
<div class="container">

<!-- KIRISH -->
<section id="auth">
 <header><div class="logo">QARZ PRO</div><span class="muted">Moliyaviy boshqaruv</span></header>
 <div class="panel auth">
  <h2 id="authTitle">Tizimga kirish</h2>
  <div id="loginBox">
   <label class="muted">Foydalanuvchi ID</label>
   <input id="loginId" placeholder="Masalan: QP123456">
   <label class="muted">Parol</label>
   <input id="loginPass" type="password" placeholder="Parolingiz">
   <button class="btn full" onclick="login()">Kirish</button>
   <p class="muted">Hisobingiz yo‘qmi? <a href="#" onclick="showRegister()" style="color:#70a6ff">Ro‘yxatdan o‘tish</a></p>
  </div>
  <div id="registerBox" class="hidden">
   <label class="muted">Ism familiya</label>
   <input id="regName" placeholder="Ismingiz">
   <label class="muted">Telefon raqam</label>
   <input id="regPhone" placeholder="+998...">
   <label class="muted">Yangi parol</label>
   <input id="regPass" type="password" placeholder="Kamida 6 ta belgi">
   <button class="btn full" onclick="register()">Hisob yaratish</button>
   <p class="muted"><a href="#" onclick="showLogin()" style="color:#70a6ff">Orqaga qaytish</a></p>
  </div>
  <p id="authMsg" class="error"></p>
  <div class="panel" style="margin-bottom:0">
   <div class="row"><b>OneID</b><span class="badge">Rasmiy ulanish kutilmoqda</span></div>
   <p class="muted">OneID orqali kirish hozircha yoqilmagan. Rasmiy integratsiya talab etiladi.</p>
  </div>
 </div>
</section>

<!-- ASOSIY TIZIM -->
<section id="app" class="hidden">
 <header>
  <div class="logo">QARZ PRO</div>
  <button class="btn2" onclick="logout()">Chiqish ↗</button>
 </header>
 <div class="row">
  <div><h2 id="welcome">Salom!</h2><div class="muted" id="userId"></div></div>
  <span class="badge" id="role">Foydalanuvchi</span>
 </div>
 <nav>
  <button class="active" onclick="tab('home',this)">Bosh sahifa</button>
  <button onclick="tab('loans',this)">Qarzlar</button>
  <button onclick="tab('history',this)">Tarix</button>
  <button id="adminTab" class="hidden" onclick="tab('admin',this)">Admin</button>
  <button onclick="tab('profile',this)">Profil</button>
 </nav>

 <div id="home" class="page">
  <div class="stats">
   <div class="stat"><span class="muted">Jami berilgan qarz</span><strong id="totalLoan">0</strong><span class="muted">so‘m</span></div>
   <div class="stat"><span class="muted">Qaytarilgan</span><strong id="totalPaid">0</strong><span class="muted">so‘m</span></div>
   <div class="stat"><span class="muted">Qolgan qarz</span><strong id="totalLeft">0</strong><span class="muted">so‘m</span></div>
  </div>
  <div class="panel">
   <h2>So‘nggi operatsiyalar</h2>
   <div id="recent" class="muted">Hozircha operatsiyalar yo‘q.</div>
  </div>
 </div>

 <div id="loans" class="page hidden">
  <div class="panel">
   <h2>Qarzlarim</h2>
   <div id="myLoans" class="muted">Hozircha qarz mavjud emas.</div>
  </div>
 </div>

 <div id="history" class="page hidden">
  <div class="panel">
   <h2>Operatsiyalar tarixi</h2>
   <div id="myHistory" class="muted">Tarix bo‘sh.</div>
  </div>
 </div>

 <div id="admin" class="page hidden">
  <div class="panel">
   <h2>Yangi qarz rasmiylashtirish</h2>
   <label class="muted">Qarz oluvchi ID</label>
   <input id="borrowerId" placeholder="QP123456">
   <label class="muted">Qarz summasi (so‘m)</label>
   <input id="loanAmount" type="number" min="1" placeholder="1000000">
   <label class="muted">Oylik foiz (%)</label>
   <input id="loanRate" type="number" min="0" step="0.1" placeholder="Masalan: 3">
   <label class="muted">Muddat (oy)</label>
   <input id="loanMonths" type="number" min="1" placeholder="6">
   <button class="btn full" onclick="giveLoan()">Qarz rasmiylashtirish</button>
   <p id="loanMsg" class="error"></p>
  </div>
  <div class="panel">
   <h2>To‘lov qabul qilish</h2>
   <label class="muted">Qarz ID</label>
   <input id="payLoanId" placeholder="Qarz ID raqami">
   <label class="muted">To‘lov summasi</label>
   <input id="payAmount" type="number" min="1" placeholder="100000">
   <button class="btn full" onclick="makePayment()">To‘lovni qayd etish</button>
   <p id="payMsg" class="error"></p>
  </div>
  <div class="panel">
   <h2>Foydalanuvchilar</h2>
   <div id="usersList"></div>
  </div>
 </div>

 <div id="profile" class="page hidden">
  <div class="panel">
   <h2>Shaxsiy profil</h2>
   <p class="muted">Ism familiya</p><b id="profileName"></b>
   <p class="muted">Foydalanuvchi ID</p><b id="profileId"></b>
   <p class="muted">Telefon raqam</p><b id="profilePhone"></b>
   <p class="muted">Hisob turi</p><b id="profileRole"></b>
  </div>
 </div>
 <p class="muted">QARZ PRO • Demo versiya</p>
</section>
</div>

<script>
// FAQAT BRAUZERDA ISHLAYDIGAN DEMO
const get=(k,d)=>JSON.parse(localStorage.getItem(k)||JSON.stringify(d));
const save=(k,v)=>localStorage.setItem(k,JSON.stringify(v));
let users=get('qp_users',[]);
let loans=get('qp_loans',[]);
let history=get('qp_history',[]);
let current=null;

function showRegister(){
 loginBox.classList.add('hidden');
 registerBox.classList.remove('hidden');
 authTitle.textContent='Ro‘yxatdan o‘tish';
 authMsg.textContent='';
}
function showLogin(){
 registerBox.classList.add('hidden');
 loginBox.classList.remove('hidden');
 authTitle.textContent='Tizimga kirish';
 authMsg.textContent='';
}
function register(){
 const name=regName.value.trim(),phone=regPhone.value.trim(),pass=regPass.value;
 if(!name||!phone||pass.length<6){authMsg.textContent='Barcha maydonlarni to‘ldiring. Parol kamida 6 ta belgidan iborat bo‘lsin.';return;}
 const id='QP'+Math.floor(100000+Math.random()*900000);
 const user={id,name,phone,pass,role:users.length===0?'admin':'user'};
 users.push(user);save('qp_users',users);
 alert('Hisob yaratildi! Sizning ID raqamingiz: '+id);
 showLogin();loginId.value=id;loginPass.value='';
}
function login(){
 const id=loginId.value.trim().toUpperCase(),pass=loginPass.value;
 const user=users.find(u=>u.id===id&&u.pass===pass);
 if(!user){authMsg.textContent='ID yoki parol noto‘g‘ri.';return;}
 current=user;openApp();
}
function openApp(){
 auth.classList.add('hidden');app.classList.remove('hidden');
 welcome.textContent='Salom, '+current.name;
 userId.textContent='ID: '+current.id;
 role.textContent=current.role==='admin'?'Administrator':'Foydalanuvchi';
 adminTab.classList.toggle('hidden',current.role!=='admin');
 profileName.textContent=current.name;
 profileId.textContent=current.id;
 profilePhone.textContent=current.phone;
 profileRole.textContent=current.role==='admin'?'Administrator':'Foydalanuvchi';
 render();
}
function logout(){current=null;app.classList.add('hidden');auth.classList.remove('hidden');showLogin();}
function tab(id,btn){
 document.querySelectorAll('.page').forEach(p=>p.classList.add('hidden'));
 document.getElementById(id).classList.remove('hidden');
 document.querySelectorAll('nav button').forEach(b=>b.classList.remove('active'));
 btn.classList.add('active');render();
}
function money(n){return Number(n||0).toLocaleString('uz-UZ');}
function due(l){return l.amount*(1+l.rate/100*l.months);}
function paid(l){return history.filter(h=>h.loanId===l.id&&h.type==='payment').reduce((s,h)=>s+h.amount,0);}
function giveLoan(){
 if(current.role!=='admin')return;
 const id=borrowerId.value.trim().toUpperCase();
 const u=users.find(x=>x.id===id);
 const amount=Number(loanAmount.value),rate=Number(loanRate.value),months=Number(loanMonths.value);
 if(!u||!amount||amount<=0||rate<0||!months||months<=0){loanMsg.textContent='Ma’lumotlarni tekshiring. Qarz oluvchi ID mavjud bo‘lishi kerak.';return;}
 const l={id:'L'+Date.now(),userId:id,amount,rate,months,date:new Date().toISOString()};
 loans.push(l);save('qp_loans',loans);
 history.push({type:'loan',loanId:l.id,userId:id,amount,date:l.date});save('qp_history',history);
 loanMsg.textContent='Demo qarz qayd etildi: '+l.id;
 render();
}
function makePayment(){
 if(current.role!=='admin')return;
 const id=payLoanId.value.trim(),amount=Number(payAmount.value);
 const l=loans.find(x=>x.id===id);
 if(!l||!amount||amount<=0){payMsg.textContent='Qarz ID yoki to‘lov summasi noto‘g‘ri.';return;}
 const left=due(l)-paid(l);
 if(amount>left){payMsg.textContent='To‘lov qolgan qarzdan katta.';return;}
 history.push({type:'payment',loanId:id,userId:l.userId,amount,date:new Date().toISOString()});
 save('qp_history',history);payMsg.textContent='To‘lov qayd etildi.';render();
}
function render(){
 if(!current)return;
 const mine=loans.filter(l=>current.role==='admin'||l.userId===current.id);
 const total=mine.reduce((s,l)=>s+l.amount,0);
 const totalPaid=mine.reduce((s,l)=>s+paid(l),0);
 const left=mine.reduce((s,l)=>s+Math.max(0,due(l)-paid(l)),0);
 totalLoan.textContent=money(total);totalPaid.textContent=money(totalPaid);totalLeft.textContent=money(left);
 myLoans.innerHTML=mine.length?mine.map(l=>`
 <div class="panel">
 <b>${l.id}</b><p class="muted">Qarz oluvchi: ${l.userId}</p>
 <p>Asosiy summa: ${money(l.amount)} so‘m</p>
 <p>Foiz: ${l.rate}% / oy • Muddat: ${l.months} oy</p>
 <p>Jami qaytarish: <b>${money(due(l))} so‘m</b></p>
 <p>To‘langan: ${money(paid(l))} so‘m</p>
 <p>Qoldiq: <b>${money(Math.max(0,due(l)-paid(l)))} so‘m</b></p>
 </div>`).join(''):'Hozircha qarz mavjud emas.';
 const hist=history.filter(h=>current.role==='admin'||h.userId===current.id).slice().reverse();
 myHistory.innerHTML=hist.length?hist.map(h=>`<div class="panel"><b>${h.type==='loan'?'Qarz berildi':'To‘lov qabul qilindi'}</b><p>${h.userId} • ${money(h.amount)} so‘m</p><span class="muted">${new Date(h.date).toLocaleString('uz-UZ')} • ${h.loanId}</span></div>`).join(''):'Tarix bo‘sh.';
 recent.innerHTML=hist.slice(0,4).map(h=>`<p>${h.type==='loan'?'Qarz':'To‘lov'} • ${h.userId} • ${money(h.amount)} so‘m</p>`).join('')||'Hozircha operatsiyalar yo‘q.';
 if(current.role==='admin'){
 usersList.innerHTML=users.map(u=>`<div class="panel"><b>${u.name}</b><p class="muted">${u.id} • ${u.phone}</p><span class="badge">${u.role}</span></div>`).join('');
 }
}
showLogin();
</script>
</body>
</html>
