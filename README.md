
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Legends of the Arena</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@500;600;700;900&family=Inter:wght@400;500;600;700;800&display=swap');
:root{--gold:#d8b36b;--red:#b83d46;--bg:#090a10;--panel:#151720;--muted:#9699a8;--line:#343744;--blue:#6d9ce7}
*{box-sizing:border-box}
body{margin:0;background:radial-gradient(ellipse at 50% -10%,#442c36 0%,#15141d 45%,#08090e 100%);color:#f3eee5;font-family:Inter,sans-serif;min-height:100vh}
button{font:inherit;cursor:pointer}
button:disabled{opacity:.35;cursor:not-allowed}
.top{display:flex;justify-content:space-between;align-items:center;padding:16px 5%;background:#08090ddf;border-bottom:1px solid #ffffff17;position:sticky;top:0;z-index:5;backdrop-filter:blur(12px);gap:15px}
.logo{font:900 21px Cinzel;color:var(--gold);letter-spacing:2px}
.resources{display:flex;gap:16px;font-size:12px;color:#e8d8b7;flex-wrap:wrap}
.wrap{max-width:1160px;margin:auto;padding:26px 18px}
h1,h2,h3{font-family:Cinzel,serif}
h1{text-align:center;font-size:clamp(29px,5vw,52px);color:var(--gold);text-shadow:0 0 35px #b77a454c;margin:8px 0}
.subtitle{text-align:center;color:#a8a1a2;font-size:10px;letter-spacing:5px;margin-bottom:28px}
.panel{background:linear-gradient(145deg,#1b1c27,#11131b);border:1px solid var(--line);border-radius:13px;box-shadow:0 15px 40px #0005}
.section-title{text-align:center;color:var(--gold);letter-spacing:2px;font-size:19px}
.muted{color:var(--muted)}
.center{text-align:center}
.btn{border:1px solid #947143;background:linear-gradient(180deg,#9c7443,#5d4026);color:#fff0d4;border-radius:7px;padding:12px 17px;font-weight:800;transition:.2s}
.btn:hover{filter:brightness(1.2);transform:translateY(-2px)}
.btn.red{background:linear-gradient(#9f3944,#571e2b);border-color:#a34b51}
.btn.blue{background:linear-gradient(#345e94,#1d304c);border-color:#5276a6}
.btn.dark{background:#252733;border-color:#4a4c59}
.selection{padding:22px}
.heroes{display:grid;grid-template-columns:repeat(3,1fr);gap:15px;margin:22px 0}
.hero{padding:13px;border-radius:12px;background:#11131c;border:1px solid #373947;cursor:pointer;text-align:center;transition:.2s}
.hero:hover,.hero.selected{border-color:var(--gold);box-shadow:0 0 24px #d8b36b24;transform:translateY(-3px)}
.hero h3{color:var(--gold);margin:8px 0}
.hero p{font-size:12px;line-height:1.6;color:var(--muted);min-height:40px}
.art{width:100%;max-width:190px;height:205px;margin:auto;display:block}
.art.big{max-width:250px;height:250px}
.art svg{width:100%;height:100%;overflow:visible;filter:drop-shadow(0 14px 10px #0009)}
.art .float{transform-origin:50% 90%;animation:float 3s ease-in-out infinite}
.art .glow{animation:glow 2s ease-in-out infinite alternate}
@keyframes float{0%,100%{transform:translateY(0)}50%{transform:translateY(-6px)}}
@keyframes glow{from{opacity:.45}to{opacity:1}}
@keyframes slash{0%{transform:translateX(-50px) rotate(-20deg);opacity:0}40%{opacity:1}100%{transform:translateX(40px) rotate(20deg);opacity:0}}
@keyframes hit{0%,100%{transform:translateX(0)}25%{transform:translateX(-9px)}60%{transform:translateX(8px)}}
@keyframes pulse{0%,100%{filter:drop-shadow(0 0 2px #f5c36a)}50%{filter:drop-shadow(0 0 20px #e5a34d)}}
.fighter.hit{animation:hit .3s}
.battle{display:grid;grid-template-columns:1fr 1fr;gap:15px;margin-top:18px}
.fighter{padding:17px;text-align:center;position:relative;overflow:hidden}
.fighter.enemy{background:linear-gradient(140deg,#29161e,#17141c)}
.fighter.player{background:linear-gradient(140deg,#192235,#15151d)}
.fighter h2{font-size:18px;color:var(--gold);margin:3px}
.level{font-size:10px;letter-spacing:3px;color:#a6a4ad}
.bar{height:10px;background:#08090e;border-radius:20px;overflow:hidden;border:1px solid #ffffff17;margin:8px 0 4px}
.fill{height:100%;transition:width .35s}
.hp{background:linear-gradient(90deg,#8b2637,#ed5a61)}
.mp{background:linear-gradient(90deg,#2552a1,#69b7ef)}
.xp{background:linear-gradient(90deg,#8c632a,#f4ce75)}
.barlabel{display:flex;justify-content:space-between;font-size:10px;color:#aaa}
.actions{padding:18px;margin-top:15px}
.actions h3,.shop h3,.chronicle h3{color:var(--gold);text-align:center;margin:0 0 14px}
.action-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:10px}
.action-grid button{min-height:62px}
.chronicle,.shop{padding:17px;margin-top:15px}
.log{font-size:12px;line-height:1.8;color:#c6c4cb;max-height:130px;overflow:auto}
.log div{border-bottom:1px solid #ffffff0d;padding:2px}
.shopgrid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px}
.item{background:#20212c;border:1px solid #3d3d49;border-radius:9px;padding:13px}
.item strong{color:#ead3a8;font-size:13px}
.item p{font-size:11px;color:var(--muted);min-height:32px}
.item button{width:100%;padding:9px;font-size:11px}
.bottom{display:flex;gap:9px;justify-content:center;flex-wrap:wrap;margin-top:16px}
.hidden{display:none!important}
.battle-actions{display:flex;gap:8px;justify-content:center;flex-wrap:wrap;margin-top:10px}
@media(max-width:680px){.top{align-items:flex-start;flex-direction:column}.heroes{grid-template-columns:1fr}.hero{display:grid;grid-template-columns:110px 1fr;text-align:left;align-items:center}.hero .art{height:140px}.hero p{min-height:0}.battle{grid-template-columns:1fr}.action-grid{grid-template-columns:repeat(2,1fr)}.shopgrid{grid-template-columns:1fr}.art.big{height:210px}}
</style>
</head>
<body>
<header class="top">
 <div class="logo">⚔ LEGENDS OF THE ARENA</div>
 <div class="resources">
  <span>⭐ LV <b id="topLevel">1</b></span>
  <span>🪙 <b id="topGold">100</b></span>
  <span>🏆 <b id="topWins">0</b></span>
 </div>
</header>
<main class="wrap">
 <h1>LEGENDS OF THE ARENA</h1>
 <div class="subtitle">RISE FROM THE ASHES · CLAIM YOUR DESTINY</div>

 <section id="menu" class="panel selection">
  <h2 class="section-title">CHOOSE YOUR CHAMPION</h2>
  <p class="center muted">Three paths. One legend. Choose wisely.</p>
  <div class="heroes">
   <div class="hero selected" data-hero="knight" onclick="selectHero('knight')">
    <div class="art" id="knightArt"></div><div><h3>THE KNIGHT</h3><p>Steel, courage and an unbreakable shield.</p><small>140 HP · 18 ATTACK</small></div>
   </div>
   <div class="hero" data-hero="mage" onclick="selectHero('mage')">
    <div class="art" id="mageArt"></div><div><h3>THE MAGE</h3><p>Ancient magic burns within this spellcaster.</p><small>105 HP · 15 ATTACK</small></div>
   </div>
   <div class="hero" data-hero="assassin" onclick="selectHero('assassin')">
    <div class="art" id="assassinArt"></div><div><h3>THE ASSASSIN</h3><p>Silent blades. Deadly speed. No mercy.</p><small>115 HP · 17 ATTACK</small></div>
   </div>
  </div>
  <div class="center"><button class="btn" onclick="begin()">ENTER THE ARENA</button></div>
 </section>

 <section id="game" class="hidden">
  <div class="battle">
   <div class="fighter player panel" id="playerFighter">
    <div class="level">YOUR CHAMPION</div><div class="art big" id="playerArt"></div>
    <h2 id="playerName">THE KNIGHT</h2><div class="level" id="playerLevel">LEVEL 1</div>
    <div class="bar"><div id="pHP" class="fill hp"></div></div><div class="barlabel"><span>HEALTH</span><span id="pHPText"></span></div>
    <div class="bar"><div id="pMP" class="fill mp"></div></div><div class="barlabel"><span>MANA</span><span id="pMPText"></span></div>
    <div class="bar"><div id="pXP" class="fill xp"></div></div><div class="barlabel"><span>EXPERIENCE</span><span id="pXPText"></span></div>
   </div>
   <div class="fighter enemy panel" id="enemyFighter">
    <div class="level">YOUR OPPONENT</div><div class="art big" id="enemyArt"></div>
    <h2 id="enemyName">SHADOW WOLF</h2><div class="level" id="enemyLevel">LEVEL 1</div>
    <div class="bar"><div id="eHP" class="fill hp"></div></div><div class="barlabel"><span>ENEMY HEALTH</span><span id="eHPText"></span></div>
    <p id="enemyDesc" class="muted" style="font-size:11px"></p>
   </div>
  </div>
  <div class="panel actions">
   <h3>⚔ BATTLE COMMAND</h3>
   <div class="action-grid">
    <button class="btn" id="attack" onclick="act('attack')">⚔<br>ATTACK</button>
    <button class="btn red" id="heavy" onclick="act('heavy')">✦<br>HEAVY STRIKE</button>
    <button class="btn blue" id="skill" onclick="act('skill')">✧<br>SPECIAL SKILL</button>
    <button class="btn dark" id="defend" onclick="act('defend')">🛡<br>DEFEND</button>
   </div>
   <div class="battle-actions">
    <button class="btn dark" onclick="potion()">HEALTH POTION · <span id="potionCount">2</span></button>
    <button class="btn dark" onclick="manaPotion()">MANA ELIXIR · <span id="manaCount">1</span></button>
   </div>
  </div>
  <div class="panel chronicle"><h3>📜 BATTLE CHRONICLE</h3><div id="log" class="log"></div></div>
  <div class="panel shop">
   <h3>⚒ THE BLACKSMITH</h3>
   <div class="shopgrid">
    <div class="item"><strong>⚔ Forged Blade</strong><p>Increase attack by 5.</p><button class="btn" onclick="buy('weapon')">100 GOLD</button></div>
    <div class="item"><strong>🛡 Iron Armor</strong><p>Reduce incoming damage by 3.</p><button class="btn" onclick="buy('armor')">100 GOLD</button></div>
    <div class="item"><strong>🧪 Health Potion</strong><p>Restore one health potion.</p><button class="btn" onclick="buy('potion')">40 GOLD</button></div>
   </div>
  </div>
  <div class="bottom">
   <button class="btn dark" onclick="backMenu()">CHARACTER MENU</button>
   <button class="btn dark" onclick="resetSave()">RESET PROGRESS</button>
  </div>
 </section>
</main>
<script>
// Original vector character artwork, included directly in this file.
const artwork={
knight:`<svg viewBox="0 0 200 240"><defs><linearGradient id="karm" x2="1" y2="1"><stop stop-color="#cbd1dc"/><stop offset=".5" stop-color="#596273"/><stop offset="1" stop-color="#252c3c"/></linearGradient><linearGradient id="kcape"><stop stop-color="#781f2d"/><stop offset="1" stop-color="#30121e"/></linearGradient></defs><ellipse cx="100" cy="224" rx="60" ry="9" fill="#000" opacity=".5"/><g class="float"><path d="M68 94 L48 206 L99 220 L124 205 L135 104Z" fill="url(#kcape)" stroke="#a94c4b" stroke-width="2"/><path d="M67 106 L53 202 L92 214 L104 118Z" fill="#67202c"/><path d="M71 132 L60 205 L89 210 L99 139Z" fill="url(#karm)" stroke="#aeb7c7"/><path d="M105 132 L117 205 L91 210 L98 139Z" fill="#434b5c" stroke="#aeb7c7"/><path d="M66 104 L53 144 L77 153 L91 129 L111 153 L136 141 L123 101 L100 91Z" fill="url(#karm)" stroke="#c4cbd7" stroke-width="2"/><path d="M76 105 L100 120 L123 105 L117 148 L83 148Z" fill="#394356"/><path d="M78 35 Q100 16 122 36 L127 76 L113 97 L87 97 L73 76Z" fill="url(#karm)" stroke="#d3d8e0" stroke-width="3"/><path d="M75 55 L125 55 L122 73 L78 73Z" fill="#1a202e"/><path d="M85 64 L96 64 M105 64 L116 64" stroke="#e9b85e" stroke-width="4"/><path d="M100 26 L100 91" stroke="#d7dbe2" stroke-width="2"/><path d="M69 110 L37 154 L53 167 L84 130 M126 110 L157 151 L142 168 L115 132" fill="url(#karm)" stroke="#bbc3d0" stroke-width="3"/><path d="M43 151 L30 174 L56 183 L67 158Z" fill="#792532"/><path d="M143 150 L158 175 L137 184 L127 158Z" fill="#792532"/><path d="M38 174 L24 208 L30 211 L54 181Z" fill="#d3d7e0"/><path d="M158 175 L172 208 L166 211 L143 181Z" fill="#d3d7e0"/><path d="M90 147 L110 147" stroke="#d9b66d" stroke-width="5"/><circle cx="100" cy="144" r="7" fill="#b88b45"/></g></svg>`,
mage:`<svg viewBox="0 0 200 240"><defs><linearGradient id="mrobe" x2="1" y2="1"><stop stop-color="#5654a4"/><stop offset="1" stop-color="#171b40"/></linearGradient><radialGradient id="orb"><stop stop-color="#e6f5ff"/><stop offset=".35" stop-color="#62c8ff"/><stop offset="1" stop-color="#3150d2" stop-opacity="0"/></radialGradient></defs><ellipse cx="100" cy="224" rx="58" ry="9" fill="#000" opacity=".5"/><g class="float"><path d="M67 82 L36 214 L164 214 L128 82Z" fill="url(#mrobe)" stroke="#7778cb" stroke-width="2"/><path d="M100 95 L100 213 M70 142 L130 142" stroke="#b7a8e9" stroke-width="2"/><path d="M68 82 L100 105 L132 82 L119 60 L81 60Z" fill="#7770bc"/><path d="M78 40 Q100 18 122 40 L126 74 L112 94 L88 94 L74 74Z" fill="#b78b70" stroke="#e3c1a1" stroke-width="2"/><path d="M70 49 L100 2 L132 50 L117 44 L100 27 L84 47Z" fill="#29264f" stroke="#9b91d4" stroke-width="3"/><path d="M83 67 L96 67 M105 67 L117 67" stroke="#54d4ff" stroke-width="4"/><path d="M55 94 L35 157 L65 163 L81 111 M145 94 L165 157 L135 163 L119 111" fill="#34336f" stroke="#8c83c7" stroke-width="3"/><path d="M43 149 L32 177 L57 184 L70 159" fill="#b98e72"/><path d="M158 149 L169 177 L144 184 L131 159" fill="#b98e72"/><path d="M154 80 L157 210" stroke="#8d6d48" stroke-width="7"/><circle cx="157" cy="72" r="23" fill="url(#orb)" class="glow"/><circle cx="157" cy="72" r="9" fill="#9be6ff"/><path d="M93 108 L100 121 L107 108" fill="none" stroke="#e1c37c" stroke-width="3"/></g></svg>`,
assassin:`<svg viewBox="0 0 200 240"><defs><linearGradient id="arobe" x2="1" y2="1"><stop stop-color="#414451"/><stop offset="1" stop-color="#10121a"/></linearGradient></defs><ellipse cx="100" cy="224" rx="58" ry="9" fill="#000" opacity=".5"/><g class="float"><path d="M67 91 L43 212 L101 218 L133 205 L130 92Z" fill="#22232e" stroke="#666a7c" stroke-width="2"/><path d="M78 105 L60 205 L92 213 L101 121Z" fill="#4c2434"/><path d="M100 121 L119 210 L143 196 L123 103Z" fill="#161a26"/><path d="M68 91 L53 126 L80 145 L101 112 L124 145 L148 124 L128 89 L100 81Z" fill="url(#arobe)" stroke="#7d8394" stroke-width="2"/><path d="M77 34 Q100 12 123 34 L127 70 L111 91 L88 91 L73 70Z" fill="#292c39" stroke="#888da0" stroke-width="2"/><path d="M72 48 L128 48 L122 68 L78 68Z" fill="#11121b"/><path d="M84 57 L96 57 M104 57 L116 57" stroke="#e95e72" stroke-width="4"/><path d="M70 101 L31 147 L44 163 L83 127 M130 101 L168 145 L154 162 L118 127" fill="#292d3c" stroke="#747a8a" stroke-width="3"/><path d="M39 151 L12 197 L19 201 L54 165Z" fill="#cbd3e0" stroke="#71839e" stroke-width="2"/><path d="M160 151 L188 197 L181 201 L145 165Z" fill="#cbd3e0" stroke="#71839e" stroke-width="2"/><path d="M85 143 L115 143" stroke="#b34a60" stroke-width="5"/><path d="M100 95 L100 210" stroke="#55596a" stroke-width="2"/></g></svg>`,
wolf:`<svg viewBox="0 0 200 220"><ellipse cx="100" cy="205" rx="64" ry="9" fill="#000" opacity=".5"/><g class="float"><path d="M39 114 L23 76 L62 91 L83 71 L128 80 L164 113 L147 156 L119 174 L61 162Z" fill="#555968" stroke="#959aaa" stroke-width="3"/><path d="M60 91 L43 37 L88 70 L105 58 L145 31 L133 90Z" fill="#404653" stroke="#a3a9b8" stroke-width="3"/><path d="M52 53 L68 72 L60 76Z M127 60 L144 48 L134 75Z" fill="#a23c52"/><path d="M143 112 L184 121 L156 141 L137 137Z" fill="#737989"/><path d="M69 153 L58 195 L76 195 L91 161 M122 155 L126 197 L145 196 L141 144" fill="#454957" stroke="#a0a6b2" stroke-width="3"/><circle cx="119" cy="96" r="5" fill="#f3bc59" class="glow"/><path d="M166 122 L180 123" stroke="#d9b6a0" stroke-width="3"/></g></svg>`,
skeleton:`<svg viewBox="0 0 200 220"><ellipse cx="100" cy="206" rx="55" ry="8" fill="#000" opacity=".5"/><g class="float" stroke="#c8c4b8" stroke-width="7" stroke-linecap="round" fill="none"><path d="M79 111 L60 158 L69 195 M121 111 L140 158 L131 195 M83 144 L64 180 M117 144 L136 180 M77 109 L49 139 M123 109 L151 139"/><path d="M80 109 L120 109 L128 145 L72 145Z" fill="#888879"/><path d="M85 105 L80 70 Q100 50 120 70 L115 105Z" fill="#d8d3c2"/><path d="M87 80 L96 80 M104 80 L113 80" stroke="#a42f43" stroke-width="8"/><path d="M88 96 L112 96" stroke="#77776d" stroke-width="3"/><path d="M90 145 L83 190 M110 145 L117 190"/></g></svg>`,
orc:`<svg viewBox="0 0 200 220"><ellipse cx="100" cy="207" rx="62" ry="9" fill="#000" opacity=".5"/><g class="float"><path d="M52 91 L42 62 L68 76 L132 76 L158 61 L148 98 L159 153 L136 193 L64 193 L41 150Z" fill="#5d7854" stroke="#a2a978" stroke-width="3"/><path d="M60 47 Q100 18 140 47 L135 101 L117 125 L83 125 L65 101Z" fill="#789465" stroke="#bac28b" stroke-width="3"/><path d="M62 50 L35 33 L53 78 M138 50 L165 33 L147 78" fill="#e4d6b4" stroke="#a2a978" stroke-width="3"/><path d="M70 76 L93 76 M107 76 L130 76" stroke="#24221e" stroke-width="7"/><circle cx="82" cy="76" r="4" fill="#ffb84e"/><circle cx="118" cy="76" r="4" fill="#ffb84e"/><path d="M81 104 L100 112 L119 104" fill="none" stroke="#362b26" stroke-width="6"/><path d="M77 110 L88 132 L100 112 L112 132 L123 110" fill="#e8e0c9"/><path d="M63 126 L39 172 L63 187 L82 140 M137 126 L161 172 L137 187 L118 140" fill="#566b4b" stroke="#b5bd8d" stroke-width="3"/><path d="M72 143 L128 143 L139 179 L61 179Z" fill="#4b3630" stroke="#ba9864" stroke-width="3"/></g></svg>`,
dragon:`<svg viewBox="0 0 240 220"><ellipse cx="120" cy="205" rx="78" ry="8" fill="#000" opacity=".5"/><g class="float"><path d="M90 105 L25 38 L39 119 L81 153 M149 102 L216 35 L197 129 L160 158" fill="#6c2732" stroke="#d05b49" stroke-width="4"/><path d="M78 99 L46 61 L82 78 M164 96 L198 60 L162 79" fill="#a3423c"/><path d="M66 98 Q110 57 165 99 L175 156 L148 185 L84 180 L60 145Z" fill="#722b36" stroke="#dc7754" stroke-width="3"/><path d="M88 117 L45 138 L62 158 L104 146 M151 117 L192 138 L174 158 L137 146" fill="#81333b" stroke="#dc7754" stroke-width="3"/><path d="M85 97 L75 64 L103 80 L120 47 L137 80 L165 62 L153 105" fill="#7b303a" stroke="#dc7754" stroke-width="3"/><path d="M88 115 Q120 91 151 115 L147 141 L92 141Z" fill="#bb5945"/><path d="M100 118 L109 118 M131 118 L140 118" stroke="#ffcf61" stroke-width="5"/><path d="M104 142 L120 154 L136 142" fill="none" stroke="#351a20" stroke-width="5"/><path d="M86 174 L77 198 L100 196 L111 174 M139 174 L150 198 L171 195 L154 169" fill="#6d2834" stroke="#dc7754" stroke-width="3"/><path d="M157 152 Q203 163 209 188 Q180 175 168 185" fill="none" stroke="#a84443" stroke-width="10"/></g></svg>`
};
const heroData={
 knight:{name:"THE KNIGHT",hp:140,mp:55,atk:18,skill:"SHIELD BREAKER",art:artwork.knight},
 mage:{name:"THE MAGE",hp:105,mp:110,atk:15,skill:"ARCANE BLAST",art:artwork.mage},
 assassin:{name:"THE ASSASSIN",hp:115,mp:75,atk:17,skill:"SHADOW STRIKE",art:artwork.assassin}
};
const foes=[
 {name:"SHADOW WOLF",hp:55,atk:9,art:artwork.wolf,desc:"A predator from the forgotten forest."},
 {name:"SKELETON WARRIOR",hp:75,atk:12,art:artwork.skeleton,desc:"An ancient warrior risen from the grave."},
 {name:"ORC BRUTE",hp:100,atk:15,art:artwork.orc,desc:"A brutal champion of the dark tribes."},
 {name:"DARK KNIGHT",hp:130,atk:18,art:artwork.knight,desc:"A fallen champion in cursed armor."},
 {name:"FIRE DEMON",hp:155,atk:21,art:artwork.orc,desc:"A creature forged in the depths of fire."},
 {name:"CAVE TROLL",hp:190,atk:23,art:artwork.orc,desc:"An enormous beast of terrifying strength."},
 {name:"FROST WRAITH",hp:220,atk:25,art:artwork.skeleton,desc:"A spirit that brings endless winter."},
 {name:"ANCIENT GOLEM",hp:260,atk:28,art:artwork.orc,desc:"A guardian of forgotten kingdoms."},
 {name:"WYVERN",hp:300,atk:31,art:artwork.dragon,desc:"A winged monster that rules the skies."},
 {name:"THE ANCIENT DRAGON",hp:420,atk:37,art:artwork.dragon,desc:"The ultimate ruler of the arena."}
];
let s={
 hero:"knight",level:1,xp:0,gold:100,wins:0,
 hp:140,mp:55,maxHP:140,maxMP:55,atk:18,armor:0,
 potions:2,manaPotions:1,weapon:0,armorUp:0,
 enemyIndex:0,enemyHP:55,enemyMax:55,
 started:false,defending:false,skillReady:true
};
let selected="knight";
function $(id){return document.getElementById(id)}
function save(){localStorage.setItem("lotA_full_v1",JSON.stringify(s))}
function load(){
 try{let d=JSON.parse(localStorage.getItem("lotA_full_v1"));if(d&&heroData[d.hero]&&Number.isFinite(d.hp))s={...s,...d}}catch(e){}
}
function selectHero(h){
 selected=h;
 document.querySelectorAll(".hero").forEach(x=>x.classList.toggle("selected",x.dataset.hero===h));
}
function artInit(){
 $("knightArt").innerHTML=artwork.knight;
 $("mageArt").innerHTML=artwork.mage;
 $("assassinArt").innerHTML=artwork.assassin;
}
function begin(){
 if(!s.started){
  let h=heroData[selected];s.hero=selected;s.maxHP=h.hp;s.hp=h.hp;s.maxMP=h.mp;s.mp=h.mp;s.atk=h.atk;s.started=true;s.enemyIndex=0;spawn();
 }
 $("menu").classList.add("hidden");$("game").classList.remove("hidden");
 render();say("You enter the arena. Your legend begins.");
}
function spawn(){
 let f=foes[s.enemyIndex%foes.length];
 let tier=Math.floor(s.enemyIndex/foes.length);
 s.enemyMax=Math.round(f.hp*(1+tier*.45));s.enemyHP=s.enemyMax;
 $("enemyArt").innerHTML=f.art;$("enemyName").textContent=f.name;
 $("enemyLevel").textContent="LEVEL "+(s.enemyIndex+1);
 $("enemyDesc").textContent=f.desc;
 s.defending=false;
}
function say(t){
 let d=document.createElement("div");d.textContent="› "+t;$("log").prepend(d);
 while($("log").children.length>28)$("log").lastChild.remove();
}
function xpNeeded(){return 100+(s.level-1)*65}
function gainXP(n){
 s.xp+=n;
 while(s.xp>=xpNeeded()){
  s.xp-=xpNeeded();s.level++;s.maxHP+=12;s.maxMP+=7;s.atk+=2;
  s.hp=s.maxHP;s.mp=s.maxMP;
  say("LEVEL UP! You reached level "+s.level+". Your power increases!");
 }
}
function render(){
 let h=heroData[s.hero],need=xpNeeded();
 $("topLevel").textContent=s.level;$("topGold").textContent=s.gold;$("topWins").textContent=s.wins;
 $("playerArt").innerHTML=h.art;$("playerName").textContent=h.name;
 $("playerLevel").textContent="LEVEL "+s.level;
 $("pHP").style.width=Math.max(0,s.hp/s.maxHP*100)+"%";
 $("pHPText").textContent=Math.max(0,s.hp)+" / "+s.maxHP;
 $("pMP").style.width=s.mp/s.maxMP*100+"%";
 $("pMPText").textContent=s.mp+" / "+s.maxMP;
 $("pXP").style.width=s.xp/need*100+"%";
 $("pXPText").textContent=s.xp+" / "+need;
 $("eHP").style.width=Math.max(0,s.enemyHP/s.enemyMax*100)+"%";
 $("eHPText").textContent=Math.max(0,s.enemyHP)+" / "+s.enemyMax;
 $("potionCount").textContent=s.potions;$("manaCount").textContent=s.manaPotions;
 $("attack").disabled=s.hp<=0||s.enemyHP<=0;
 $("heavy").disabled=s.hp<=0||s.enemyHP<=0||s.mp<15;
 $("skill").disabled=s.hp<=0||s.enemyHP<=0||s.mp<30||!s.skillReady;
 $("defend").disabled=s.hp<=0||s.enemyHP<=0;
}
function animate(id){$(id).classList.remove("hit");void $(id).offsetWidth;$(id).classList.add("hit")}
function act(type){
 if(s.hp<=0||s.enemyHP<=0)return;
 let dmg=0;
 if(type==="attack"){
  dmg=s.atk+Math.floor(Math.random()*7);
  if(s.hero==="assassin"&&Math.random()<.22){dmg*=2;say("CRITICAL STRIKE!");}
  say("You attack for "+dmg+" damage.");
 }
 if(type==="heavy"){
  if(s.mp<15)return;s.mp-=15;dmg=Math.round(s.atk*1.9+Math.random()*8);
  say("You unleash a heavy strike for "+dmg+" damage.");
 }
 if(type==="skill"){
  if(s.mp<30||!s.skillReady)return;
  s.mp-=30;s.skillReady=false;
  dmg=Math.round(s.atk*2.8+Math.random()*12);
  if(s.hero==="knight"){s.hp=Math.min(s.maxHP,s.hp+12);say("Your shield absorbs energy. You recover 12 HP.");}
  if(s.hero==="mage"){dmg=Math.round(dmg*1.25);say("ARCANE POWER EXPLODES!");}
  if(s.hero==="assassin"){dmg=Math.round(dmg*1.2);say("SHADOW STRIKE! A deadly ambush!");}
  say(heroData[s.hero].skill+" deals "+dmg+" damage.");
  $("skill").textContent="✧ RECHARGING";
  setTimeout(()=>{s.skillReady=true;$("skill").textContent="✧ SPECIAL SKILL";render();},6500);
 }
 if(type==="defend"){
  s.defending=true;s.mp=Math.min(s.maxMP,s.mp+12);
  say("You raise your guard and recover 12 mana.");enemyTurn();return;
 }
 s.enemyHP=Math.max(0,s.enemyHP-dmg);animate("enemyFighter");render();
 if(s.enemyHP<=0){victory();return}
 enemyTurn();
}
function enemyTurn(){
 let f=foes[s.enemyIndex%foes.length],tier=Math.floor(s.enemyIndex/foes.length);
 let dmg=f.atk+Math.floor(Math.random()*6)+tier*4;
 if(s.defending){dmg=Math.ceil(dmg*.25);s.defending=false;say("Your defense absorbs most of the attack!");}
 else if(Math.random()<.14){dmg=Math.round(dmg*1.5);say("The enemy lands a critical blow!");}
 let actual=Math.max(1,dmg-s.armor);s.hp=Math.max(0,s.hp-actual);
 say(f.name+" hits you for "+actual+" damage.");animate("playerFighter");
 if(s.hp<=0)say("DEFEAT. Your legend is not over. Return to the arena!");
 render();save();
}
function victory(){
 let reward=35+s.enemyIndex*15,exp=50+s.enemyIndex*24;
 s.gold+=reward;s.wins++;say("VICTORY! +"+reward+" GOLD · +"+exp+" XP");
 gainXP(exp);
 if((s.enemyIndex+1)%10===0)say("BOSS DEFEATED! You have conquered a great enemy!");
 s.enemyIndex++;
 s.hp=Math.min(s.maxHP,s.hp+Math.round(s.maxHP*.2));
 s.mp=Math.min(s.maxMP,s.mp+20);
 render();save();
 setTimeout(()=>{if(s.hp>0){spawn();say("A new challenger enters the arena!");render();save();}},1100);
}
function potion(){
 if(s.potions<1||s.hp<=0)return;
 s.potions--;let heal=Math.round(s.maxHP*.4);
 s.hp=Math.min(s.maxHP,s.hp+heal);say("Health potion restores "+heal+" HP.");
 render();save();if(s.enemyHP>0)enemyTurn();
}
function manaPotion(){
 if(s.manaPotions<1||s.hp<=0)return;
 s.manaPotions--;let amount=Math.round(s.maxMP*.5);
 s.mp=Math.min(s.maxMP,s.mp+amount);
 say("Mana elixir restores "+amount+" mana.");render();save();
 if(s.enemyHP>0)enemyTurn();
}
function buy(type){
 let cost=type==="potion"?40:100;
 if(s.gold<cost){say("Not enough gold!");return}
 if(type==="weapon"&&s.weapon>=5){say("Weapon fully upgraded!");return}
 if(type==="armor"&&s.armorUp>=5){say("Armor fully upgraded!");return}
 s.gold-=cost;
 if(type==="weapon"){s.atk+=5;s.weapon++;say("Weapon upgraded. Attack +5.");}
 if(type==="armor"){s.armor+=3;s.armorUp++;say("Armor upgraded. Defense +3.");}
 if(type==="potion"){s.potions++;say("Health potion purchased.");}
 render();save();
}
function backMenu(){$("game").classList.add("hidden");$("menu").classList.remove("hidden")}
function resetSave(){
 if(!confirm("Delete all your saved progress?"))return;
 localStorage.removeItem("lotA_full_v1");location.reload();
}
load();artInit();
if(s.started){
 $("menu").classList.add("hidden");$("game").classList.remove("hidden");
 spawn();render();
}
</script>
</body>
</html>
