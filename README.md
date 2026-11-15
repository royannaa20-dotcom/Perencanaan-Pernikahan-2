<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Perencana Pernikahan</title>
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-database-compat.js"></script>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:wght@500;600&family=Figtree:wght@400;600&display=swap" rel="stylesheet">
<style>
:root{--bg:#fdeef3;--sf:#fffafc;--ink:#4a2b3b;--mu:#7d586a;--ln:#f3cddb;--ac:#b53a6e;--on:#fff;--gd:#7a5aa6;--p1:#fbd5e3;--p2:#e8defa;--p3:#d6f0e4;--p4:#ffe7d2;color-scheme:light;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#2a1822;--sf:#34202b;--ink:#fbe8ef;--mu:#c9a3b3;--ln:#553444;--ac:#f4a3c2;--on:#3b1626;--gd:#c9b2f0;--p1:#4d2b3d;--p2:#3d3354;--p3:#254238;--p4:#4f3b2c;color-scheme:dark}}
:root[data-theme="dark"]{--bg:#2a1822;--sf:#34202b;--ink:#fbe8ef;--mu:#c9a3b3;--ln:#553444;--ac:#f4a3c2;--on:#3b1626;--gd:#c9b2f0;--p1:#4d2b3d;--p2:#3d3354;--p3:#254238;--p4:#4f3b2c;color-scheme:dark}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*,*::before,*::after{box-sizing:inherit}
body{margin:0;color:var(--ink);font:15px/1.55 Figtree,system-ui,-apple-system,"Segoe UI",Roboto,sans-serif;background:radial-gradient(50rem 26rem at 100% -5%,var(--p2),transparent 70%),radial-gradient(40rem 24rem at 0 100%,var(--p3),transparent 70%),var(--bg);background-attachment:fixed}
.w{max-width:1040px;margin:0 auto;padding:28px 18px 56px}
h1,h2,.big{font-family:Fraunces,Georgia,serif;font-weight:500;letter-spacing:-.01em}
h1{font-size:clamp(1.9rem,6vw,3rem);line-height:1.1;margin:0}
h2{font-size:1.5rem;margin:0 0 4px}
.sub{color:var(--mu);margin:0 0 16px;max-width:62ch}
.hd{display:flex;justify-content:space-between;align-items:flex-end;gap:12px 24px;flex-wrap:wrap;margin-bottom:18px}
.bar{display:flex;gap:8px;align-items:center;flex-wrap:wrap}
.q{color:var(--mu);font-size:.9rem}
nav{display:flex;gap:4px;overflow-x:auto;border-bottom:1px solid var(--ln);margin-bottom:24px}
.tab{background:none;border:0;border-bottom:2px solid transparent;color:var(--mu);font:inherit;padding:10px 14px;cursor:pointer;white-space:nowrap}
.tab.on{color:var(--ac);border-color:var(--ac);font-weight:600}
.hero{display:flex;align-items:baseline;gap:14px;flex-wrap:wrap;margin-bottom:12px}
.big{font-size:clamp(4rem,18vw,8rem);line-height:1;color:var(--ac)}
.hl{font-size:1.2rem;color:var(--gd)}
.st{display:grid;grid-template-columns:repeat(auto-fit,minmax(170px,1fr));gap:10px;margin:0 0 22px}
.st div{padding:12px 14px;border-radius:14px;background:var(--p1)}
.st div:nth-child(4n+2){background:var(--p2)}.st div:nth-child(4n+3){background:var(--p3)}.st div:nth-child(4n+4){background:var(--p4)}
.st span{display:block;color:var(--mu);font-size:.85rem}
.st b{font:500 1.25rem Fraunces,Georgia,serif}
.sc{overflow-x:auto;background:var(--sf);border:1px solid var(--ln);border-radius:16px}
table{border-collapse:collapse;width:100%;min-width:760px}
th{text-align:left;font-weight:600;font-size:.85rem;padding:10px 6px;background:var(--p1)}
td{padding:3px 4px;border-bottom:1px solid var(--ln);vertical-align:top}
tr:last-child td{border-bottom:0}
td.e{padding:18px 8px;color:var(--mu)}
input,select,textarea{font:inherit;color:inherit;background:transparent;border:1px solid transparent;border-radius:8px;padding:7px 8px;width:100%}
select option{color:#4a2b3b;background:#fff}
td input:hover,td select:hover,td textarea:hover{border-color:var(--ln)}
input:focus-visible,select:focus-visible,textarea:focus-visible,button:focus-visible{outline:2px solid var(--ac);outline-offset:1px}
textarea.t{display:block;min-width:190px;min-height:0;margin:0;border-color:transparent;background:transparent;font-size:1em;line-height:1.4;resize:none;overflow:hidden}td select{min-width:120px}input[type=number]{min-width:110px}input.rp{min-width:140px;text-align:right}
select[data-st]{border-radius:999px;font-weight:600;padding:6px 10px}
.s0{background:var(--p4)}.s1{background:var(--p2)}.s2{background:var(--p3)}
.cv{display:block;padding:8px;white-space:nowrap}
.done .t{text-decoration:line-through;color:var(--mu)}
.b{background:var(--ac);color:var(--on);border:1.5px solid var(--ac);border-radius:999px;padding:8px 18px;font:inherit;font-weight:600;cursor:pointer;width:auto}
.g{background:transparent;color:var(--ac)}
.x{background:none;border:0;color:var(--mu);font-size:1.3rem;cursor:pointer;padding:2px 8px}
.x:hover{color:var(--ink)}
.act{display:flex;gap:8px;margin-top:16px;flex-wrap:wrap}
.fm{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:14px;margin-bottom:30px}
.fm label{display:block;color:var(--mu);font-size:.85rem}
.fm input,textarea{border-color:var(--ln);background:var(--sf);margin-top:4px}
textarea{min-height:90px;font-size:.8rem}
footer{margin-top:40px;color:var(--mu);font-size:.85rem;max-width:70ch}
#msg{color:var(--gd);font-size:.9rem;margin-top:8px;min-height:1.3em}
h3{font:500 1.05rem Fraunces,Georgia,serif;margin:0 0 8px}
.seg{display:inline-flex;flex-wrap:wrap;gap:4px;background:var(--p1);border-radius:999px;padding:4px;margin-bottom:14px}
.seg button{border:0;background:transparent;color:var(--ink);font:inherit;padding:6px 14px;border-radius:999px;cursor:pointer}
.seg button.on{background:var(--ac);color:var(--on);font-weight:600}
.cg{display:grid;grid-template-columns:repeat(auto-fit,minmax(min(100%,320px),1fr));gap:14px;margin-bottom:22px}
.cc,.dd{background:var(--sf);border:1px solid var(--ln);border-radius:16px;padding:14px}
.dd{margin-bottom:30px}
.cw{position:relative;height:420px}.cw.s{height:300px}
.ir{display:flex;justify-content:space-between;gap:12px;padding:6px 0;border-bottom:1px solid var(--ln)}
@media (max-width:720px){
table{min-width:0}
thead{display:none}
table,tbody,tr,td{display:block;width:100%}
tr{padding:10px 12px;border-bottom:1px solid var(--ln)}
tr:last-child{border-bottom:0}
td,tr:last-child td{border:0;padding:4px 0}
td[data-label]::before{content:attr(data-label);display:block;color:var(--mu);font-size:.78rem;margin-bottom:2px}
td input,td select,td textarea.t{border-color:var(--ln);background:var(--sf)}
td.e{padding:18px 8px}
td:last-child{text-align:right}
.sc{overflow-x:visible}
}
</style>
</head>
<body>
<div class="w">
<header class="hd"><h1 id="ttl"></h1><div class="bar" id="bar"></div></header>
<p class="q" id="sy"></p>
<nav id="nav"></nav>
<main id="app"></main>
<footer>Isian tersimpan otomatis di browser ini. Tombol Simpan memastikan data tersimpan, dan Reset mengembalikan semuanya ke template awal agar bisa dipakai orang lain.</footer>
</div>
<script>
// ===== PENGATURAN SAMBUNGAN ONLINE (isi sekali) =====
// Tempel alamat Realtime Database Firebase di antara tanda kutip. Biarkan kosong untuk mode lokal.
var FB={databaseURL:""};
</script>
<script>
(function(){
var K="wp-v2",cl=o=>JSON.parse(JSON.stringify(o)),$=s=>document.querySelector(s);
var PH=["6-12 Bulan Sebelum","4-6 Bulan Sebelum","2-3 Bulan Sebelum","1-2 Bulan Sebelum","1 Minggu Sebelum"],BY=["Belum","DP","Lunas"],TS=["Belum","Proses","Selesai"],GC=["Keluarga","Kerabat","Teman","Rekan kerja","Tetangga","VIP"];
var TABS=[["home","Ringkasan"],["cost","Anggaran"],["check","Timeline"],["run","Rundown"],["guest","Tamu"],["mahar","Mahar dan seserahan"],["vendor","Kontak"]];
var T={
cost:{t:"Anggaran dan kebutuhan",d:"Isi estimasi bawah dan atas tiap item. Jika estimasi atas dikosongkan, dianggap sama dengan estimasi bawah.",f:[["cat","Kategori","text"],["n","Item kebutuhan","text"],["est","Estimasi bawah (Rp)","rp"],["max","Estimasi atas (Rp)","rp"],["act","Pengeluaran aktual (Rp)","rp"],["st","Status pembayaran","sel",BY,1],["note","Catatan","text"]],b:{cat:"",n:"",est:0,max:0,act:0,st:"Belum",note:""}},
check:{t:"Timeline dan checklist",d:"Urutan persiapan dari 12 bulan sebelum hari H. Ubah status tugas saat sudah dikerjakan.",f:[["ph","Fase waktu","sel",PH],["t","Tugas utama","text"],["pic","Penanggung jawab","text"],["st","Status","sel",TS,1],["note","Catatan","text"]],b:{ph:PH[0],t:"",pic:"Berdua",st:"Belum",note:""}},
run:{t:"Rundown hari H",d:"Jadwal acara dari rias sampai penutupan, lengkap dengan lokasi dan PIC.",f:[["time","Waktu","text"],["ev","Kegiatan / acara","text"],["loc","Lokasi","text"],["pic","PIC","text"],["note","Perlengkapan / keterangan","text"]],b:{time:"",ev:"",loc:"",pic:"",note:""}},
guest:{t:"Daftar tamu",d:"Catat jumlah orang, status undangan, dan konfirmasi kehadiran.",f:[["n","Nama tamu / keluarga","text"],["cat","Kategori","sel",GC],["pax","Jumlah orang","num"],["hp","No. HP / alamat","text"],["inv","Status undangan","sel",["Belum dikirim","Terkirim"],1],["rsvp","RSVP","sel",["Belum konfirmasi","Tidak hadir","Hadir"],1],["note","Catatan","text"]],b:{n:"",cat:"Keluarga",pax:2,hp:"",inv:"Belum dikirim",rsvp:"Belum konfirmasi",note:""}},
mahar:{t:"Mahar dan seserahan",d:"Total estimasi dihitung otomatis dari jumlah dikali harga satuan.",f:[["cat","Kategori","text"],["n","Item / barang","text"],["spec","Merk / spesifikasi","text"],["qty","Jumlah","num"],["price","Harga satuan (Rp)","rp"],["tot","Total estimasi (Rp)","calc"],["act","Harga aktual (Rp)","rp"],["st","Status pembelian","sel",["Belum beli","Sudah beli"],1],["note","Catatan","text"]],b:{cat:"",n:"",spec:"",qty:1,price:0,act:0,st:"Belum beli",note:""}},
vendor:{t:"Kontak vendor dan panitia",d:"Simpan nama dan nomor WhatsApp semua pihak yang terlibat di hari H.",f:[["cat","Kategori","sel",["Kepanitiaan","Vendor"]],["n","Peran / vendor","text"],["pic","Nama kontak (PIC)","text"],["wa","No. WhatsApp","text"],["note","Tugas / catatan","text"]],b:{cat:"Vendor",n:"",pic:"",wa:"",note:""}}};
function rows(k,keys,txt){keys=keys.split(" ");return txt.split("\n").map(l=>{var o=cl(T[k].b),p=l.split("|");keys.forEach((x,i)=>{if(p[i]){var f=T[k].f.filter(q=>q[0]===x)[0];o[x]=f[2]==="num"||f[2]==="rp"?+p[i]:p[i]}});return o})}
var D={names:"",date:"",
cost:rows("cost","cat n est note",`Administrasi & Legal|Pendaftaran KUA/Catatan Sipil|1000000|Gratis di KUA (hari kerja)
Administrasi & Legal|Surat Pengantar Desa/Kelurahan||Tergantung kebijakan RT/RW
Mahar & Cincin|Cincin Kawin (Sepasang)|3000000|Tergantung gram & bahan
Mahar & Cincin|Mahar Pernikahan|2500000|Sesuai kesepakatan berdua
Mahar & Cincin|Kotak Mahar & Seserahan|2600000|Sewa kotak atau beli sendiri
Acara & Resepsi|Sewa Gedung/Venue||Bisa dihapus jika di rumah/tenda
Acara & Resepsi|Katering (Misal: 500 pax)|20000000|Asumsi Rp40k-100k per pax
Acara & Resepsi|Dekorasi Venue & Pelaminan|5000000
Acara & Resepsi|Sound System & Hiburan|2000000
Pakaian & Rias|MUA & Hairdo/Hijab (Pengantin)|3000000|Sangat krusial, amankan awal
Pakaian & Rias|Busana & Rias Keluarga Inti|2000000
Dokumentasi|Fotografer & Videografer|3000000|Bisa tambah paket pre-wedding
Undangan & Souvenir|Undangan (Cetak & Digital)|500000
Undangan & Souvenir|Souvenir (Misal: 500 pcs)|2500000|Asumsi Rp5k-20k per pcs
Kesehatan|Pre-marital Check-up|1000000|Bisa pakai rujukan Puskesmas
Lain-lain|Biaya Tak Terduga (10%)|5000000|Wajib ada sbg dana darurat acara
Pakaian & Rias|Seragam Bridesmaid / Panitia / Keluarga|1000000|Kain atau Baju jadi
Undangan & Souvenir|Buku Tamu, Alat Tulis, Kotak Angpao|100000|Kerap terlewat saat belanja
Printilan & Logistik|Sewa Mobil Pengantin & Hiasan Bunga|500000|Termasuk bensin & supir
Printilan & Logistik|Transportasi Keluarga Besar (Bus/Hiace)|1000000|Antar jemput keluarga ke venue
Printilan & Logistik|Penginapan / Hotel Transit Keluarga|1000000|Jika ada keluarga dari luar kota
Printilan & Logistik|Konsumsi Rapat Panitia & Gladi Bersih|500000|Makan siang/malam saat kumpul
Printilan & Logistik|Konsumsi Sarapan Vendor (Hari-H)|300000|Agar kru & MUA tetap prima
Printilan & Logistik|Amplop Tip Vendor, Kru, MC|300000|Siapkan amplop kecil & pecahan uang
Printilan & Logistik|Keamanan, Parkir & Izin Keramaian|200000|RT/RW, Polsek, Karang Taruna setempat`),
check:rows("check","ph t pic note",`6-12 Bulan Sebelum|Tentukan tanggal & estimasi jumlah tamu|Berdua|Berpengaruh ke booking venue
6-12 Bulan Sebelum|Bahas budget & pembagian biaya acara|Berdua|Penting disepakati sejak awal
6-12 Bulan Sebelum|Booking Venue & Katering|Berdua|Segera amankan tanggal & DP
4-6 Bulan Sebelum|Booking MUA, Fotografer & Dekorasi|Berdua
4-6 Bulan Sebelum|Pre-marital Checkup|Berdua|Cek darah rutin, golongan darah
2-3 Bulan Sebelum|Urus Surat N1-N4 (RT, Kelurahan, KUA)|Masing-masing|Syarat administrasi negara
2-3 Bulan Sebelum|Beli Cincin Kawin & Pesan Seserahan|Berdua
1-2 Bulan Sebelum|Sebar Undangan Digital & Cetak|Berdua
1-2 Bulan Sebelum|Fitting Baju Terakhir & Tes Makeup|Pengantin
1 Minggu Sebelum|Technical Meeting dengan semua vendor|Keluarga & Vendor|Finalisasi rundown acara
1 Minggu Sebelum|Fokus istirahat & kurangi pekerjaan berat|Berdua|Jaga kondisi kulit & kesehatan`),
run:rows("run","time ev loc pic note",`04:00 - 06:00|Makeup Pengantin & Keluarga Inti|Ruang Rias|MUA & WO|Pastikan pengantin sarapan terlebih dahulu
06:00 - 07:00|Briefing Panitia & Cek Kesiapan Venue|Venue|Ketua Panitia|Cek sound, katering, dekor, & AC
07:30 - 08:00|Penyambutan Keluarga Mempelai Pria|Area Depan|Penerima Tamu|Siapkan kalung melati & seserahan
08:00 - 09:30|Prosesi Akad Nikah|Panggung Utama|Penghulu & MC|Siapkan berkas, meja akad, mahar, cincin, mic
09:30 - 10:30|Sesi Foto Keluarga Inti & Sungkeman|Pelaminan|Fotografer|Ikuti list panduan foto keluarga
10:30 - 11:00|Ganti Busana Resepsi / Retouch|Ruang Rias|MUA|Keluarga bersiap di posisi penyambutan
11:00 - 13:00|Resepsi Sesi 1 & Ramah Tamah|Venue|MC & WO|Katering utama dibuka, hiburan mulai
13:00 - 15:00|Resepsi Sesi 2 & Penutupan|Venue|MC & WO|Makan bersama panitia pasca acara`),
guest:[],
mahar:rows("mahar","cat n spec qty price note",`Mahar Utama|Logam Mulia|Sesuai kesepakatan|1|2500000|Bisa berupa emas batangan / perhiasan / uang hias
Perhiasan|Cincin Kawin|Emas / Palladium / Platinum|2|1500000|Harga untuk sepasang
Alat Ibadah|Mukena & Sajadah|Bahan sutra/katun premium|1|500000|Bisa tambah Al-Quran
Perawatan Tubuh (Bodycare)|Lulur, Body Lotion, Bodymist|Satu rangkaian merk sama|1|200000|Sesuaikan dengan kebiasaan calon istri
Perawatan Wajah (Skincare)|Sabun Muka, Moist, Micellar, Sunscreen|Sesuai kondisi kulit|1|500000
Make Up|Bedak, Lipstik, Eyeshadow|Rangkaian kosmetik harian|1|300000
Toiletries|Handuk, Bodywash, Shampo||1|300000
Pakaian|Piyama dan underware||1|500000
Kotak|Biaya per kotak||6|50000`),
vendor:rows("vendor","cat n note",`Kepanitiaan|Ketua Panitia Keluarga|Kordinator utama hari H (Pastikan orang yang tegas)
Kepanitiaan|Penerima Tamu & Jaga Angpao|Mengarahkan tamu VIP, mengamankan kotak uang
Kepanitiaan|Kordinator Katering|Memantau kelancaran piring kotor & isi ulang makanan
Kepanitiaan|Kordinator Perlengkapan|Bawa cincin, mahar, dan berkas KUA agar tidak tertinggal
Vendor|KUA / Penghulu|Koordinasi waktu kedatangan jemputan
Vendor|Make-Up Artist (MUA)|Konfirmasi jam mulai makeup & jumlah orang yang dirias
Vendor|Dekorasi & Venue|Tenggat waktu loading & bongkar barang
Vendor|Katering|Pilihan menu, jumlah porsi, & waktu penyajian
Vendor|Fotografi & Videografi|Siapkan kertas daftar foto wajib keluarga & VIP
Vendor|MC & Hiburan (Band/Sound)|Daftar putar lagu (playlist) / do and don’ts`)};
var S=cl(D),cur="home",rc=false;
try{var o=JSON.parse(localStorage.getItem(K));if(o&&typeof o==="object"&&!Array.isArray(o))S=Object.assign(S,o)}catch(e){}
function fix(){Object.keys(T).forEach(k=>{if(!Array.isArray(S[k]))S[k]=cl(D)[k]})}
fix();
var KEYS=Object.keys(T),rm=null,ref=null,online=false,pend=false;
try{rm=localStorage.getItem("wp-room")}catch(e){}
function sy(t){var e=$("#sy");if(e)e.innerHTML=E(t)+(rm&&ref?" <button class='b g' data-room='out' style='padding:2px 12px'>Ganti ruangan</button>":"")}
function persist(k){
var ok=true;try{localStorage.setItem(K,JSON.stringify(S))}catch(e){ok=false}
if(!ref)return ok;
try{var u={};if(!k||k==="top"){u.names=S.names||"";u.date=S.date||""}
KEYS.forEach(x=>{if(!k||k===x)u[x]=S[x].length?S[x]:null});
ref.update(JSON.parse(JSON.stringify(u)));return true}catch(e){return false}}
function canon(o){return JSON.stringify(o,(k,v)=>v&&typeof v==="object"&&!Array.isArray(v)?Object.keys(v).sort().reduce((a,x)=>(a[x]=v[x],a),{}):v)}
function busy(){var a=document.activeElement;return !!(a&&/^(INPUT|TEXTAREA|SELECT)$/.test(a.tagName)&&$("#app").contains(a))}
function gate(){$("#nav").innerHTML="";$("#app").innerHTML=`<h2>Masuk ke ruangan</h2><p class='sub'>Masukkan kode ruangan yang sama di semua perangkat. Kode ini berfungsi seperti kata sandi, jadi buat yang panjang dan sulit ditebak (6 sampai 40 huruf kecil, angka, atau tanda hubung).</p><div class='fm'><label>Kode ruangan<input id='rmc' autocomplete='off' placeholder='contoh: rina-dimas-2027-x7k'></label></div><div class='act'><button class='b' data-room='1'>Masuk</button></div><div id='msg' class='q' role='status'></div>`}
function connect(){
if(!FB.databaseURL){sy("Mode lokal: data hanya tersimpan di browser ini.");return}
if(typeof firebase==="undefined"){sy("Layanan online tidak dapat dimuat, memakai mode lokal.");return}
if(!rm||!/^[a-z0-9_-]{6,40}$/.test(rm)){gate();return}
if(!firebase.apps.length)firebase.initializeApp(FB);
var db=firebase.database();
ref=db.ref("rooms/"+rm);sy("Menyambungkan...");
db.ref(".info/connected").on("value",s=>{online=!!s.val();sy(online?"Tersambung ke ruangan "+rm:"Tidak ada koneksi. Perubahan dikirim saat tersambung kembali.")});
ref.on("value",s=>{var v=s.val();
if(v===null){S=cl(D);persist();return}
var n={names:v.names||"",date:v.date||""};KEYS.forEach(k=>{n[k]=Array.isArray(v[k])?v[k]:[]});
if(canon(n)===canon(S))return;
S=n;try{localStorage.setItem(K,JSON.stringify(S))}catch(e){}
if(busy())pend=true;else render()},e=>sy("Gagal tersambung: "+e.message))}
var E=s=>String(s==null?"":s).replace(/[&<>"]/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;"}[c]));
var fm=n=>String(n).replace(/\B(?=(\d{3})+(?!\d))/g,"."),Rp=n=>{n=Math.round(+n||0);return (n<0?"-":"")+"Rp "+fm(Math.abs(n))},sum=(a,f)=>a.reduce((s,r)=>s+(+f(r)||0),0),c=(l,v)=>"<div><span>"+l+"</span><b>"+v+"</b></div>",sc=(i,n)=>"s"+(i===0?0:i===n-1?2:1);
function bud(){var mn=sum(S.cost,r=>r.est),mx=sum(S.cost,r=>r.max>0?r.max:r.est),ac=sum(S.cost,r=>r.act);return c("Estimasi minimal",Rp(mn))+c("Estimasi maksimal",Rp(mx))+c("Sudah dikeluarkan",Rp(ac))+c("Sisa dana (dari maksimal)",Rp(mx-ac))}
function tasks(){var a=S.check,d=a.filter(r=>r.st==="Selesai").length;return c("Tugas selesai",d+" dari "+a.length)+c("Progres",(a.length?Math.round(d/a.length*100):0)+"%")}
function stats(k){var a=S[k];
if(k==="cost")return bud();
if(k==="check")return tasks();
if(k==="guest"){var h=a.filter(r=>r.rsvp!=="Tidak hadir");return c("Total undangan",a.length)+c("Estimasi hadir",sum(h,r=>r.pax)+" orang")+c("Konfirmasi hadir",sum(a.filter(r=>r.rsvp==="Hadir"),r=>r.pax)+" orang")+c("Undangan terkirim",a.filter(r=>r.inv==="Terkirim").length+" dari "+a.length)}
if(k==="mahar")return c("Total estimasi",Rp(sum(a,r=>r.qty*r.price)))+c("Total aktual",Rp(sum(a,r=>r.act)))+c("Sudah dibeli",a.filter(r=>r.st==="Sudah beli").length+" dari "+a.length);
if(k==="vendor")return c("Jumlah kontak",a.length)+c("Nomor terisi",a.filter(r=>r.wa).length+" dari "+a.length);
return c("Jumlah kegiatan",a.length)}
function hst(){return bud()+tasks()+c("Tamu hadir",sum(S.guest.filter(r=>r.rsvp==="Hadir"),r=>r.pax)+" orang")}
function cdHtml(){if(!S.date)return '<span class="big">—</span><span class="hl">Pilih tanggal pernikahan di bawah</span>';
var n=Math.round((new Date(S.date+"T00:00:00")-new Date(new Date().toDateString()))/864e5);
return n>0?'<span class="big">'+n+'</span><span class="hl">hari menuju hari bahagia</span>':n===0?'<span class="big">Hari ini</span>':'<span class="big">Selesai</span><span class="hl">Selamat menempuh hidup baru</span>'}
function inp(k,i,f,r){var n=f[0],t=f[2],v=r[n],a='data-k="'+k+'" data-i="'+i+'" data-f="'+n+'" aria-label="'+f[1]+'"';
if(t==="calc")return '<span class="cv">'+Rp(r.qty*r.price)+"</span>";
if(t==="sel"){var o=f[3];return "<select"+(f[4]?' class="'+sc(o.indexOf(v),o.length)+'" data-st="1"':"")+" "+a+">"+o.map(x=>"<option"+(x===v?" selected":"")+">"+E(x)+"</option>").join("")+"</select>"}
if(t==="rp")return '<input class="rp" type="text" inputmode="numeric" placeholder="Rp 0" '+a+' value="'+(v?Rp(v):"")+'">';
if(t==="num")return '<input type="number" min="0" inputmode="numeric" '+a+' value="'+(v||"")+'">';
return '<textarea class="t" rows="1" '+a+">"+E(v)+"</textarea>"}
function home(){return '<div class="hero" id="cd"></div><div class="st" id="st"></div>'+chh()+
'<h2>Data pernikahan</h2><p class="sub">Dipakai untuk judul halaman dan hitung mundur.</p>'+
'<div class="fm"><label>Nama mempelai<input data-top="names" value="'+E(S.names)+'" placeholder="Contoh: Rina dan Dimas"></label>'+
'<label>Tanggal pernikahan<input type="date" data-top="date" value="'+E(S.date)+'"></label></div>'+
'<h2>Cadangan data</h2><p class="sub">Salin teks cadangan untuk memindahkan data ke perangkat lain, lalu tempel dan pulihkan di sana.</p>'+
'<textarea id="bk" aria-label="Teks cadangan" spellcheck="false"></textarea>'+
'<div class="act"><button class="b g" data-bk="show">Tampilkan dan salin</button><button class="b" data-bk="load">Pulihkan dari teks</button></div><div id="msg" role="status"></div>'}
function panel(k){var q=T[k],h="<h2>"+q.t+'</h2><p class="sub">'+q.d+'</p><div class="st" id="st"></div><div class="sc"><table><thead><tr>'+q.f.map(f=>"<th>"+f[1]+"</th>").join("")+"<th></th></tr></thead><tbody>";
if(!S[k].length)h+='<tr><td class="e" colspan="'+(q.f.length+1)+'">Belum ada data. Pilih “Tambah baris” untuk memulai.</td></tr>';
S[k].forEach((r,i)=>{h+="<tr"+(k==="check"&&r.st==="Selesai"?' class="done"':"")+">"+q.f.map(f=>'<td data-label="'+f[1]+'">'+inp(k,i,f,r)+"</td>").join("")+'<td><button class="x" data-del="'+k+":"+i+'" aria-label="Hapus baris">×</button></td></tr>'});
return h+'</tbody></table></div><div class="act"><button class="b" data-add="'+k+'">Tambah baris</button></div>'}
function bar(m){$("#bar").innerHTML=rc?'<span class="q">Kembalikan semua isian ke template awal'+(ref?" untuk semua pengguna ruangan ini":"")+'?</span><button class="b" data-rs="y">Ya, reset</button><button class="b g" data-rs="n">Batal</button>':'<button class="b" data-sv="1">Simpan</button><button class="b g" data-rs="ask">Reset</button>'+(m?'<span class="q" role="status">'+m+"</span>":"")}
function meta(){$("#ttl").textContent=S.names||"Hari bahagia kita";var s=$("#st");if(!s)return;if(cur==="home"){$("#cd").innerHTML=cdHtml();s.innerHTML=hst()}else s.innerHTML=stats(cur)}
function render(){$("#nav").innerHTML=TABS.map(t=>'<button class="tab'+(t[0]===cur?" on":"")+'" data-tab="'+t[0]+'">'+t[1]+"</button>").join("");$("#app").innerHTML=cur==="home"?home():panel(cur);meta();growAll();CH.forEach(x=>x.destroy());CH=[];if(cur==="home"){charts();dd()}}
var PAL=['#f4a3c2','#c9b2f0','#9fdcc0','#ffc9a3','#a9d4f5','#f7d794','#e6a8d7','#b5ead7','#ffb7b2'],M='est',sel=null,CH=[],MN={est:'Estimasi bawah',max:'Estimasi atas',act:'Aktual'},hv=(e,a)=>{if(e.native)e.native.target.style.cursor=a.length?'pointer':'default'},go=k=>setTimeout(()=>{cur=k;render()},0);
function cats(){var m={},o=[];S.cost.forEach(r=>{var k=r.cat||'Lainnya';if(!m[k]){m[k]={n:k,est:0,max:0,act:0,items:[]};o.push(m[k])}m[k].est+=+r.est||0;m[k].max+=(+r.max>0?+r.max:+r.est)||0;m[k].act+=+r.act||0;m[k].items.push(r)});return o}
function segh(){return ['est','max','act'].map(m=>`<button class='${m===M?'on':''}' data-m='${m}'>${MN[m]}</button>`).join('')}
function chh(){return `<h2>Grafik anggaran</h2><p class='sub'>Arahkan kursor untuk melihat angka. Klik irisan atau batang untuk melihat rincian kategori, dan klik nama di legenda untuk menyembunyikan data.</p><div class='seg' id='seg'>${segh()}</div><div class='cg'><div class='cc'><h3>Komposisi anggaran</h3><div class='cw'><canvas id='c1'></canvas></div></div><div class='cc'><h3>Estimasi dan aktual per kategori</h3><div class='cw'><canvas id='c2'></canvas></div></div></div><div class='dd' id='dd'></div><h2>Progres dan tamu</h2><p class='sub'>Klik grafik untuk membuka tab terkait.</p><div class='cg'><div class='cc'><h3>Progres tugas per fase</h3><div class='cw s'><canvas id='c3'></canvas></div></div><div class='cc'><h3>Kehadiran tamu</h3><div class='cw s'><canvas id='c4'></canvas></div></div></div>`}
function dd(){var e=$('#dd');if(!e)return;var x=cats().filter(c=>c.n===sel)[0];if(!x){e.innerHTML=`<p class='q'>Klik irisan atau batang pada grafik untuk melihat rincian kategori.</p>`;return}e.innerHTML=`<h3>${E(x.n)} · ${Rp(x[M])}</h3>`+x.items.map(r=>`<div class='ir'><span>${E(r.n)}</span><span>${Rp(M==='act'?r.act:(M==='max'&&r.max>0?r.max:r.est))}</span></div>`).join('')+`<div class='act'><button class='b g' data-go='cost'>Buka tab Anggaran</button></div>`}
function pick(n){sel=sel===n?null:n;if(CH[0]){CH[0].data.datasets[0].offset=cats().map(x=>x.n===sel?18:0);CH[0].update()}dd()}
function charts(){
if(typeof Chart==='undefined'){document.querySelectorAll('.cw').forEach(w=>{w.innerHTML=`<p class='q'>Grafik tidak dapat dimuat. Periksa koneksi internet lalu muat ulang halaman.</p>`});return}
var cs=getComputedStyle(document.documentElement),v=n=>cs.getPropertyValue(n).trim(),ink=v('--ink'),mu=v('--mu'),ln=v('--ln'),sf=v('--sf'),ct=cats(),tt=()=>cats().reduce((s,x)=>s+x[M],0),lg={position:'bottom',labels:{boxWidth:12}};
Chart.defaults.color=ink;Chart.defaults.font.family='Figtree,system-ui,sans-serif';
CH.push(new Chart($('#c1'),{type:'doughnut',data:{labels:ct.map(x=>x.n),datasets:[{data:ct.map(x=>x[M]),backgroundColor:ct.map((x,i)=>PAL[i%PAL.length]),borderColor:sf,borderWidth:2,offset:ct.map(x=>x.n===sel?18:0),hoverOffset:10}]},options:{maintainAspectRatio:false,cutout:'62%',plugins:{legend:lg,tooltip:{callbacks:{label:c=>' '+c.label+': '+Rp(c.parsed)+' ('+(tt()?Math.round(c.parsed/tt()*100):0)+'%)'}}},onHover:hv,onClick:(e,a)=>{if(a.length)pick(ct[a[0].index].n)}},plugins:[{id:'ctr',afterDraw(ch){var a=ch.chartArea,x=ch.ctx,cx=(a.left+a.right)/2,cy=(a.top+a.bottom)/2;x.save();x.textAlign='center';x.fillStyle=ink;x.font='500 16px Fraunces,Georgia,serif';x.fillText(Rp(tt()),cx,cy+2);x.fillStyle=mu;x.font='12px Figtree,sans-serif';x.fillText(MN[M],cx,cy+20);x.restore()}}]}));
CH.push(new Chart($('#c2'),{type:'bar',data:{labels:ct.map(x=>x.n),datasets:[['est','Estimasi bawah',PAL[0]],['max','Estimasi atas',PAL[1]],['act','Aktual',PAL[2]]].map(d=>({label:d[1],data:ct.map(x=>x[d[0]]),backgroundColor:d[2],borderRadius:6}))},options:{indexAxis:'y',maintainAspectRatio:false,scales:{x:{ticks:{callback:v=>String(+(v/1e6).toFixed(1)).replace('.',',')+' jt'},grid:{color:ln}},y:{grid:{display:false}}},plugins:{legend:lg,tooltip:{callbacks:{label:c=>' '+c.dataset.label+': '+Rp(c.parsed.x)}}},onHover:hv,onClick:(e,a)=>{if(a.length)pick(ct[a[0].index].n)}}}));
CH.push(new Chart($('#c3'),{type:'bar',data:{labels:PH.map(p=>p.replace(' Sebelum','')),datasets:[['Selesai',PAL[2]],['Proses',PAL[1]],['Belum',PAL[3]]].map(d=>({label:d[0],data:PH.map(p=>S.check.filter(r=>r.ph===p&&r.st===d[0]).length),backgroundColor:d[1],borderRadius:4}))},options:{maintainAspectRatio:false,scales:{x:{stacked:true,grid:{display:false}},y:{stacked:true,ticks:{precision:0},grid:{color:ln}}},plugins:{legend:lg},onHover:hv,onClick:(e,a)=>{if(a.length)go('check')}}}));
var gs=[['Hadir',PAL[2]],['Belum konfirmasi',PAL[3]],['Tidak hadir',PAL[0]]].map(d=>[d[0],d[1],sum(S.guest.filter(r=>r.rsvp===d[0]),r=>r.pax)]);
if(!S.guest.length)$('#c4').parentNode.innerHTML=`<p class='q'>Belum ada tamu. Tambahkan di tab Tamu.</p>`;
else CH.push(new Chart($('#c4'),{type:'doughnut',data:{labels:gs.map(d=>d[0]),datasets:[{data:gs.map(d=>d[2]),backgroundColor:gs.map(d=>d[1]),borderColor:sf,borderWidth:2,hoverOffset:10}]},options:{maintainAspectRatio:false,cutout:'62%',plugins:{legend:lg,tooltip:{callbacks:{label:c=>' '+c.label+': '+c.parsed+' orang'}}},onHover:hv,onClick:(e,a)=>{if(a.length)go('guest')}}}))}
function grow(el){el.style.height="auto";el.style.height=el.scrollHeight+"px"}
function growAll(){document.querySelectorAll("textarea.t").forEach(grow)}
function say(t){var m=$("#msg");if(m)m.textContent=t}
document.addEventListener("click",e=>{var t=e.target.closest("button");if(!t)return;var d=t.dataset;
if(d.tab||d.go){cur=d.tab||d.go;render()}
else if(d.m){M=d.m;$('#seg').innerHTML=segh();if(CH[0]){CH[0].data.datasets[0].data=cats().map(x=>x[M]);CH[0].update()}dd()}
else if(d.add){S[d.add].push(cl(T[d.add].b));persist(d.add);render()}
else if(d.del){var p=d.del.split(":");S[p[0]].splice(+p[1],1);persist(p[0]);render()}
else if(d.room==="out"){try{localStorage.removeItem("wp-room")}catch(x){}location.reload()}
else if(d.room){var rc2=$("#rmc").value.trim().toLowerCase();if(!/^[a-z0-9_-]{6,40}$/.test(rc2)){say("Kode harus 6 sampai 40 karakter: huruf kecil, angka, atau tanda hubung.");return}rm=rc2;try{localStorage.setItem("wp-room",rc2)}catch(x){}connect();render()}
else if(d.sv){var ok=persist();bar(ok?"Tersimpan pukul "+new Date().toLocaleTimeString("id-ID",{hour:"2-digit",minute:"2-digit"}):"Gagal menyimpan di browser ini. Gunakan cadangan teks di tab Ringkasan.")}
else if(d.rs==="ask"){rc=true;bar()}
else if(d.rs==="n"){rc=false;bar()}
else if(d.rs==="y"){S=cl(D);rc=false;persist();render();bar("Data dikembalikan ke template awal.")}
else if(d.bk==="show"){var a=$("#bk");a.value=JSON.stringify(S);a.select();var ok2=false;try{ok2=document.execCommand("copy")}catch(x){}say(ok2?"Teks cadangan sudah disalin.":"Pilih semua teks di atas, lalu salin.")}
else if(d.bk==="load"){try{var o2=JSON.parse($("#bk").value);if(!o2||typeof o2!=="object"||Array.isArray(o2))throw 0;S=Object.assign(cl(D),o2);fix();persist();render();say("Data berhasil dipulihkan.")}catch(x){say("Teks cadangan tidak valid. Periksa kembali teks yang ditempel.")}}
});
document.addEventListener("change",e=>{var el=e.target,d=el.dataset;
if(d.top){S[d.top]=el.value;persist("top");meta()}
else if(d.f){var rp=el.classList.contains("rp"),r=S[d.k][+d.i],v=rp?(+el.value.replace(/\D/g,"")||0):el.type==="number"?(+el.value||0):el.value,tr=el.closest("tr");if(!r)return;r[d.f]=v;persist(d.k);if(rp)el.value=v?Rp(v):"";
if(d.st)el.className=sc(el.selectedIndex,el.options.length);
if(d.k==="check"&&d.f==="st")tr.classList.toggle("done",v==="Selesai");
var cv=tr.querySelector(".cv");if(cv)cv.textContent=Rp(r.qty*r.price);
meta()}});
document.addEventListener("input",e=>{var el=e.target;if(el.matches("textarea.t"))grow(el);else if(el.classList.contains("rp")){var n=el.value.slice(0,el.selectionStart).replace(/\D/g,"").length,v=el.value.replace(/\D/g,"").replace(/^0+(?=\d)/,"");el.value=v?"Rp "+fm(v):"";var i=0,k=0;for(;i<el.value.length&&k<n;i++)if(/\d/.test(el.value[i]))k++;if(el.value)i=Math.max(i,3);el.setSelectionRange(i,i)}});window.addEventListener("resize",growAll);if(document.fonts&&document.fonts.ready)document.fonts.ready.then(growAll);document.addEventListener("focusout",()=>{if(pend){pend=false;setTimeout(()=>{if(busy())pend=true;else render()},60)}});render();bar();connect();
})();
</script>
</body>
</html>
