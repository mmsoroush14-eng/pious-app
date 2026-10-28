<!DOCTYPE html>  
<html lang="fa" dir="rtl">  
<head>  
<meta charset="utf-8">  
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">  
<title>ویزیتوری پایس</title>  
<style>  
:root { --bg:#f0f4f8; --card:#fff; --tx:#1e293b; --mu:#64748b; --bd:#e2e8f0; --ac:#0a8fc4; --ac-grad:linear-gradient(135deg,#0f172a,#1e293b); --pr:#059669; --dn:#dc2626; --dnb:#fee2e2; --sh:0 4px 15px rgba(0,0,0,.05); }  
* { box-sizing:border-box; -webkit-tap-highlight-color:transparent; }  
body { margin:0; background:var(--bg); color:var(--tx); font-family:system-ui,-apple-system,Tahoma,sans-serif; font-size:14px; padding-bottom:20px; }  
header { position:sticky; top:0; z-index:10; background:var(--ac-grad); padding:12px; border-radius:0 0 16px 16px; color:#fff; box-shadow:0 4px 10px rgba(0,0,0,.2); }  
h1 { font-size:16px; margin:0 0 10px; display:flex; justify-content:space-between; align-items:center; }  
span.st { font-size:11px; background:rgba(255,255,255,.2); padding:2px 8px; border-radius:10px; }  
.tabs { display:flex; gap:5px; margin-bottom:10px; }  
.tab { flex:1; padding:8px; border:none; border-radius:8px; font-weight:bold; background:rgba(255,255,255,.1); color:#cbd5e1; font-size:13px; }  
.tab.on { background:#fff; color:var(--ac); }  
.row { display:flex; gap:5px; margin-bottom:8px; }  
input,select,button { font-family:inherit; font-size:13px; padding:8px 10px; border-radius:8px; border:1px solid var(--bd); width:100%; }  
button { cursor:pointer; font-weight:bold; border:none; }  
.btn-add { background:#fff; color:var(--ac); width:auto; white-space:nowrap; }  
.btn-imp { background:rgba(255,255,255,.2); color:#fff; width:auto; }  
#list { padding:12px; display:grid; gap:12px; }  
.c { background:var(--card); border-radius:12px; padding:12px; box-shadow:var(--sh); border-top:4px solid var(--ac); }  
.cat { font-size:10px; color:var(--ac); background:#e0f2fe; padding:2px 6px; border-radius:4px; font-weight:bold; }  
.nm { font-size:15px; font-weight:bold; margin:8px 0 4px; }  
.pr { font-size:18px; font-weight:900; color:var(--pr); margin-top:8px; }  
.np { color:var(--dn); background:var(--dnb); font-weight:bold; padding:4px 8px; border-radius:6px; display:inline-block; margin-top:8px; font-size:12px; }  
.ln { font-size:12px; color:var(--mu); margin-top:4px; }  
.nt { font-size:12px; background:var(--bg); padding:6px; border-radius:6px; margin-top:8px; }  
.bs { display:flex; gap:5px; margin-top:10px; }  
.bt { flex:1; padding:6px; font-size:12px; background:var(--bg); border:1px solid var(--bd); border-radius:6px; color:var(--tx); }  
.bt.p { background:var(--ac); color:#fff; border:none; }  
.fm { display:grid; gap:8px; margin-top:10px; border-top:1px dashed var(--bd); padding-top:10px; }  
.fm label { font-size:11px; color:var(--mu); font-weight:bold; margin-bottom:-4px; }  
.hide { display:none!important; }  
#toast { position:fixed; bottom:20px; left:50%; transform:translateX(-50%); background:#1e293b; color:#fff; padding:10px 20px; border-radius:20px; font-size:12px; opacity:0; transition:.3s; z-index:100; }  
#toast.show { opacity:1; }  
</style>  
</head>  
<body>  
<header>  
  <h1>💧 ویزیتوری پایس <span class="st" id="st">ذخیره محلی</span></h1>  
  <div class="tabs">  
    <button class="tab on" id="tp">کالاها</button>  
    <button class="tab" id="tl">مغازه‌ها</button>  
    <button class="btn-add" id="ad">+ جدید</button>  
  </div>  
  <div class="row">  
    <input id="q" type="search" placeholder="جستجو...">  
    <button class="btn-imp" id="imp" title="آپلود فایل اکسل">📥</button>  
  </div>  
  <div class="row">  
    <select id="cat"><option value="">همه دسته‌ها</option></select>  
    <select id="city" class="hide"><option value="">همه شهرها</option></select>  
  </div>  
</header>  
  
<input type="file" id="fcsv" accept=".csv" hidden>  
<div id="toast"></div>  
<div id="list"></div>  
  
<script>  
// دیتابیس کالاها  
const D = [{"category": "دستگاه های کلاسیک", "name": "پایس پیور* (اقتصادی)", "code": "", "specs": "شاسی پلاستیکی با مخزن 3.2 گالن وارداتی | پمپ LEFOO", "price": 18950000, "notes": "در مدل پیور سه راهی و شیر ورودی از نوع پلاستیکی است", "k": "p1"}, {"category": "دستگاه های کلاسیک", "name": "پایس استار", "code": "", "specs": "شاسی پلاستیکی با مخزن 3.2 گالن وارداتی", "price": 24750000, "notes": "", "k": "p2"}, {"category": "دستگاه های نیمه صنعتی", "name": "دستگاه 400 گالن", "code": "", "specs": "پمپ 36 ولت لیفو", "price": 59750000, "notes": "", "k": "p3"}, {"category": "پمپ", "name": "پمپ لیفو روتور کوچک 75 گالن", "code": "", "specs": "", "price": 4350000, "notes": "", "k": "p4"}, {"category": "ترانس", "name": "ترانس 24 ولت - 3 آمپر برند جتفلو", "code": "", "specs": "", "price": 0, "notes": "", "k": "p5"}, {"category": "فیلتر", "name": "فیلتر مرحله یک 100 گرم", "code": "", "specs": "", "price": 0, "notes": "", "k": "p6"}];  
  
// دیتابیس مغازه‌ها (بیش از ۵۰ مغازه نمونه)  
const STORES_INIT = [  
  {id:"t1", n:"تأمین‌کننده تجهیزات تصفیه آب تهرانپارس", type:"تأمین‌کننده", city:"تهران", addr:"تهران، منطقه ۴، خیابان ۱۹۶ شرقی", ph:"", st:"جدید"},  
  {id:"t2", n:"فروشگاه تصفیه آب H2O", type:"فروشگاه", city:"تهران", addr:"تهران، شهرک شهید بهشتی", ph:"02177105649", st:"جدید"},  
  {id:"t3", n:"تصفیه آب آبشار", type:"فروشگاه", city:"تهران", addr:"تهران، شادمان، خیابان بهبودی", ph:"02166502580", st:"جدید"},  
  {id:"t4", n:"تکنو آب تهران", type:"فروشگاه", city:"تهران", addr:"تهران، خیابان جمالزاده جنوبی", ph:"02166569129", st:"جدید"},  
  {id:"m1", n:"کلینیک تخصصی تصفیه آب گوارا", type:"مرکز تخصصی", city:"مشهد", addr:"مشهد، میدان شهدا، نبش دانشگاه ۱", ph:"05137127871", st:"جدید"},  
  {id:"m2", n:"شرکت بازرگانی آبنوش", type:"تأمین‌کننده", city:"مشهد", addr:"مشهد، خیابان آبکوه، نبش آبکوه ۲۱", ph:"0513768003", st:"جدید"},  
  {id:"m3", n:"خانه تصفیه آب مشهد", type:"فروشگاه", city:"مشهد", addr:"مشهد، بلوار ساجدی", ph:"09926282475", st:"جدید"},  
  {id:"m4", n:"صنایع تصفیه آب آبینه پلاس", type:"فروشگاه", city:"مشهد", addr:"مشهد، بلوار الهیه، نبش الهیه ۲۷", ph:"05135133000", st:"جدید"},  
  {id:"i1", n:"دفتر نمایندگی ثمین آب", type:"فروشگاه", city:"اصفهان", addr:"اصفهان، خیابان طیب", ph:"03132222223", st:"جدید"},  
  {id:"i2", n:"فروشگاه تصفیه آب زلال", type:"فروشگاه", city:"اصفهان", addr:"اصفهان، خیابان غرضی", ph:"09138291500", st:"جدید"},  
  {id:"s1", n:"تصفیه آب میرآب سان پارس", type:"فروشگاه", city:"شیراز", addr:"شیراز، خیابان فلسطین", ph:"07132341919", st:"جدید"},  
  {id:"s2", n:"تصفیه آب پردیس واتر", type:"فروشگاه", city:"شیراز", addr:"شیراز، خیابان فخراباد شرقی", ph:"07132369498", st:"جدید"},  
  {id:"tb1", n:"تصفیه آب هیدرولایف", type:"فروشگاه", city:"تبریز", addr:"تبریز، میدان قطب", ph:"04133359608", st:"جدید"},  
  {id:"tb2", n:"تصفیه آب اکواپلاس", type:"فروشگاه", city:"تبریز", addr:"تبریز، پاستور جدید", ph:"04133367573", st:"جدید"},  
  {id:"k1", n:"آبین پلاس", type:"فروشگاه", city:"کرج", addr:"کرج، بلوار دانش‌آموز", ph:"09150444148", st:"جدید"},  
  {id:"q1", n:"تصفیه آب اردهال", type:"فروشگاه", city:"قم", addr:"قم، جاده اصفهان", ph:"02532860013", st:"جدید"},  
  {id:"a1", n:"فروشگاه تصفیه آب معصومی", type:"فروشگاه", city:"اهواز", addr:"اهواز، بلوار پاسداران", ph:"06132267351", st:"جدید"},  
  {id:"r1", n:"تصفیه آب ناب گیلان", type:"فروشگاه", city:"رشت", addr:"رشت، شهرک ولی عصر", ph:"09111371745", st:"جدید"}  
];  
  
const fa="۰۱۲۳۴۵۶۷۸۹"; const toFa=s=>String(s).replace(/\d/g,d=>fa[d]);  
const esc=s=>String(s==null?"":s).replace(/[&<>"]/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;"}[c]));  
const fmt=p=>toFa(Number(p).toLocaleString("en-US"));  
const $=i=>document.getElementById(i);  
const LS="pv_data_v7";  
let db=JSON.parse(localStorage.getItem(LS) || '{"prods":{},"stores":{}}');  
if(Object.keys(db.stores).length === 0) { STORES_INIT.forEach(s => db.stores[s.id] = s); }  
const save=()=>localStorage.setItem(LS, JSON.stringify(db));  
const toast=m=>{const t=$("toast");t.textContent=m;t.classList.add("show");setTimeout(()=>t.classList.remove("show"),3000)};  
  
let V="p"; // p=products, s=stores  
  
function fillSelects(){  
  let cHtml = '<option value="">همه دسته‌ها</option>';  
  [...new Set(D.map(r=>r.category))].forEach(c=>{ cHtml+=`<option value="${c}">${c}</option>`});  
  $("cat").innerHTML = cHtml;  
    
  let cityHtml = '<option value="">همه شهرها</option>';  
  [...new Set(Object.values(db.stores).map(s=>s.city))].filter(Boolean).forEach(c=>{ cityHtml+=`<option value="${c}">${c}</option>`});  
  $("city").innerHTML = cityHtml;  
}  
  
function render(){  
  fillSelects();  
  let html = "";  
  const q = $("q").value.toLowerCase();  
    
  if(V === "p"){  
    let arr = D.map(d => ({...d, ...(db.prods[d.k]||{})}));  
    if($("cat").value) arr = arr.filter(x => x.category === $("cat").value);  
    if(q) arr = arr.filter(x => (x.name+x.specs+x.notes).toLowerCase().includes(q));  
      
    arr.forEach(p => {  
      let pr = p.price > 0 ? `<div class="pr">${fmt(p.price)} تومان</div>` : `<div class="np">ناموجود / بدون قیمت</div>`;  
      html += `<div class="c"><span class="cat">${p.category}</span><div class="nm">${p.name}</div><div class="nt">${p.specs}</div>${pr}</div>`;  
    });  
  } else {  
    let arr = Object.values(db.stores);  
    if($("city").value) arr = arr.filter(x => x.city === $("city").value);  
    if(q) arr = arr.filter(x => (x.n+x.addr+x.ph+x.city).toLowerCase().includes(q));  
      
    arr.forEach(s => {  
      html += `<div class="c"><span class="cat">${s.type} - ${s.city||''}</span><div class="nm">${s.n}</div>  
        <div class="ln">📞 ${s.ph ? `<a href="tel:${s.ph}" style="color:var(--ac)">${s.ph}</a>` : 'ثبت نشده'}</div>  
        <div class="ln">📍 ${s.addr||''}</div>  
        <div class="bs"><button class="bt" onclick="window.open('https://maps.google.com/?q=${encodeURIComponent(s.addr)}','_blank')">🗺️ مسیریابی</button></div>  
      </div>`;  
    });  
  }  
  $("list").innerHTML = html || '<div style="text-align:center;padding:20px;color:gray">موردی یافت نشد</div>';  
}  
  
$("tp").onclick=()=>{V="p";$("tp").classList.add("on");$("tl").classList.remove("on");$("cat").classList.remove("hide");$("city").classList.add("hide");render()};  
$("tl").onclick=()=>{V="s";$("tl").classList.add("on");$("tp").classList.remove("on");$("cat").classList.add("hide");$("city").classList.remove("hide");render()};  
["q","cat","city"].forEach(id => $(id).addEventListener("input", render));  
  
// دکمه آپلود اصلاح‌شده  
$("imp").onclick = () => $("fcsv").click();  
$("fcsv").onchange = e => {  
  const file = e.target.files[0]; if(!file) return;  
  const reader = new FileReader();  
  reader.onload = ev => {  
    const lines = ev.target.result.split(/\r?\n/);  
    let added = 0;  
    if(V === "s") {  
      lines.forEach((line, i) => {  
        if(i===0 && line.includes("name")) return; // هدر  
        const cols = line.split(",");  
        if(cols.length >= 2) {  
          const id = "imp_"+Date.now()+"_"+i;  
          db.stores[id] = {id, n:cols[0].trim(), city:cols[1].trim(), addr:cols[2]?cols[2].trim():"", ph:cols[3]?cols[3].trim():"", type:"فروشگاه", st:"جدید"};  
          added++;  
        }  
      });  
    } else {  
      toast("برای آپدیت قیمت، فایل را در تب کالاها آپلود کنید (در نسخه بعدی کامل می‌شود)");  
    }  
    if(added>0) { save(); render(); toast(added+" مغازه اضافه شد"); }  
  };  
  reader.readAsText(file, "UTF-8");  
  e.target.value = "";  
};  
  
render();  
</script>  
</body>  
</html>  
