[mikres_maxes (1).html](https://github.com/user-attachments/files/34856496/mikres_maxes.1.html)
<!doctype html>
<html lang="el">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Μικρές Μάχες</title>
<style>
:root{--bg:#111827;--panel:#1f2937;--panel2:#273449;--gold:#fbbf24;--red:#ef4444;--green:#34d399;--text:#f9fafb;--muted:#cbd5e1}
*{box-sizing:border-box}body{margin:0;background:radial-gradient(circle at top,#26354d,#101827 60%);color:var(--text);font-family:system-ui,Segoe UI,sans-serif;min-height:100vh;padding:20px}
main{max-width:900px;margin:auto}.top{display:flex;justify-content:space-between;gap:12px;align-items:center;flex-wrap:wrap}
h1{margin:0;font-size:clamp(26px,5vw,38px)}.sub{color:var(--muted);margin:6px 0 18px}
.stats{display:flex;gap:10px;flex-wrap:wrap}.pill{background:#263449;border:1px solid #40516b;border-radius:999px;padding:8px 13px;font-weight:700}
.grid{display:grid;grid-template-columns:1fr 1fr;gap:16px}.card{background:linear-gradient(145deg,#263449,#1b2637);border:1px solid #40516b;border-radius:18px;padding:18px;box-shadow:0 12px 30px #0003}
.card h2{margin:0 0 12px;font-size:20px}.fighter{font-size:76px;text-align:center;line-height:1.25;margin:8px}.name{text-align:center;font-weight:800;font-size:20px}
.bar{height:13px;background:#0b1220;border-radius:99px;overflow:hidden;margin:8px 0}.fill{height:100%;width:100%;background:var(--green);transition:width .25s}
.hptext{font-size:13px;color:var(--muted);display:flex;justify-content:space-between}
.actions{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-top:15px}
button{border:0;border-radius:12px;padding:13px 10px;font-weight:800;font-size:15px;cursor:pointer;color:#111827;background:var(--gold);transition:transform .08s,filter .15s}
button:hover{filter:brightness(1.08)}button:active{transform:scale(.97)}button:disabled{opacity:.4;cursor:not-allowed}
.secondary{background:#93c5fd}.defend{background:#a7f3d0}.danger{background:#fca5a5}
.log{height:170px;overflow:auto;background:#101827;border-radius:12px;padding:12px;color:#dbeafe;font-size:14px;line-height:1.55}
.shop{display:flex;gap:10px;flex-wrap:wrap}.shop button{flex:1;min-width:180px}
.notice{color:var(--muted);font-size:13px;margin-top:10px}
@media(max-width:650px){.grid{grid-template-columns:1fr}.actions{grid-template-columns:1fr}.fighter{font-size:60px}}
</style>
</head>
<body>
<main>
  <div class="top">
    <div><h1>⚔️ Μικρές Μάχες</h1><div class="sub">Μπες στην αρένα, νίκησε τέρατα και γίνε δυνατότερος!</div></div>
    <div class="stats"><div class="pill">🪙 <span id="coins">0</span></div><div class="pill">⭐ Level <span id="level">1</span></div><div class="pill">XP <span id="xp">0</span>/<span id="nextxp">50</span></div></div>
  </div>

  <section class="grid">
    <div class="card">
      <h2>🛡️ Ο ήρωάς σου</h2>
      <div class="fighter" id="heroArt">🧙</div><div class="name">Ήρωας</div>
      <div class="hptext"><span>❤️ Ζωή</span><span id="heroHpText">100 / 100</span></div><div class="bar"><div class="fill" id="heroBar"></div></div>
      <div class="hptext"><span>⚔️ Δύναμη</span><b id="attackStat">15</b></div>
      <div class="hptext"><span>🛡️ Άμυνα</span><b id="defStat">5</b></div>
    </div>
    <div class="card">
      <h2>👹 Αντίπαλος</h2>
      <div class="fighter" id="enemyArt">🐺</div><div class="name" id="enemyName">Άγριος λύκος</div>
      <div class="hptext"><span>❤️ Ζωή</span><span id="enemyHpText">60 / 60</span></div><div class="bar"><div class="fill" id="enemyBar" style="background:var(--red)"></div></div>
      <div class="hptext"><span>⚔️ Δύναμη</span><b id="enemyAttack">9</b></div>
      <div class="notice" id="enemyHint">Νίκησέ τον για να πάρεις ανταμοιβές.</div>
    </div>
  </section>

  <section class="card" style="margin-top:16px">
    <h2>🎮 Οι κινήσεις σου</h2>
    <div class="actions">
      <button id="attackBtn" onclick="playerMove('attack')">⚔️ Επίθεση</button>
      <button class="danger" id="heavyBtn" onclick="playerMove('heavy')">💥 Δυνατή επίθεση</button>
      <button class="defend" id="defendBtn" onclick="playerMove('defend')">🛡️ Άμυνα</button>
    </div>
    <div class="notice">Η δυνατή επίθεση κάνει περισσότερη ζημιά, αλλά μπορεί να αστοχήσει. Η άμυνα μειώνει το επόμενο χτύπημα.</div>
  </section>

  <section class="card" style="margin-top:16px">
    <h2>🛒 Αναβαθμίσεις</h2>
    <div class="shop">
      <button class="secondary" onclick="buy('weapon')">⚔️ Ακόνισε όπλο — 30 🪙<br><small>+4 δύναμη</small></button>
      <button class="secondary" onclick="buy('armor')">🛡️ Καλύτερη πανοπλία — 30 🪙<br><small>+3 άμυνα</small></button>
      <button class="secondary" onclick="buy('potion')">🧪 Φίλτρο ζωής — 20 🪙<br><small>+35 ζωή</small></button>
    </div>
  </section>

  <section class="card" style="margin-top:16px">
    <h2>📜 Ιστορικό μάχης</h2><div class="log" id="log" aria-live="polite">Καλώς ήρθες στην αρένα! Κάνε την πρώτη σου κίνηση.</div>
    <div class="actions" style="grid-template-columns:1fr 1fr">
      <button onclick="newEnemy()">➡️ Επόμενος αντίπαλος</button>
      <button class="secondary" onclick="resetGame()">🔄 Νέο παιχνίδι</button>
    </div>
  </section>
</main>
<script>
const enemies=[
 {name:"Άγριος λύκος",art:"🐺",hp:60,atk:9,coins:15,xp:20},
 {name:"Σκελετός πολεμιστής",art:"💀",hp:80,atk:12,coins:22,xp:28},
 {name:"Ορκ",art:"👹",hp:110,atk:15,coins:30,xp:35},
 {name:"Μικρός δράκος",art:"🐉",hp:145,atk:19,coins:45,xp:45},
 {name:"Σκοτεινός ιππότης",art:"🦹",hp:185,atk:23,coins:60,xp:55}
];
let hero={hp:100,maxHp:100,atk:15,def:5,coins:0,xp:0,level:1};
let enemy,enemyIndex=0,guarding=false,won=false,turn=0;
const $=id=>document.getElementById(id);
function log(msg){$("log").innerHTML+=`<div>${msg}</div>`;$("log").scrollTop=$("log").scrollHeight}
function render(){
 $("coins").textContent=hero.coins;$("level").textContent=hero.level;$("xp").textContent=hero.xp;$("nextxp").textContent=hero.level*50;
 $("heroHpText").textContent=`${hero.hp} / ${hero.maxHp}`;$("heroBar").style.width=(hero.hp/hero.maxHp*100)+"%";
 $("attackStat").textContent=hero.atk;$("defStat").textContent=hero.def;
 $("enemyName").textContent=enemy.name;$("enemyArt").textContent=enemy.art;$("enemyHpText").textContent=`${enemy.hp} / ${enemy.maxHp}`;$("enemyBar").style.width=Math.max(0,enemy.hp/enemy.maxHp*100)+"%";$("enemyAttack").textContent=enemy.atk;
 const disabled=won||hero.hp<=0;
 ["attackBtn","heavyBtn","defendBtn"].forEach(id=>$(id).disabled=disabled);
}
function spawnEnemy(){
 const base=enemies[enemyIndex%enemies.length],scale=1+Math.floor(enemyIndex/enemies.length)*.35;
 enemy={...base,maxHp:Math.round(base.hp*scale),hp:Math.round(base.hp*scale),atk:Math.round(base.atk*scale)};
 won=false;guarding=false;$("enemyHint").textContent="Νίκησέ τον για να πάρεις ανταμοιβές.";render();
}
function enemyTurn(){
 if(enemy.hp<=0)return;
 let raw=enemy.atk+Math.floor(Math.random()*5),damage=Math.max(1,raw-hero.def-(guarding?12:0));
 hero.hp=Math.max(0,hero.hp-damage);guarding=false;
 log(`👹 Ο ${enemy.name} σου έκανε ${damage} ζημιά.`);
 if(hero.hp<=0){log("💀 Έπεσες στη μάχη. Πάτησε «Νέο παιχνίδι» για να ξαναρχίσεις.");$("enemyHint").textContent="Ηττήθηκες!";}render();
}
function playerMove(move){
 if(won||hero.hp<=0)return;
 turn++;
 if(move==="attack"){let d=hero.atk+Math.floor(Math.random()*6);enemy.hp=Math.max(0,enemy.hp-d);log(`⚔️ Χτύπησες για ${d} ζημιά.`);}
 if(move==="heavy"){if(Math.random()<.25){log("💨 Η δυνατή επίθεση αστόχησε!");}else{let d=Math.round(hero.atk*1.9+Math.random()*5);enemy.hp=Math.max(0,enemy.hp-d);log(`💥 Δυνατό χτύπημα! ${d} ζημιά.`);}}
 if(move==="defend"){guarding=true;log("🛡️ Παίρνεις αμυντική στάση. Το επόμενο χτύπημα θα είναι πιο αδύναμο.");}
 render();
 if(enemy.hp<=0){winBattle();return;}
 enemyTurn();
}
function winBattle(){
 won=true;hero.coins+=enemy.coins;hero.xp+=enemy.xp;
 log(`🏆 Νίκη! Κέρδισες ${enemy.coins} coins και ${enemy.xp} XP.`);
 while(hero.xp>=hero.level*50){hero.xp-=hero.level*50;hero.level++;hero.maxHp+=10;hero.atk+=2;hero.hp=Math.min(hero.maxHp,hero.hp+20);log(`⭐ Ανέβηκες στο level ${hero.level}! +2 δύναμη, +10 μέγιστη ζωή.`);}
 $("enemyHint").textContent="Νίκησες! Πάτησε «Επόμενος αντίπαλος».";render();
}
function newEnemy(){if(!won&&hero.hp>0){log("Πρέπει πρώτα να τελειώσεις αυτή τη μάχη.");return;}enemyIndex++;spawnEnemy();log(`⚔️ Εμφανίστηκε: ${enemy.name}!`);}
function buy(type){
 if(type==="weapon"){if(hero.coins<30)return log("Δεν έχεις αρκετά coins.");hero.coins-=30;hero.atk+=4;log("⚔️ Το όπλο αναβαθμίστηκε! +4 δύναμη.");}
 if(type==="armor"){if(hero.coins<30)return log("Δεν έχεις αρκετά coins.");hero.coins-=30;hero.def+=3;log("🛡️ Η πανοπλία αναβαθμίστηκε! +3 άμυνα.");}
 if(type==="potion"){if(hero.coins<20)return log("Δεν έχεις αρκετά coins.");if(hero.hp===hero.maxHp)return log("Η ζωή σου είναι ήδη γεμάτη.");hero.coins-=20;let before=hero.hp;hero.hp=Math.min(hero.maxHp,hero.hp+35);log(`🧪 Ανέκτησες ${hero.hp-before} ζωή.`);}
 render();
}
function resetGame(){hero={hp:100,maxHp:100,atk:15,def:5,coins:0,xp:0,level:1};enemyIndex=0;guarding=false;$("log").innerHTML="Ξεκίνησες από την αρχή. Καλή μάχη!";spawnEnemy();}
spawnEnemy();
</script>
</body>
</html>
