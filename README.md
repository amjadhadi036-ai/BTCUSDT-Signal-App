<!doctype html>
<html lang="ur" dir="rtl">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no">
<meta name="theme-color" content="#08111f">
<title>AMJAD BTCUSDT PRO SIGNALS</title>
<style>
*{box-sizing:border-box}body{margin:0;background:#08111f;color:#eaf1fb;font-family:Arial,sans-serif}
header{padding:15px;background:#101d30;border-bottom:1px solid #263951;text-align:center}
h1{font-size:20px;margin:0 0 5px;color:#61d5ff}small,.muted{color:#9db0c8}
main{max-width:900px;margin:auto;padding:12px}.grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:9px}
.card{background:#111f33;border:1px solid #263951;border-radius:12px;padding:12px;margin-bottom:10px;min-width:0}
.wide{grid-column:1/-1}.label{font-size:12px;color:#9db0c8;margin-bottom:6px}
.value{font-size:20px;font-weight:bold;overflow-wrap:anywhere}.green{color:#29d391}.red{color:#ff647c}.yellow{color:#ffd166}.blue{color:#61d5ff}
#signal{font-size:25px;font-weight:bold;text-align:center;padding:12px;border-radius:10px;background:#1a2b42}
button{border:0;border-radius:9px;padding:11px 15px;background:#147db5;color:white;font-weight:bold}
button:active{opacity:.75}.row{display:flex;gap:8px;align-items:center;justify-content:space-between;flex-wrap:wrap}
canvas{width:100%;height:270px;background:#0b1728;border-radius:8px;display:block}
table{width:100%;border-collapse:collapse;font-size:13px}td,th{padding:8px;border-bottom:1px solid #263951;text-align:right}
.note{font-size:12px;line-height:1.7;color:#9db0c8}
#status{font-size:12px;color:#ffd166}
.pill{padding:5px 8px;border-radius:20px;background:#203650;font-size:12px}
@media(min-width:650px){.grid{grid-template-columns:repeat(4,minmax(0,1fr))}}
</style>
</head>
<body>
<header>
<h1>AMJAD BTCUSDT PRO SIGNALS</h1>
<div class="muted">لائیو مارکیٹ تجزیہ • 1 منٹ ڈیٹا • 15 منٹ سگنل</div>
</header>
<main>
<div class="row" style="margin:8px 0 12px">
<span class="pill">Pair: BTCUSDT</span><span class="pill">Analysis: 15m</span><span id="status">ڈیٹا لوڈ ہو رہا ہے...</span>
<button onclick="refreshAll()">ابھی ریفریش کریں</button>
</div>

<div class="card wide">
<div class="label">موجودہ سگنل</div><div id="signal">ڈیٹا کا انتظار ہے</div>
<div id="reason" class="note" style="text-align:center;margin-top:8px">مارکیٹ کا تجزیہ کیا جا رہا ہے۔</div>
</div>

<div class="grid">
<div class="card"><div class="label">BTCUSDT قیمت</div><div class="value blue" id="price">--</div></div>
<div class="card"><div class="label">15 منٹ رجحان</div><div class="value" id="trend">--</div></div>
<div class="card"><div class="label">RSI (14)</div><div class="value" id="rsi">--</div></div>
<div class="card"><div class="label">EMA 9 / 21</div><div class="value" id="emas">--</div></div>
<div class="card"><div class="label">Bollinger Bands</div><div class="value" id="bb">--</div></div>
<div class="card"><div class="label">Buy Pressure</div><div class="value green" id="buy">--</div></div>
<div class="card"><div class="label">Sell Pressure</div><div class="value red" id="sell">--</div></div>
<div class="card"><div class="label">Order Book فرق</div><div class="value" id="book">--</div></div>
</div>

<div class="card wide">
<div class="row"><strong>چارٹ — 15 منٹ کینڈلز</strong><span class="note">سرخ/سبز کینڈلز، پچھلے دن کی سطحیں</span></div>
<canvas id="chart" width="900" height="300"></canvas>
<div class="note">پیلی لائن = گزشتہ دن کا High، نیلی لائن = گزشتہ دن کا Low۔ سگنل بننے پر چارٹ پر LONG یا SHORT نشان لگے گا۔</div>
</div>

<div class="grid">
<div class="card"><div class="label">گزشتہ دن کا High</div><div class="value yellow" id="yhigh">--</div></div>
<div class="card"><div class="label">گزشتہ دن کا Low</div><div class="value blue" id="ylow">--</div></div>
<div class="card"><div class="label">Entry Price</div><div class="value" id="entry">--</div></div>
<div class="card"><div class="label">Stop Loss</div><div class="value red" id="sl">--</div></div>
<div class="card"><div class="label">Take Profit 1</div><div class="value green" id="tp1">--</div></div>
<div class="card"><div class="label">Take Profit 2</div><div class="value green" id="tp2">--</div></div>
<div class="card"><div class="label">EMA 50</div><div class="value" id="ema50">--</div></div>
<div class="card"><div class="label">15m کینڈل کا وقت</div><div class="value" id="candleTime">--</div></div>
</div>

<div class="card wide">
<strong>گزشتہ دن کی کینڈل اور ٹریڈ لیولز</strong>
<table><tr><th>تفصیل</th><th>قیمت</th><th>حیثیت</th></tr>
<tr><td>Yesterday High</td><td id="tabHigh">--</td><td>مزاحمت</td></tr>
<tr><td>Yesterday Low</td><td id="tabLow">--</td><td>سپورٹ</td></tr>
<tr><td>موجودہ سگنل</td><td id="tabSignal">--</td><td id="tabSignalStatus">--</td></tr>
</table>
</div>

<div class="card wide">
<strong>حالیہ سگنلز / ٹریڈ ہسٹری</strong>
<table><thead><tr><th>وقت</th><th>سگنل</th><th>Entry</th><th>SL</th><th>TP1</th></tr></thead><tbody id="history"><tr><td colspan="5">ابھی کوئی سگنل نہیں</td></tr></tbody></table>
</div>

<div class="card wide">
<strong>Institutional Data — BlackRock / Bloomberg</strong>
<div class="grid" style="margin-top:10px">
 <div class="card"><div class="label">BlackRock Bitcoin ETF</div><div class="value blue">IBIT</div><div class="note">BlackRock iShares Bitcoin Trust کی سرکاری Holdings، Net Assets اور Shares Outstanding معلومات</div><a href="https://www.blackrock.com/us/individual/products/333011/ishares-bitcoin-trust" target="_blank" rel="noopener" style="color:#61d5ff">BlackRock کی آفیشل معلومات کھولیں ↗</a></div>
 <div class="card"><div class="label">Bloomberg Bitcoin Benchmark</div><div class="value blue">BRRNY</div><div class="note">BlackRock IBIT کا Benchmark: CME CF Bitcoin Reference Rate — New York Variant۔ یہ Bloomberg Terminal کی live feed نہیں ہے۔</div><a href="https://professional.bloomberg.com/products/data/data-license/" target="_blank" rel="noopener" style="color:#61d5ff">Bloomberg Data License ↗</a></div>
</div>
<div class="note">ڈیٹا کی شفافیت: یہ سیکشن آفیشل عوامی ذرائع کے لنکس دیتا ہے۔ IBIT کی تازہ holdings/flows کو خودکار طور پر ایپ میں لانے کے لیے قابلِ اعتماد، مجاز data endpoint درکار ہے۔ Bloomberg Terminal کی لائیو قیمتیں/flows اس ایپ میں شامل نہیں، کیونکہ ان کے لیے لائسنس اور API رسائی چاہیے۔ کوئی فرضی inflow/outflow سگنل نہیں بنایا جاتا۔</div>
</div>

<div class="card wide note">
<strong>ڈیٹا اور رسک نوٹ</strong><br>
یہ ایپ Binance کے عوامی مارکیٹ ڈیٹا سے معلومات لیتی ہے۔ Bloomberg یا BlackRock کے نجی/ادارہ جاتی ڈیٹا تک اس میں براہ راست رسائی نہیں ہے۔ سگنل تکنیکی اشاروں پر مبنی اندازہ ہے، منافع کی ضمانت نہیں۔ فیوچرز میں لیوریج سے نقصان بہت تیزی سے ہو سکتا ہے؛ ہر ٹریڈ سے پہلے خود تصدیق کریں۔
</div>
</main>
<script>
const API='https://api.binance.com';
let candles=[],daily=null,bookData=null,lastSignalKey='',history=[];
const $=id=>document.getElementById(id);
const fmt=n=>Number.isFinite(n)?n.toLocaleString('en-US',{minimumFractionDigits:2,maximumFractionDigits:2}):'--';
const set=(id,v)=>$(id).textContent=v;
async function getJSON(path){
 const r=await fetch(API+path,{cache:'no-store'});
 if(!r.ok)throw new Error('Binance API '+r.status);
 return r.json();
}
function ema(values,period){
 if(values.length<period)return [];
 const k=2/(period+1);let out=[],prev=values.slice(0,period).reduce((a,b)=>a+b,0)/period;
 out[period-1]=prev;
 for(let i=period;i<values.length;i++){prev=values[i]*k+prev*(1-k);out[i]=prev;}
 return out;
}
function rsi(values,p=14){
 let out=Array(values.length).fill(null);
 if(values.length<=p)return out;
 let gain=0,loss=0;
 for(let i=1;i<=p;i++){let d=values[i]-values[i-1];gain+=Math.max(d,0);loss+=Math.max(-d,0);}
 let ag=gain/p,al=loss/p;
 out[p]=al===0?100:100-100/(1+ag/al);
 for(let i=p+1;i<values.length;i++){
  let d=values[i]-values[i-1];ag=(ag*(p-1)+Math.max(d,0))/p;al=(al*(p-1)+Math.max(-d,0))/p;
  out[i]=al===0?100:100-100/(1+ag/al);
 }return out;
}
function bollinger(v,p=20){
 if(v.length<p)return null;let a=v.slice(-p),m=a.reduce((x,y)=>x+y,0)/p;
 let sd=Math.sqrt(a.reduce((s,x)=>s+(x-m)**2,0)/p);
 return {mid:m,upper:m+2*sd,lower:m-2*sd};
}
function aggregate15(raw){
 const groups=new Map();
 raw.forEach(k=>{
  const t=Number(k[0]),bucket=Math.floor(t/900000)*900000;
  if(!groups.has(bucket))groups.set(bucket,{time:bucket,open:+k[1],high:+k[2],low:+k[3],close:+k[4],volume:+k[5]});
  else{let c=groups.get(bucket);c.high=Math.max(c.high,+k[2]);c.low=Math.min(c.low,+k[3]);c.close=+k[4];c.volume+=+k[5];}
 });
 return [...groups.values()].sort((a,b)=>a.time-b.time);
}
async function loadMarket(){
 const [raw,day,depth,ticker]=await Promise.all([
  getJSON('/api/v3/klines?symbol=BTCUSDT&interval=1m&limit=1000'),
  getJSON('/api/v3/klines?symbol=BTCUSDT&interval=1d&limit=3'),
  getJSON('/api/v3/depth?symbol=BTCUSDT&limit=100'),
  getJSON('/api/v3/ticker/price?symbol=BTCUSDT')
 ]);
 candles=aggregate15(raw);
 // روزانہ کینڈل کا آخری مکمل دن استعمال کریں، موجودہ نامکمل دن نہیں
 const nowDay=Math.floor(Date.now()/86400000)*86400000;
 const prev=day.filter(k=>Number(k[0])<nowDay).slice(-1)[0] || day[day.length-2];
 daily={high:+prev[2],low:+prev[3],open:+prev[1],close:+prev[4],time:+prev[0]};
 bookData=depth;render(+ticker.price);
}
function render(price){
 const closes=candles.map(c=>c.close), highs=candles.map(c=>c.high),lows=candles.map(c=>c.low);
 const e9=ema(closes,9),e21=ema(closes,21),e50=ema(closes,50),rv=rsi(closes),bb=bollinger(closes);
 const i=closes.length-1, last=candles[i];
 if(i<55||!daily||!bookData)throw new Error('مزید ڈیٹا درکار ہے');
 const r=rv[i],a=e9[i],b=e21[i],c=e50[i];
 const bid=bookData.bids.slice(0,20).reduce((s,x)=>s+(+x[0])*(+x[1]),0);
 const ask=bookData.asks.slice(0,20).reduce((s,x)=>s+(+x[0])*(+x[1]),0);
 const total=bid+ask,buyPct=total?bid/total*100:50,sellPct=100-buyPct;
 const bullish=a>b&&b>c&&last.close>a;
 const bearish=a<b&&b<c&&last.close<a;
 const nearHigh=Math.abs(price-daily.high)/price<0.002;
 const nearLow=Math.abs(price-daily.low)/price<0.002;
 let score=0,reasons=[];
 if(bullish){score+=2;reasons.push('EMA 9، 21 اور 50 کا رجحان اوپر ہے');}
 if(bearish){score-=2;reasons.push('EMA 9، 21 اور 50 کا رجحان نیچے ہے');}
 if(r>52&&r<70){score++;reasons.push('RSI مثبت ہے');}
 if(r<48&&r>30){score--;reasons.push('RSI کمزوری دکھا رہا ہے');}
 if(buyPct>55){score++;reasons.push('Order Book میں خریدار زیادہ ہیں');}
 if(sellPct>55){score--;reasons.push('Order Book میں فروخت کا دباؤ زیادہ ہے');}
 if(bb&&price>bb.mid){score+=0.5;reasons.push('قیمت Bollinger کی درمیانی لائن سے اوپر ہے');}
 if(bb&&price<bb.mid){score-=0.5;reasons.push('قیمت Bollinger کی درمیانی لائن سے نیچے ہے');}
 if(nearHigh){score-=0.5;reasons.push('قیمت گزشتہ دن کے High کے قریب ہے');}
 if(nearLow){score+=0.5;reasons.push('قیمت گزشتہ دن کے Low کے قریب ہے');}
 let signal='NO TRADE',cls='yellow';
 if(score>=3&&bullish&&r<72){signal='LONG';cls='green';}
 else if(score<=-3&&bearish&&r>28){signal='SHORT';cls='red';}
 const atr=average(highs.slice(-14).map((h,j)=>h-lows.slice(-14)[j]));
 const risk=Math.max(atr*1.3,price*0.001);
 let sl=signal==='LONG'?price-risk:signal==='SHORT'?price+risk:null;
 let tp1=signal==='LONG'?price+risk*1.5:signal==='SHORT'?price-risk*1.5:null;
 let tp2=signal==='LONG'?price+risk*2.2:signal==='SHORT'?price-risk*2.2:null;
 set('price',fmt(price));$('price').className='value blue';
 set('trend',bullish?'UPTREND':bearish?'DOWNTREND':'SIDEWAYS');$('trend').className='value '+(bullish?'green':bearish?'red':'yellow');
 set('rsi',r.toFixed(1));$('rsi').className='value '+(r>70?'red':r<30?'green':'blue');
 set('emas',fmt(a)+' / '+fmt(b));set('ema50',fmt(c));
 set('bb',bb?fmt(bb.lower)+' - '+fmt(bb.upper):'--');
 set('buy',buyPct.toFixed(1)+'%');set('sell',sellPct.toFixed(1)+'%');
 set('book',bid>ask?'BID مضبوط':ask>bid?'ASK مضبوط':'برابر');
 set('yhigh',fmt(daily.high));set('ylow',fmt(daily.low));set('tabHigh',fmt(daily.high));set('tabLow',fmt(daily.low));
 set('entry',signal==='NO TRADE'?'--':fmt(price));set('sl',sl?fmt(sl):'--');set('tp1',tp1?fmt(tp1):'--');set('tp2',tp2?fmt(tp2):'--');
 set('candleTime',new Date(last.time).toLocaleString());
 $('signal').textContent=signal;$('signal').className=cls;
 set('reason',reasons.join(' • ')||'واضح رجحان موجود نہیں، انتظار کریں۔');
 set('tabSignal',signal);set('tabSignalStatus',signal==='NO TRADE'?'انتظار': 'ممکنہ موقع');
 const key=signal+'-'+last.time;
 if(signal!=='NO TRADE'&&key!==lastSignalKey){
  lastSignalKey=key;history.unshift({time:new Date().toLocaleTimeString(),signal,entry:price,sl,tp1});
  history=history.slice(0,12);drawHistory();
 }
 drawChart(signal,price);
}
function average(a){return a.length?a.reduce((x,y)=>x+y,0)/a.length:0;}
function drawHistory(){
 $('history').innerHTML=history.length?history.map(x=>`<tr><td>${x.time}</td><td class="${x.signal==='LONG'?'green':'red'}">${x.signal}</td><td>${fmt(x.entry)}</td><td>${fmt(x.sl)}</td><td>${fmt(x.tp1)}</td></tr>`).join(''):'<tr><td colspan="5">ابھی کوئی سگنل نہیں</td></tr>';
}
function drawChart(signal,price){
 const cv=$('chart'),ctx=cv.getContext('2d'),W=cv.width,H=cv.height;
 ctx.clearRect(0,0,W,H);
 const data=candles.slice(-55);if(!data.length)return;
 let min=Math.min(...data.map(x=>x.low),daily.low),max=Math.max(...data.map(x=>x.high),daily.high);
 let pad=(max-min)*.09||1;min-=pad;max+=pad;
 const y=v=>H-24-(v-min)/(max-min)*(H-45),step=(W-55)/data.length;
 ctx.strokeStyle='#263951';ctx.lineWidth=1;
 for(let n=0;n<5;n++){let yy=20+n*(H-45)/4;ctx.beginPath();ctx.moveTo(42,yy);ctx.lineTo(W-8,yy);ctx.stroke();}
 function level(v,color,label){ctx.strokeStyle=color;ctx.setLineDash([7,5]);ctx.beginPath();ctx.moveTo(42,y(v));ctx.lineTo(W-8,y(v));ctx.stroke();ctx.setLineDash([]);ctx.fillStyle=color;ctx.font='13px Arial';ctx.fillText(label+' '+fmt(v),48,Math.max(14,y(v)-5));}
 level(daily.high,'#ffd166','Yesterday High');level(daily.low,'#61d5ff','Yesterday Low');
 data.forEach((d,i)=>{
  let x=44+i*step+step/2,up=d.close>=d.open,col=up?'#29d391':'#ff647c';
  ctx.strokeStyle=col;ctx.fillStyle=col;ctx.beginPath();ctx.moveTo(x,y(d.high));ctx.lineTo(x,y(d.low));ctx.stroke();
  let top=y(Math.max(d.open,d.close)),bottom=y(Math.min(d.open,d.close));
  ctx.fillRect(x-Math.max(2,step*.28),top,Math.max(3,step*.56),Math.max(2,bottom-top));
 });
 if(signal!=='NO TRADE'){
  ctx.fillStyle=signal==='LONG'?'#29d391':'#ff647c';ctx.font='bold 16px Arial';
  ctx.fillText(signal+' '+fmt(price),W-180,35);
 }
}
async function refreshAll(){
 try{set('status','ڈیٹا اپڈیٹ ہو رہا ہے...');await loadMarket();set('status','لائیو اپڈیٹ: '+new Date().toLocaleTimeString());}
 catch(e){set('status','خرابی: '+e.message+' — دوبارہ کوشش کریں');console.error(e);}
}
refreshAll();setInterval(refreshAll,15000);
</script>
</body>
</html> BTCUSDT-Signal-App
