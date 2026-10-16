<!DOCTYPE html>
<html lang="kk">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Материалдар базасы</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<style>
:root{
  --bg:#eef2f6; --surface:#ffffff; --ink:#14213d; --muted:#5b6679; --line:#d5dce6;
  --brand:#14213d; --brand-ink:#f4f7fb; --accent:#e8a33d; --link:#2563b0; --ok:#2f8f5b; --warn:#b4531a;
  box-sizing:border-box;
  padding-top:env(safe-area-inset-top,0px); padding-bottom:env(safe-area-inset-bottom,0px);
}
@media (prefers-color-scheme: dark){
  :root:not([data-theme="light"]){
    --bg:#0e1626; --surface:#17223a; --ink:#e8edf6; --muted:#9aa7bd; --line:#2a3858;
    --brand:#0a1120; --brand-ink:#e8edf6; --link:#7db4f0; --ok:#5ec48b; --warn:#f0a070;
  }
}
:root[data-theme="dark"]{
  --bg:#0e1626; --surface:#17223a; --ink:#e8edf6; --muted:#9aa7bd; --line:#2a3858;
  --brand:#0a1120; --brand-ink:#e8edf6; --link:#7db4f0; --ok:#5ec48b; --warn:#f0a070;
}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--ink);font-family:"Segoe UI",Roboto,"Helvetica Neue",Arial,sans-serif;line-height:1.5;-webkit-text-size-adjust:100%}
button,input,select{font:inherit;color:inherit}
:focus-visible{outline:3px solid var(--accent);outline-offset:2px}
header{background:var(--brand);color:var(--brand-ink)}
.bar{max-width:1080px;margin:0 auto;padding:16px 20px;display:flex;align-items:center;gap:16px;flex-wrap:wrap}
.logo{font-weight:700;font-size:1.2rem;margin-right:auto}
.sub{opacity:.8;font-size:.95rem}
header nav{display:flex;gap:4px;flex-wrap:wrap}
header nav button{background:none;border:0;color:inherit;opacity:.8;padding:8px 14px;border-radius:8px;cursor:pointer}
header nav button:hover{opacity:1;background:rgba(255,255,255,.08)}
header nav button[aria-current="page"]{opacity:1;background:rgba(255,255,255,.16);font-weight:600}
main{max-width:1080px;margin:0 auto;padding:32px 20px 64px}
h1{font-size:clamp(1.8rem,4.5vw,2.8rem);line-height:1.12;margin:0 0 10px;letter-spacing:-.01em}
h2{font-size:1.3rem;margin:0 0 12px}
p{margin:0 0 12px}
.muted{color:var(--muted)}
.top{display:grid;grid-template-columns:1fr 250px;gap:28px;align-items:start;margin-bottom:28px}
.card{background:var(--surface);border:1px solid var(--line);border-radius:16px;padding:20px}
.qrcard{text-align:center}
.qrbox{background:#fff;padding:10px;border-radius:12px;width:196px;height:196px;margin:10px auto;display:grid;place-items:center}
.qrbox img,.qrbox canvas{max-width:100%;height:auto;display:block}
.btn{border:0;border-radius:10px;padding:10px 16px;cursor:pointer;font-weight:600;text-decoration:none;display:inline-block;text-align:center}
.btn.primary{background:var(--brand);color:var(--brand-ink)}
.btn.ghost{background:transparent;border:1.5px solid var(--line)}
.btn:hover{filter:brightness(1.1)}
.btn:disabled{opacity:.55;cursor:not-allowed}
.sec{font-size:.88rem;color:var(--muted)}
.grid2{display:grid;grid-template-columns:repeat(auto-fit,minmax(170px,1fr));gap:10px;margin:12px 0}
.grid2 input,.grid2 select,.toolbar input,.toolbar select{background:var(--bg);border:1px solid var(--line);border-radius:10px;padding:10px 12px;min-width:0;width:100%}
.toolbar{display:flex;gap:10px;flex-wrap:wrap;margin:22px 0 16px}
.toolbar input{flex:1 1 220px;width:auto}
.toolbar select{width:auto;flex:0 1 auto}
.list{display:grid;grid-template-columns:repeat(auto-fill,minmax(250px,1fr));gap:14px}
.item{background:var(--surface);border:1px solid var(--line);border-radius:14px;padding:18px;display:flex;flex-direction:column;gap:8px}
.item h3{margin:0;font-size:1.05rem;word-break:break-word}
.item .acts{display:flex;gap:8px;flex-wrap:wrap;margin-top:4px}
.tag{display:inline-block;align-self:flex-start;font-size:.8rem;padding:2px 10px;border-radius:99px;border:1px solid var(--line);color:var(--muted)}
.tag.t-жоспар{border-color:var(--link);color:var(--link)}
.tag.t-презентация{border-color:var(--accent);color:var(--warn)}
.tag.t-тапсырма{border-color:var(--ok);color:var(--ok)}
.empty{padding:36px 20px;text-align:center}
.viewer{position:fixed;inset:0;background:rgba(8,14,26,.72);z-index:50;display:flex;align-items:center;justify-content:center;padding:max(16px,env(safe-area-inset-top,0px)) 16px max(16px,env(safe-area-inset-bottom,0px))}
.vbox{background:var(--surface);border-radius:16px;width:min(1000px,100%);height:min(86vh,100%);display:flex;flex-direction:column;overflow:hidden;border:1px solid var(--line)}
.vhead{display:flex;gap:10px;align-items:center;padding:12px 16px;border-bottom:1px solid var(--line)}
.vhead b{margin-right:auto;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.vbody{flex:1;overflow:auto;display:flex;align-items:center;justify-content:center;background:var(--bg)}
.vbody iframe{width:100%;height:100%;border:0;background:#fff}
.vbody img,.vbody video{max-width:100%;max-height:100%}
.vbody pre{margin:0;padding:16px;width:100%;height:100%;overflow:auto;white-space:pre-wrap;word-break:break-word;align-self:flex-start}
.hidden{display:none!important}
.toast{position:fixed;left:50%;bottom:calc(24px + env(safe-area-inset-bottom,0px));transform:translateX(-50%);background:var(--brand);color:var(--brand-ink);padding:12px 20px;border-radius:12px;opacity:0;pointer-events:none;transition:opacity .25s;max-width:90vw;z-index:60}
.toast.show{opacity:1}
@media (max-width:820px){.top{grid-template-columns:1fr}}
@media (prefers-reduced-motion:reduce){*{transition:none!important}}
</style>
</head>
<body>
<header>
  <div class="bar">
    <div class="logo">Материалдар базасы</div>
    <nav id="nav" aria-label="Бөлімдер"><button data-go="home">Басты бет</button><button data-go="materials">Материалдар</button><button data-go="tasks">Тапсырмалар</button></nav>
  </div>
</header>

<main>
  <div id="view-home">
  <section class="top">
    <div>
      <h1>Барлық материал бір жерде</h1>
      <p class="muted" style="font-size:1.1rem">Жоспарларды, презентацияларды және тапсырмаларды жүктеп, пән мен сынып бойынша тауып, тікелей сайттан ашыңыз.</p>
      <p class="sec" id="countLine"></p>
    </div>
    <div class="card qrcard">
      <h2 style="font-size:1.05rem;margin-bottom:2px">Телефонда ашу</h2>
      <p class="sec" style="margin:0">Камераны кодқа бағыттаңыз</p>
      <div class="qrbox" id="qr" role="img" aria-label="Сайтты телефонда ашуға арналған QR код"></div>
    </div>
  </section>
  <div class="list" style="grid-template-columns:repeat(auto-fit,minmax(280px,1fr))">
    <div class="item"><h3>Материалдар</h3><p class="muted" style="margin:0">Сабақ жоспарлары мен презентациялар</p><p class="sec" id="cntMat" style="margin:0"></p><div class="acts"><button class="btn primary" data-go="materials">Ашу</button></div></div>
    <div class="item"><h3>Тапсырмалар</h3><p class="muted" style="margin:0">Оқушыларға арналған тапсырмалар</p><p class="sec" id="cntTask" style="margin:0"></p><div class="acts"><button class="btn primary" data-go="tasks">Ашу</button></div></div>
  </div>
  </div>

  <div id="view-list" class="hidden">
  <h1 id="secTitle" style="font-size:clamp(1.6rem,4vw,2.2rem)"></h1>
  <p class="muted" id="secDesc"></p>
  <div class="card" id="addBox">
    <h2 id="addTitle">Файл жүктеу</h2>
    <p class="sec" id="addHelp" style="margin:0">Қабылданатын файлдар: PDF, сурет (PNG, JPG, WEBP, GIF), бейне (MP4, WEBM), TXT, CSV, MD, JSON. Көлемі 20 МБ-қа дейін. Word немесе PowerPoint файлын алдымен PDF етіп сақтаңыз.</p>
    <div class="grid2">
      <input id="aTitle" placeholder="Материал атауы" aria-label="Материал атауы">
      <select id="aSubj" aria-label="Пән"><option>Информатика</option><option>Математика</option><option>Қазақ тілі</option><option>Жаратылыстану</option><option>Дүниетану</option><option>Басқа</option></select>
      <select id="aGrade" aria-label="Сынып"><option>1</option><option>2</option><option>3</option><option>4</option><option>5</option><option>6</option><option>7</option><option>8</option><option>9</option><option>10</option><option>11</option></select>
      <select id="aType" aria-label="Түрі"><option>жоспар</option><option>презентация</option><option>тапсырма</option></select>
      <input id="aFile" type="file" accept=".pdf,.png,.jpg,.jpeg,.webp,.gif,.mp4,.webm,.txt,.csv,.md,.json" aria-label="Файл">
      <input id="aUrl" type="url" placeholder="Немесе сілтеме (Google Drive т.б.)" aria-label="Сілтеме">
    </div>
    <button class="btn primary" id="addBtn">Жүктеу</button>
    <p class="sec" id="addNote" style="margin:12px 0 0"></p>
  </div>

  <div class="toolbar">
    <input id="q" type="search" placeholder="Атауы бойынша іздеу" aria-label="Іздеу">
    <select id="fSubj" aria-label="Пән"><option value="">Барлық пән</option><option>Информатика</option><option>Математика</option><option>Қазақ тілі</option><option>Жаратылыстану</option><option>Дүниетану</option><option>Басқа</option></select>
    <select id="fGrade" aria-label="Сынып"><option value="">Барлық сынып</option><option>1</option><option>2</option><option>3</option><option>4</option><option>5</option><option>6</option><option>7</option><option>8</option><option>9</option><option>10</option><option>11</option></select>
    <select id="fType" aria-label="Түрі"><option value="">Барлық түрі</option><option>жоспар</option><option>презентация</option><option>тапсырма</option></select>
  </div>
  <div class="list" id="list"></div>
  <div class="empty muted hidden" id="none"></div>
  </div>
</main>

<div class="viewer hidden" id="viewer" role="dialog" aria-modal="true" aria-label="Файлды көру">
  <div class="vbox">
    <div class="vhead"><b id="vtitle"></b><a class="btn ghost" id="vlink" target="_blank" rel="noopener">Жаңа бетте ашу</a><button class="btn primary" id="vclose">Жабу</button></div>
    <div class="vbody" id="vbody"></div>
  </div>
</div>
<div class="toast" id="toast" role="status"></div>

<script>
(function(){
  var SAMPLES=[];
  var view="home", shared=[], local=[], st={db:null,assets:null}, idb=null, memLocal=[], memId=1, objUrl=null;
  var $=function(id){return document.getElementById(id)};
  function toast(m){var t=$("toast");t.textContent=m;t.classList.add("show");clearTimeout(toast.i);toast.i=setTimeout(function(){t.classList.remove("show")},2800)}

  try{new QRCode($("qr"),{text:location.href.split("#")[0],width:176,height:176,colorDark:"#14213d",colorLight:"#ffffff",correctLevel:QRCode.CorrectLevel.M})}
  catch(e){$("qr").textContent="QR жүктелмеді"}

  // ---- осы құрылғыдағы сақтау (IndexedDB)
  function idbOpen(){return new Promise(function(res){try{var rq=indexedDB.open("mb_files",1);rq.onupgradeneeded=function(){rq.result.createObjectStore("files",{keyPath:"id",autoIncrement:true})};rq.onsuccess=function(){res(rq.result)};rq.onerror=function(){res(null)}}catch(e){res(null)}})}
  function idbAll(){return new Promise(function(res){if(!idb){res(memLocal.slice());return}try{var rq=idb.transaction("files").objectStore("files").getAll();rq.onsuccess=function(){res(rq.result||[])};rq.onerror=function(){res([])}}catch(e){res([])}})}
  function idbAdd(rec){return new Promise(function(res,rej){if(!idb){rec.id=memId++;memLocal.push(rec);res();return}try{var tx=idb.transaction("files","readwrite");tx.objectStore("files").add(rec);tx.oncomplete=function(){res()};tx.onerror=function(){rej(tx.error)}}catch(e){rej(e)}})}
  function idbDel(id){return new Promise(function(res,rej){if(!idb){memLocal=memLocal.filter(function(x){return x.id!==id});res();return}try{var tx=idb.transaction("files","readwrite");tx.objectStore("files").delete(id);tx.oncomplete=function(){res()};tx.onerror=function(){rej(tx.error)}}catch(e){rej(e)}})}
  async function loadLocal(){
    var a=await idbAll();
    local=a.map(function(x){return{src:(x.url&&!x.blob)?"locallink":"local",id:x.id,blob:x.blob,url:x.url,t:x.title,s:x.subject,g:x.grade,ty:x.type,fn:x.fileName,at:x.createdAt}}).sort(function(x,y){return (y.at||0)-(x.at||0)});
    render();
  }
  function isShared(){return !!(st.assets&&st.db)}

  function kind(m){
    var e=(m.fn||"").split(".").pop().toLowerCase();
    if(e==="pdf")return"pdf";
    if(["png","jpg","jpeg","webp","gif"].indexOf(e)>=0)return"img";
    if(["mp4","webm"].indexOf(e)>=0)return"video";
    return"text";
  }
  function closeViewer(){$("viewer").classList.add("hidden");$("vbody").innerHTML="";if(objUrl){URL.revokeObjectURL(objUrl);objUrl=null}}
  function openFile(m){
    var body=$("vbody"),k=kind(m),url;
    closeViewer();
    if(m.src==="shared")url="/_blob/"+m.aid;else{objUrl=URL.createObjectURL(m.blob);url=objUrl}
    $("vtitle").textContent=m.t+(m.fn?" · "+m.fn:"");$("vlink").href=url;
    if(k==="pdf"){var f=document.createElement("iframe");f.src=url;f.title=m.t;body.appendChild(f)}
    else if(k==="img"){var i=document.createElement("img");i.src=url;i.alt=m.t;body.appendChild(i)}
    else if(k==="video"){var v=document.createElement("video");v.src=url;v.controls=true;body.appendChild(v)}
    else{var pr=document.createElement("pre");pr.textContent="Жүктелуде...";body.appendChild(pr);
      var get=m.src==="local"?m.blob.text():fetch(url).then(function(r){return r.text()});
      Promise.resolve(get).then(function(t){pr.textContent=t}).catch(function(){pr.textContent="Файлды ашу мүмкін болмады. «Жаңа бетте ашу» батырмасын басыңыз."})}
    $("viewer").classList.remove("hidden");$("vclose").focus();
  }
  async function removeRow(m,btn){
    try{
      if(m.src==="link"){await st.db.collection("materials").doc(m.did).delete()}
      else if(m.src==="shared"){await st.assets.delete(m.aid);await st.db.collection("materials").doc(m.did).delete()}
      else{await idbDel(m.id);await loadLocal()}
      toast("Өшірілді");
    }catch(e){
      toast(e&&e.code==="not_uploader"?"Бұл файлды басқа адам жүктеген, өшіру мүмкін емес":"Өшіру мүмкін болмады. Қайта көріңіз");
      if(btn){btn.disabled=false;btn.textContent="Өшіру";btn.style.borderColor="";btn.style.color=""}
    }
  }
  function mkDel(m,acts){var x=document.createElement("button");x.className="btn ghost";x.textContent="Өшіру";var armed=false,tm=null;x.onclick=function(){if(!armed){armed=true;x.textContent="Растау: өшіру";x.style.borderColor="var(--warn)";x.style.color="var(--warn)";tm=setTimeout(function(){armed=false;x.textContent="Өшіру";x.style.borderColor="";x.style.color=""},4000);return}clearTimeout(tm);x.disabled=true;x.textContent="Өшірілуде...";removeRow(m,x)};acts.appendChild(x)}
  function render(){
    var q=$("q").value.trim().toLowerCase(),g=$("fGrade").value,sj=$("fSubj").value,ty=$("fType").value,box=$("list");box.innerHTML="";var n=0;
    var all=shared.concat(local);var nT=all.filter(function(m){return m.ty==="тапсырма"}).length;
    $("cntMat").textContent=(all.length-nT)+" файл";$("cntTask").textContent=nT+" файл";
    var rows=all.filter(function(m){return view==="tasks"?m.ty==="тапсырма":m.ty!=="тапсырма"});
    rows.forEach(function(m){
      if(q&&String(m.t).toLowerCase().indexOf(q)<0)return;if(sj&&m.s!==sj)return;if(g&&String(m.g)!==g)return;if(ty&&m.ty!==ty)return;n++;
      var d=document.createElement("div");d.className="item";
      var h=document.createElement("h3");h.textContent=m.t;
      var s=document.createElement("span");s.className="tag t-"+m.ty;s.textContent=m.ty;
      var p=document.createElement("p");p.className="muted";p.style.margin="0";p.textContent=m.s+(m.g?" · "+m.g+"-сынып":"");
      d.appendChild(h);d.appendChild(s);d.appendChild(p);
      var note=m.src==="sample"?"Үлгі карточка":(m.src==="link"||m.src==="locallink")?"Сыртқы сілтеме":m.src==="local"?"Осы құрылғыда сақталған":"";
      if(m.fn||note){var f=document.createElement("p");f.className="sec";f.style.margin="0";f.textContent=(m.fn?m.fn:"")+(m.fn&&note?" · ":"")+note;d.appendChild(f)}
      var acts=document.createElement("div");acts.className="acts";
      if(m.src==="sample"){
        var b=document.createElement("button");b.className="btn ghost";b.textContent="Ашу";b.onclick=function(){toast("Бұл үлгі карточка. Өз файлыңызды жүктегенде осы жерден ашылады")};acts.appendChild(b);
      }else if(m.src==="link"||m.src==="locallink"){
        var k=document.createElement("a");k.className="btn primary";k.textContent="Ашу";k.href=m.url;k.target="_blank";k.rel="noopener noreferrer";acts.appendChild(k);
        if(m.src==="locallink"||st.db)mkDel(m,acts);
      }else{
        if(m.url){var a=document.createElement("a");a.className="btn primary";a.textContent="Ашу";a.href=m.url;a.target="_blank";a.rel="noopener noreferrer";acts.appendChild(a)}
        else{var a2=document.createElement("button");a2.className="btn primary";a2.textContent="Ашу";a2.onclick=function(){openFile(m)};acts.appendChild(a2)}
        if(m.src==="local"||isShared()){
          var x=document.createElement("button");x.className="btn ghost";x.textContent="Өшіру";var armed=false,tm=null;
          x.onclick=function(){
            if(!armed){armed=true;x.textContent="Растау: өшіру";x.style.borderColor="var(--warn)";x.style.color="var(--warn)";tm=setTimeout(function(){armed=false;x.textContent="Өшіру";x.style.borderColor="";x.style.color=""},4000);return}
            clearTimeout(tm);x.disabled=true;x.textContent="Өшірілуде...";removeRow(m,x);
          };acts.appendChild(x);
        }
      }
      d.appendChild(acts);box.appendChild(d);
    });
    $("countLine").textContent="Жүктелген файл: "+(shared.length+local.length);
    $("none").textContent=view==="tasks"?"Әзірге тапсырма жоқ. Жоғарыдағы блоктан тапсырма қосыңыз.":"Ештеңе табылмады. Файл жүктеу арқылы материал қосыңыз.";
    $("none").classList.toggle("hidden",n>0);
    $("addNote").textContent=isShared()?"Файл ортақ қоймаға жүктеледі, оны барлық адам көре алады.":"Файл осы құрылғының браузерінде сақталады және басқа құрылғыда көрінбейді.";
  }
  async function addMaterial(){
    var f=$("aFile").files[0],t=$("aTitle").value.trim(),u=$("aUrl").value.trim();
    if(!t||(!f&&!u)){toast(view==="tasks"?"Атауын жазып, сілтеме енгізіңіз":"Атауын жазып, файл таңдаңыз немесе сілтеме енгізіңіз");return}
    if(!f){
      if(!/^https?:\/\//i.test(u)){toast("Сілтеме https:// деп басталуы керек");return}
      var mt={title:t,subject:$("aSubj").value,grade:Number($("aGrade").value),type:$("aType").value,url:u,createdAt:Date.now()};
      try{
        if(st.db){await st.db.collection("materials").add(mt)}else{await idbAdd(mt);await loadLocal()}
        toast("Сілтеме қосылды");
      }catch(e){
        try{await idbAdd(mt);await loadLocal();toast("Сілтеме осы құрылғыда сақталды")}catch(e2){toast("Қосу мүмкін болмады")}
      }
      $("aTitle").value="";$("aUrl").value="";return;
    }
    var ext=(f.name.split(".").pop()||"").toLowerCase();
    if(["doc","docx","ppt","pptx","xls","xlsx"].indexOf(ext)>=0){toast("Word/PowerPoint/Excel файлын PDF етіп сақтап жүктеңіз");return}
    if(["pdf","png","jpg","jpeg","webp","gif","mp4","webm","txt","csv","md","json"].indexOf(ext)<0){toast("Бұл файл түрі қабылданбайды. PDF немесе сурет жүктеңіз");return}
    if(f.size>20*1024*1024){toast("Файл тым үлкен (20 МБ-қа дейін)");return}
    var map={csv:"text/csv",md:"text/markdown",json:"application/json",txt:"text/plain"};
    var btn=$("addBtn");btn.disabled=true;btn.textContent="Жүктелуде...";
    var meta={title:t,subject:$("aSubj").value,grade:Number($("aGrade").value),type:$("aType").value,fileName:f.name,createdAt:Date.now()};
    try{
      if(isShared()){
        var r=await st.assets.upload(f,map[ext]?{type:map[ext]}:undefined);
        meta.assetId=r.id;
        await st.db.collection("materials").add(meta);
      }else{
        meta.blob=f;await idbAdd(meta);await loadLocal();
      }
      $("aTitle").value="";$("aFile").value="";toast("Файл қосылды");
    }catch(e){
      var c=e&&e.code,m="Жүктеу мүмкін болмады. Қайта көріңіз";
      if(c==="too_large")m="Файл тым үлкен (20 МБ-қа дейін)";
      else if(c==="unsupported_type")m="Бұл файл түрі қабылданбайды. PDF немесе сурет жүктеңіз";
      else if(c==="quota_or_state")m="Сақтау орны толды";
      else if(c==="rate_limited")m="Тым жиі. Біраз күтіңіз";
      toast(m);
    }
    btn.disabled=false;btn.textContent="Жүктеу";
  }

  ["q","fSubj","fGrade","fType"].forEach(function(id){$(id).addEventListener("input",render);$(id).addEventListener("change",render)});
  $("addBtn").onclick=addMaterial;$("vclose").onclick=closeViewer;
  document.addEventListener("keydown",function(e){if(e.key==="Escape")closeViewer()});
  function go(v){
    view=v;
    $("view-home").classList.toggle("hidden",v!=="home");
    $("view-list").classList.toggle("hidden",v==="home");
    document.querySelectorAll("#nav button").forEach(function(b){if(b.dataset.go===v)b.setAttribute("aria-current","page");else b.removeAttribute("aria-current")});
    if(v==="materials"){
      $("secTitle").textContent="Материалдар";$("secDesc").textContent="Сабақ жоспарлары мен презентациялар.";
      $("aType").innerHTML="<option>жоспар</option><option>презентация</option>";
      $("fType").innerHTML='<option value="">Барлық түрі</option><option>жоспар</option><option>презентация</option>';$("fType").classList.remove("hidden");
      $("addTitle").textContent="Файл жүктеу";$("addHelp").textContent="Қабылданатын файлдар: PDF, сурет (PNG, JPG, WEBP, GIF), бейне (MP4, WEBM), TXT, CSV, MD, JSON. Көлемі 20 МБ-қа дейін. Word немесе PowerPoint файлын алдымен PDF етіп сақтаңыз.";
      $("aFile").classList.remove("hidden");$("aUrl").placeholder="Немесе сілтеме (Google Drive т.б.)";$("addBtn").textContent="Жүктеу";
    }else if(v==="tasks"){
      $("secTitle").textContent="Тапсырмалар";$("secDesc").textContent="Оқушыларға арналған тапсырмалар.";
      $("aType").innerHTML="<option>тапсырма</option>";
      $("fType").innerHTML='<option value="">Барлық түрі</option>';$("fType").classList.add("hidden");
      $("addTitle").textContent="Тапсырма қосу";$("addHelp").textContent="Тапсырманың сілтемесін қойыңыз: сайт, Google Drive, Canva және т.б. Оқушы «Ашу» батырмасын басып, тапсырманы жаңа бетте ашады.";
      $("aFile").value="";$("aFile").classList.add("hidden");$("aUrl").placeholder="Тапсырма сілтемесі (https://...)";$("addBtn").textContent="Сілтеме қосу";
    }
    window.scrollTo(0,0);render();
  }
  document.querySelectorAll("[data-go]").forEach(function(b){b.addEventListener("click",function(){go(b.dataset.go)})});
  go("home");
  idbOpen().then(function(db){idb=db;return loadLocal()});

  // ортақ қойма: қолдау болса қосылады
  (async function(){
    try{
      if(!window.claude||!window.claude.use)return;
      var db=await window.claude.use("db"),as=await window.claude.use("assets");
      if(!db)return;
      st.db=db;st.assets=as;
      db.collection("materials").orderBy("createdAt","desc").onSnapshot(function(snap){
        shared=snap.docs.map(function(d){var x=d.data()||{};return {src:(x.url&&!x.assetId)?"link":"shared",did:d.id,url:x.url,t:x.title,s:x.subject,g:x.grade,ty:x.type,aid:x.assetId,fn:x.fileName}});
        render();
      },function(){});
      render();
    }catch(e){}
  })();
})();
</script>
</body>
</html>
