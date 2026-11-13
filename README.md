<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="color-scheme" content="dark">
<title>Старт</title>
<style>
:root{
  --bg:#0c0c10; --ink:#f4f1ec; --dim:rgba(244,241,236,.55);
  --glass:rgba(255,255,255,.08); --edge:rgba(255,255,255,.2);
  --accent:#F8BD88;
}
*{box-sizing:border-box;margin:0;-webkit-tap-highlight-color:transparent}
html,body{min-height:100%;background:var(--bg);color:var(--ink);
  font-family:-apple-system,"SF Pro Display","Helvetica Neue",Arial,sans-serif}
body{padding:calc(env(safe-area-inset-top,0px) + 28px) 18px calc(env(safe-area-inset-bottom,0px) + 90px);
  position:relative;overflow-x:hidden}
.orb{position:fixed;border-radius:50%;filter:blur(70px);opacity:.55;z-index:0;pointer-events:none}
.o1{width:300px;height:300px;background:#e8803a;top:-80px;left:-90px}
.o2{width:320px;height:320px;background:#5a4bd6;top:38%;right:-140px}
.o3{width:260px;height:260px;background:#c7527a;bottom:-60px;left:10%}
main{position:relative;z-index:1;max-width:560px;margin:0 auto}
.glass{background:var(--glass);border:1px solid var(--edge);
  -webkit-backdrop-filter:blur(26px) saturate(170%);backdrop-filter:blur(26px) saturate(170%);
  box-shadow:inset 0 1px 0 rgba(255,255,255,.28),0 10px 30px rgba(0,0,0,.3)}
.clock{text-align:center;padding:6px 0 22px}
#time{font-size:76px;font-weight:200;letter-spacing:-2px;line-height:1}
#date{margin-top:8px;font-size:16px;color:var(--dim);text-transform:capitalize}
form.search{display:flex;align-items:center;gap:10px;border-radius:999px;padding:6px 8px 6px 18px;margin-bottom:22px}
form.search input{flex:1;min-width:0;background:none;border:0;outline:0;color:var(--ink);font-size:17px;padding:10px 0}
form.search input::placeholder{color:var(--dim)}
form.search button{width:38px;height:38px;border-radius:50%;border:0;background:var(--accent);color:#1b1208;font-size:18px}
section.group{border-radius:28px;padding:16px 14px 14px;margin-bottom:16px}
h2{font-size:15px;font-weight:600;color:var(--accent);margin:0 6px 12px}
.tiles{display:grid;grid-template-columns:repeat(3,1fr);gap:10px}
a.tile{display:flex;flex-direction:column;align-items:center;gap:8px;padding:12px 6px 10px;border-radius:20px;
  text-decoration:none;color:var(--ink);background:rgba(255,255,255,.06);border:1px solid rgba(255,255,255,.1);
  transition:transform .15s,background .15s}
a.tile:active{transform:scale(.95);background:rgba(255,255,255,.14)}
a.tile:focus-visible{outline:2px solid var(--accent)}
.ico{width:46px;height:46px;border-radius:12px;background:rgba(255,255,255,.12);display:grid;place-items:center;
  overflow:hidden;font-size:20px;font-weight:600}
.ico img{width:30px;height:30px;border-radius:6px}
.name{font-size:12px;text-align:center;line-height:1.2;max-width:100%;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
</style>
</head>
<body>
<div class="orb o1"></div><div class="orb o2"></div><div class="orb o3"></div>
<main>
  <div class="clock"><div id="time">--:--</div><div id="date"></div></div>
  <form class="search glass" action="https://duckduckgo.com/"
    method="get">
    <input name="q" type="search" placeholder="Поиск" autocomplete="off" aria-label="Поиск">
    <button type="submit" aria-label="Искать">&#8250;</button>
  </form>
  <div id="groups"></div>
</main>
<script>
const GROUPS = [
  {title:"Additional", links:[
    ["Depositphotos","https://depositphotos.com/ru/photos/%D1%82%D1%86-%D0%BC%D0%B0%D0%BD%D1%83%D1%84%D0%B0%D0%BA%D1%82%D1%83%D1%80%D0%B0.html?offset=150&filter=all"],
    ["Символы","https://symbl.cc/ru/unicode-table/"],
    ["Номера","https://ru.piliapp.com/symbol/number/"]]},
  {title:"Треш", links:[
    ["BoyfriendTV","https://www.boyfriendtv.com/"],
    ["Apple","http://www.apple.com/"]]},
  {title:"Interface", links:[
    ["Apple","http://www.apple.com/"],
    ["Themes","https://themes.contest.com/"],
    ["App Store","https://logos.fandom.com/wiki/App_Store_(iOS)"]]},
  {title:"Craft", links:[
    ["Depositphotos","https://depositphotos.com/ru/"]]}
];
const root=document.getElementById("groups");
GROUPS.forEach(g=>{
  const s=document.createElement("section");s.className="group glass";
  const h=document.createElement("h2");h.textContent=g.title;s.appendChild(h);
  const t=document.createElement("div");t.className="tiles";
  g.links.forEach(([name,url])=>{
    const a=document.createElement("a");a.className="tile";a.href=url;
    const i=document.createElement("div");i.className="ico";i.textContent=name[0];
    const img=new Image();
    img.alt="";img.src="https://www.google.com/s2/favicons?sz=64&domain="+new URL(url).hostname;
    img.onload=()=>{i.textContent="";i.appendChild(img)};
    const n=document.createElement("div");n.className="name";n.textContent=name;
    a.append(i,n);t.appendChild(a);
  });
  s.appendChild(t);root.appendChild(s);
});
function tick(){
  const d=new Date();
  document.getElementById("time").textContent=d.toLocaleTimeString("ru-RU",{hour:"2-digit",minute:"2-digit"});
  document.getElementById("date").textContent=d.toLocaleDateString("ru-RU",{weekday:"long",day:"numeric",month:"long"});
}
tick();setInterval(tick,1000);
</script>
</body>
</html>
