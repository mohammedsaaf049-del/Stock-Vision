<!doctype html>
<html lang="fr" data-theme="auto">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>StockClair · Suivi et gestion de stock</title>
<link href="https://fonts.googleapis.com/css2?family=Barlow+Semi+Condensed:wght@500;700&family=Barlow:wght@400;500&display=swap" rel="stylesheet">
<style>
:root{--bg:#e8ebee;--panel:#fff;--ink:#1b2733;--mute:#5d6b78;--line:#cfd5db;--accent:#2f5d8a;--amber:#f2b705;--red:#c8372d;--green:#2e8b57;--orange:#d9822b;
box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#141b22;--panel:#1d2730;--ink:#e6ebf0;--mute:#9aa8b5;--line:#33414d;--accent:#6aa3d6;--green:#4fc183;--red:#ef6a5f;--orange:#eba15a}}
:root[data-theme="dark"]{--bg:#141b22;--panel:#1d2730;--ink:#e6ebf0;--mute:#9aa8b5;--line:#33414d;--accent:#6aa3d6;--green:#4fc183;--red:#ef6a5f;--orange:#eba15a}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--ink);font:400 15px/1.45 Barlow,system-ui,sans-serif}
h1,h2,.num{font-family:"Barlow Semi Condensed","Arial Narrow",sans-serif}
header{background:var(--ink);color:var(--bg);padding:18px clamp(14px,4vw,32px);border-bottom:6px solid var(--amber);display:flex;justify-content:space-between;align-items:center;gap:12px;flex-wrap:wrap}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]) header{background:#0d1217;color:#e6ebf0}}
h1{margin:0;font-size:26px;font-weight:700;letter-spacing:.01em}
header p{margin:2px 0 0;opacity:.75;font-size:13px}
main{max-width:1200px;margin:0 auto;padding:18px clamp(14px,4vw,32px) 40px}
.kpis{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:12px;margin-bottom:18px}
.kpi{background:var(--panel);border:1px solid var(--line);border-left:5px solid var(--accent);padding:12px 14px;border-radius:4px}
.kpi.warn{border-left-color:var(--orange)}.kpi.bad{border-left-color:var(--red)}.kpi.ok{border-left-color:var(--green)}
.kpi .num{font-size:28px;font-weight:700;line-height:1.1}
.kpi small{color:var(--mute);display:block}
.grid{display:grid;grid-template-columns:minmax(0,2fr) minmax(280px,1fr);gap:18px}
@media (max-width:860px){.grid{grid-template-columns:1fr}}
section{background:var(--panel);border:1px solid var(--line);border-radius:4px;padding:14px;margin-bottom:18px}
h2{margin:0 0 10px;font-size:20px;font-weight:700}
.tools{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:10px}
input,select,button{font:inherit;color:var(--ink);background:var(--bg);border:1px solid var(--line);border-radius:4px;padding:7px 9px;min-width:0}
input:focus-visible,select:focus-visible,button:focus-visible{outline:3px solid var(--amber);outline-offset:1px}
button{cursor:pointer;background:var(--accent);color:#fff;border-color:var(--accent);font-weight:500}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]) button.primary{color:#0d1217}}
button.ghost{background:transparent;color:var(--ink);border-color:var(--line)}
button.small{padding:3px 8px;font-size:13px}
.scroll{overflow-x:auto}
table{width:100%;border-collapse:collapse;font-size:14px}
th,td{text-align:left;padding:7px 8px;border-bottom:1px solid var(--line);white-space:nowrap}
th{color:var(--mute);font-weight:500;font-size:13px}
td.r,th.r{text-align:right}
.badge{display:inline-block;padding:2px 8px;border-radius:10px;font-size:12px;font-weight:500;color:#fff}
.b-ok{background:var(--green)}.b-low{background:var(--orange)}.b-crit{background:var(--red)}.b-out{background:var(--ink)}.b-over{background:var(--accent)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]) .badge{color:#0d1217}}
form{display:grid;gap:8px}
form label{display:grid;gap:3px;font-size:13px;color:var(--mute)}
.two{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.msg{min-height:20px;font-size:13px;color:var(--red)}
.bar{display:grid;grid-template-columns:90px 1fr auto;gap:8px;align-items:center;margin:6px 0;font-size:13px}
.bar i{display:block;height:14px;background:var(--accent);border-radius:2px}
.hist{list-style:none;margin:0;padding:0;font-size:13px;max-height:220px;overflow:auto}
.hist li{padding:5px 0;border-bottom:1px solid var(--line);display:flex;justify-content:space-between;gap:8px}
.in{color:var(--green)}.out{color:var(--red)}
.empty{color:var(--mute);padding:14px 0}
#rp{position:fixed;inset:0;z-index:10;overflow:auto;background:var(--bg);padding:calc(20px + env(safe-area-inset-top,0px)) clamp(14px,4vw,32px) calc(40px + env(safe-area-inset-bottom,0px))}
#rp[hidden]{display:none}
#rp h1{margin:14px 0 2px}
#rp .tools button{padding:8px 12px}
@media print{header,main{display:none!important}.noprint{display:none!important}body{background:#fff}#rp{position:static;overflow:visible;--bg:#fff;--panel:#fff;--ink:#000;--mute:#444;--line:#999;color:#000;padding:0}#rp .badge{color:#000;background:#fff!important;border:1px solid #000}section{break-inside:avoid}}
</style>
</head>
<body>
<header>
  <div><h1>StockClair</h1><p>Suivi et gestion de stock · indicateurs, alertes et rapport du jour</p></div>
  <div style="display:flex;gap:8px;flex-wrap:wrap"><button class="small" id="rep" style="background:var(--amber);color:#1b2733;border-color:var(--amber)">Rapport du jour</button><button class="ghost small" id="csv" style="color:inherit;border-color:currentColor">Exporter Excel (CSV)</button><button class="ghost small" id="reset" style="color:inherit;border-color:currentColor">Recharger les données d'exemple</button></div>
</header>
<main>
  <div class="kpis" id="kpis"></div>
  <div class="grid">
    <div>
      <section>
        <h2>Articles en stock</h2>
        <div class="tools">
          <input id="q" type="search" placeholder="Rechercher un article" aria-label="Rechercher">
          <select id="fcat" aria-label="Catégorie"></select>
          <select id="fst" aria-label="État">
            <option value="">Tous les états</option><option value="ok">OK</option><option value="low">À commander</option><option value="crit">Sous sécurité</option><option value="out">Rupture</option><option value="over">Surstock</option><option value="dorm">Dormant</option>
          </select>
        </div>
        <div class="scroll"><table>
          <thead><tr><th>Réf.</th><th>Désignation</th><th>Catégorie</th><th class="r">Stock</th><th class="r">Initial</th><th class="r">Sécurité</th><th class="r">Min</th><th class="r">Alerte</th><th class="r">Max</th><th class="r">Valeur (MAD)</th><th>État</th><th></th></tr></thead>
          <tbody id="rows"></tbody>
        </table></div>
        <div id="none" class="empty" hidden>Aucun article ne correspond. Modifie la recherche ou ajoute un article.</div>
      </section>
      <section>
        <h2>Alertes à traiter</h2>
        <div class="empty" style="padding:0 0 8px;font-size:13px">Stock min = conso/jour × délai · Stock d'alerte = min + sécurité · Quantité à commander = max − sécurité</div>
        <div id="alerts" class="scroll"></div>
      </section>
    </div>
    <div>
      <section>
        <h2>Enregistrer un mouvement</h2>
        <form id="mv">
          <label>Article<select id="mref"></select></label>
          <div class="two">
            <label>Type<select id="mtype"><option value="in">Entrée</option><option value="out">Sortie</option></select></label>
            <label>Quantité<input id="mqty" type="number" min="1" value="1" required></label>
          </div>
          <button class="primary" type="submit">Enregistrer le mouvement</button>
          <div class="msg" id="mmsg" role="alert"></div>
        </form>
      </section>
      <section>
        <h2>Ajouter un article</h2>
        <form id="add">
          <div class="two">
            <label>Référence<input id="aref" required></label>
            <label>Catégorie<input id="acat" required list="cats"></label>
          </div>
          <datalist id="cats"></datalist>
          <label>Désignation<input id="aname" required></label>
          <div class="two">
            <label>Stock initial<input id="aqty" type="number" min="0" value="0" required></label>
            <label>Stock maximum<input id="amax" type="number" min="1" value="100" required></label></div><div class="two"><label>Stock de sécurité<input id="asecu" type="number" min="0" value="5" required></label><label>Conso. par jour<input id="aconso" type="number" min="0" step="0.01" value="1" required></label>
          </div>
          <label>Délai de réappro. (jours)<input id="adelai" type="number" min="1" value="7" required></label>
          <label>Coût unitaire (MAD)<input id="acost" type="number" min="0" step="0.01" value="0" required></label>
          <button class="primary" type="submit">Ajouter l'article</button>
        </form>
      </section>
      <section>
        <h2>Valeur par catégorie</h2>
        <div id="chart"></div>
      </section>
      <section>
        <h2>Derniers mouvements</h2>
        <ul class="hist" id="hist"></ul>
      </section>
    </div>
  </div>
</main>
<div id="rp" hidden></div>
<script>
(function(){
var KEY="gestion-stock-v1",DORM=60,items=[],moves=[],EX={"RT-101":{init:60,max:120,secu:10,conso:2,delai:6},"RT-205":{init:40,max:80,secu:8,conso:1.5,delai:8},"FI-310":{init:30,max:60,secu:6,conso:1,delai:7},"FI-322":{init:35,max:60,secu:8,conso:1,delai:7},"EL-410":{init:20,max:40,secu:4,conso:0.5,delai:10},"EL-455":{init:400,max:500,secu:60,conso:8,delai:10},"LB-520":{init:20,max:30,secu:4,conso:0.3,delai:14},"OU-610":{init:5,max:6,secu:1,conso:0.1,delai:15}};
function day(n){var d=new Date();d.setDate(d.getDate()-n);return d.toISOString().slice(0,10)}
function seed(){
  items=[
    {ref:"RT-101",name:"Roulement 6204",cat:"Mécanique",qty:42,min:15,cost:38},
    {ref:"RT-205",name:"Courroie trapézoïdale A42",cat:"Mécanique",qty:6,min:10,cost:65},
    {ref:"FI-310",name:"Filtre à huile",cat:"Filtration",qty:0,min:8,cost:54},
    {ref:"FI-322",name:"Filtre à air",cat:"Filtration",qty:25,min:10,cost:92},
    {ref:"EL-410",name:"Contacteur 25A",cat:"Électrique",qty:12,min:6,cost:140},
    {ref:"EL-455",name:"Câble 3x2,5 mm² (m)",cat:"Électrique",qty:180,min:100,cost:12},
    {ref:"LB-520",name:"Graisse industrielle 1 kg",cat:"Lubrifiants",qty:9,min:8,cost:76},
    {ref:"OU-610",name:"Clé dynamométrique",cat:"Outillage",qty:3,min:2,cost:480}];
  moves=[];
  var h=[["RT-101","out",20,10],["RT-101","in",30,25],["RT-205","out",9,6],["FI-310","out",8,3],["FI-322","out",5,12],["EL-410","out",4,20],["EL-455","out",120,15],["LB-520","out",6,8],["RT-205","in",5,40],["FI-322","in",20,28]];
  h.forEach(function(x){moves.push({date:day(x[3]),ref:x[0],type:x[1],qty:x[2]})});
  items.forEach(function(it){var m=moves.filter(function(v){return v.ref===it.ref}).map(function(v){return v.date}).sort().pop();it.last=m||day(90)});
  var o=items.find(function(i){return i.ref==="OU-610"});o.last=day(120);o.qty=8;mig();
  save();
}
function save(){try{localStorage.setItem(KEY,JSON.stringify({items:items,moves:moves}))}catch(e){}}
function load(){try{var d=JSON.parse(localStorage.getItem(KEY));if(d&&d.items){items=d.items;moves=d.moves||[];mig();return true}}catch(e){}return false}
function $(id){return document.getElementById(id)}
function esc(s){return String(s).replace(/[&<>"']/g,function(c){return {"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]})}
function fmt(n){return Math.round(n).toLocaleString("fr-FR")}
function age(it){return Math.floor((Date.now()-new Date(it.last).getTime())/864e5)}
function mig(){items.forEach(function(it){if(it.conso==null){var x=EX[it.ref];if(x){Object.assign(it,x)}else{var m=it.min||0;it.delai=7;it.conso=+(m*0.6/7).toFixed(2);it.secu=Math.round(m*0.4);it.max=Math.max(m*4,it.qty,1);it.init=it.qty}}})}
function minS(it){return Math.ceil(it.conso*it.delai)}
function alt(it){return minS(it)+it.secu}
function state(it){return it.qty<=0?"out":it.qty<=it.secu?"crit":it.qty<=alt(it)?"low":it.qty>it.max?"over":"ok"}
var LBL={ok:"OK",low:"À commander",crit:"Sous sécurité",out:"Rupture",over:"Surstock"};
function filtered(){
  var q=$("q").value.toLowerCase(),c=$("fcat").value,s=$("fst").value;
  return items.filter(function(it){
    if(q&&(it.name+it.ref).toLowerCase().indexOf(q)<0)return false;
    if(c&&it.cat!==c)return false;
    if(s==="dorm")return age(it)>DORM;
    if(s&&state(it)!==s)return false;return true});
}
function kpis(){
  var val=0,out=0,low=0,over=0,dorm=0,sold=0,since=day(30),sold30=0;
  items.forEach(function(it){val+=it.qty*it.cost;var s=state(it);if(s==="out")out++;if(s==="low"||s==="crit")low++;if(s==="over")over++;if(age(it)>DORM)dorm++});
  var cost={};items.forEach(function(it){cost[it.ref]=it.cost});
  moves.forEach(function(m){if(m.type==="out"){var v=m.qty*(cost[m.ref]||0);sold+=v;if(m.date>=since)sold30+=v}});
  var cover=sold30>0?val/(sold30/30):null,rot=val>0?sold/val:0,n=items.length||1;
  var k=[
    ["Valeur du stock",fmt(val)+" MAD","","Quantité × coût unitaire"],
    ["Articles",items.length,"","références suivies"],
    ["Taux de rupture",(out/n*100).toFixed(0)+" %",out?"bad":"ok",out+" article(s) à zéro"],
    ["Sous stock d'alerte",low,low?"warn":"ok","articles à commander"],["Surstock",over,over?"warn":"ok","au-dessus du stock max"],
    ["Couverture",cover===null?"—":Math.round(cover)+" j",cover!==null&&cover<30?"warn":"","au rythme des 30 derniers jours"],
    ["Rotation",rot.toFixed(2),"","sorties / valeur du stock"],
    ["Stock dormant",dorm,dorm?"warn":"ok","sans mouvement depuis "+DORM+" j"]];
  $("kpis").innerHTML=k.map(function(x){return '<div class="kpi '+x[2]+'"><small>'+x[0]+'</small><div class="num">'+x[1]+'</div><small>'+x[3]+'</small></div>'}).join("");
}
function rows(){
  var list=filtered();$("none").hidden=list.length>0;
  $("rows").innerHTML=list.map(function(it){var s=state(it);
    return '<tr><td>'+esc(it.ref)+'</td><td>'+esc(it.name)+'</td><td>'+esc(it.cat)+'</td><td class="r">'+it.qty+'</td><td class="r">'+it.init+'</td><td class="r">'+it.secu+'</td><td class="r">'+minS(it)+'</td><td class="r">'+alt(it)+'</td><td class="r">'+it.max+'</td><td class="r">'+fmt(it.qty*it.cost)+'</td><td><span class="badge b-'+s+'">'+LBL[s]+'</span></td><td><button class="ghost small" data-del="'+esc(it.ref)+'" aria-label="Supprimer '+esc(it.name)+'">Supprimer</button></td></tr>'}).join("");
}
function alerts(){
  var a=items.filter(function(it){return ["out","crit","low"].indexOf(state(it))>=0}).sort(function(x,y){return x.qty-y.qty});
  if(!a.length){$("alerts").innerHTML='<div class="empty">Aucune alerte : tous les articles sont au-dessus du seuil.</div>';return}
  $("alerts").innerHTML='<table><thead><tr><th>Article</th><th class="r">Qté</th><th class="r">À commander</th></tr></thead><tbody>'+a.map(function(it){
    return '<tr><td>'+esc(it.ref)+' · '+esc(it.name)+'</td><td class="r">'+it.qty+'</td><td class="r">'+Math.max(it.max-it.secu,1)+'</td></tr>'}).join("")+'</tbody></table>';
}
function side(){
  var cats=[],tot={};items.forEach(function(it){if(cats.indexOf(it.cat)<0)cats.push(it.cat);tot[it.cat]=(tot[it.cat]||0)+it.qty*it.cost});
  var cur=$("fcat").value;
  $("fcat").innerHTML='<option value="">Toutes les catégories</option>'+cats.map(function(c){return '<option'+(c===cur?' selected':'')+'>'+esc(c)+'</option>'}).join("");
  $("cats").innerHTML=cats.map(function(c){return '<option value="'+esc(c)+'">'}).join("");
  var mr=$("mref").value;
  $("mref").innerHTML=items.map(function(it){return '<option value="'+esc(it.ref)+'"'+(it.ref===mr?' selected':'')+'>'+esc(it.ref)+' · '+esc(it.name)+'</option>'}).join("");
  var mx=Math.max.apply(null,cats.map(function(c){return tot[c]}).concat([1]));
  $("chart").innerHTML=cats.length?cats.map(function(c){return '<div class="bar"><span>'+esc(c)+'</span><i style="width:'+Math.max(tot[c]/mx*100,2)+'%"></i><span>'+fmt(tot[c])+'</span></div>'}).join(""):'<div class="empty">Ajoute un article pour voir le graphique.</div>';
  var h=moves.slice().reverse().slice(0,12);
  $("hist").innerHTML=h.length?h.map(function(m){return '<li><span>'+m.date+' · '+esc(m.ref)+'</span><span class="'+m.type+'">'+(m.type==="in"?"+":"−")+m.qty+'</span></li>'}).join(""):'<li class="empty">Aucun mouvement enregistré.</li>';
}
function render(){kpis();rows();alerts();side()}
$("mv").addEventListener("submit",function(e){
  e.preventDefault();var it=items.find(function(i){return i.ref===$("mref").value}),q=parseInt($("mqty").value,10),t=$("mtype").value;
  if(!it){$("mmsg").textContent="Ajoute d'abord un article.";return}
  if(!(q>0)){$("mmsg").textContent="Saisis une quantité supérieure à 0.";return}
  if(t==="out"&&q>it.qty){$("mmsg").textContent="Sortie impossible : il reste seulement "+it.qty+" en stock.";return}
  it.qty+=t==="in"?q:-q;it.last=day(0);moves.push({date:day(0),ref:it.ref,type:t,qty:q});
  $("mmsg").textContent="";save();render();
});
$("add").addEventListener("submit",function(e){
  e.preventDefault();var ref=$("aref").value.trim();
  if(items.some(function(i){return i.ref.toLowerCase()===ref.toLowerCase()})){alert("Cette référence existe déjà.");return}
  items.push({ref:ref,name:$("aname").value.trim(),cat:$("acat").value.trim(),qty:+$("aqty").value,init:+$("aqty").value,max:+$("amax").value,secu:+$("asecu").value,conso:+$("aconso").value,delai:+$("adelai").value,cost:+$("acost").value,last:day(0)});
  $("add").reset();save();render();
});
$("rows").addEventListener("click",function(e){
  var r=e.target.getAttribute("data-del");if(!r)return;
  if(confirm("Supprimer l'article "+r+" ?")){items=items.filter(function(i){return i.ref!==r});moves=moves.filter(function(m){return m.ref!==r});save();render()}
});
["q","fcat","fst"].forEach(function(id){$(id).addEventListener("input",rows)});
$("reset").addEventListener("click",function(){if(confirm("Remplacer toutes les données par l'exemple ?")){seed();render()}});
function cc(v){v=String(v);return /[;"\n]/.test(v)?'"'+v.replace(/"/g,'""')+'"':v}
async function saveFile(name,data){try{var d=window.claude&&await window.claude.use("downloads");if(!d){alert("L'enregistrement de fichier n'est pas disponible ici.");return}await d.save({filename:name,data:data})}catch(e){if(!e||e.code!=="declined")alert("Enregistrement impossible. Réessaie dans un instant.")}}
function exportCsv(){
  var h=["Date","Référence","Désignation","Catégorie","Stock","Stock initial","Stock sécurité","Stock min","Stock alerte","Stock max","Coût unitaire","Valeur","État","Qté à commander"];
  var L=[h.join(";")];
  items.forEach(function(it){var s=state(it);L.push([day(0),it.ref,it.name,it.cat,it.qty,it.init,it.secu,minS(it),alt(it),it.max,it.cost,it.qty*it.cost,LBL[s],(s==="out"||s==="crit"||s==="low")?Math.max(it.max-it.secu,1):0].map(cc).join(";"))});
  saveFile("rapport-stock-"+day(0)+".csv","\ufeff"+L.join("\r\n"));
}
function report(){
  var t=day(0),nm={};items.forEach(function(it){nm[it.ref]=it.name});
  var mv=moves.filter(function(m){return m.date===t});
  var mvh=mv.length?'<table><thead><tr><th>Article</th><th>Type</th><th class="r">Qté</th></tr></thead><tbody>'+mv.map(function(m){return '<tr><td>'+esc(m.ref)+' · '+esc(nm[m.ref]||"")+'</td><td>'+(m.type==="in"?"Entrée":"Sortie")+'</td><td class="r">'+m.qty+'</td></tr>'}).join("")+'</tbody></table>':'<div class="empty">Aucun mouvement enregistré aujourd\'hui.</div>';
  var all=items.map(function(it){var s=state(it);return '<tr><td>'+esc(it.ref)+'</td><td>'+esc(it.name)+'</td><td class="r">'+it.qty+'</td><td class="r">'+minS(it)+'</td><td class="r">'+alt(it)+'</td><td class="r">'+it.max+'</td><td class="r">'+fmt(it.qty*it.cost)+'</td><td><span class="badge b-'+s+'">'+LBL[s]+'</span></td></tr>'}).join("");
  var dt=new Date().toLocaleDateString("fr-FR",{weekday:"long",day:"numeric",month:"long",year:"numeric"});
  var r=$("rp");
  r.innerHTML='<div class="noprint tools"><button id="rpP">Imprimer / enregistrer en PDF</button><button id="rpC">Exporter en Excel (CSV)</button><button class="ghost" id="rpX">Fermer</button></div><h1>StockClair · Rapport du jour</h1><p>'+dt+'</p><section><h2>Indicateurs</h2><div class="kpis">'+$("kpis").innerHTML+'</div></section><section><h2>Alertes à traiter</h2>'+$("alerts").innerHTML+'</section><section><h2>Mouvements du jour</h2>'+mvh+'</section><section><h2>État complet du stock</h2><div class="scroll"><table><thead><tr><th>Réf.</th><th>Désignation</th><th class="r">Stock</th><th class="r">Min</th><th class="r">Alerte</th><th class="r">Max</th><th class="r">Valeur (MAD)</th><th>État</th></tr></thead><tbody>'+all+'</tbody></table></div></section>';
  r.hidden=false;r.scrollTop=0;
  $("rpP").onclick=function(){try{window.print()}catch(e){alert("Utilise la fonction Imprimer de ton navigateur.")}};
  $("rpC").onclick=exportCsv;
  $("rpX").onclick=function(){r.hidden=true};
}
$("rep").addEventListener("click",report);
$("csv").addEventListener("click",exportCsv);
if(!load())seed();
render();
})();
</script>
</body>
</html>
