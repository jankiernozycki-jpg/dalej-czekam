# dalej-czekam
<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Minęło już tyle...</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;}
body{
    background:#000;
    color:white;
    font-family:Arial,sans-serif;
    overflow:hidden;
    height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
}

.stars{
    position:fixed;
    inset:0;
}

.star{
    position:absolute;
    width:2px;
    height:2px;
    background:white;
    border-radius:50%;
    animation:twinkle 3s infinite ease-in-out;
}

@keyframes twinkle{
    0%,100%{opacity:0.2;transform:scale(1);}
    50%{opacity:1;transform:scale(1.8);}
}

.content{
    position:relative;
    z-index:2;
    text-align:center;
    padding:20px;
}

h1{
    margin-bottom:20px;
    font-size:2rem;
}

#timer{
    margin-top:25px;
    font-size:2rem;
}

input,button{
    padding:10px;
    margin:5px;
}
</style>
</head>
<body>

<div class="stars" id="stars"></div>

<div class="content">
    <h1>Minęło już tyle, a ja nadal będę czekał</h1>

    <input type="datetime-local" id="start">
    <button onclick="generateLink()">Generuj link</button>

    <p id="link" style="margin-top:15px"></p>
    <div id="timer"></div>
</div>

<script>
const stars=document.getElementById('stars');

for(let i=0;i<180;i++){
    const s=document.createElement('div');
    s.className='star';
    s.style.left=Math.random()*100+'%';
    s.style.top=Math.random()*100+'%';
    s.style.animationDelay=(Math.random()*3)+'s';
    stars.appendChild(s);
}

function generateLink(){
    const v=document.getElementById('start').value;
    if(!v) return;
    const ts=new Date(v).getTime();
    const url=location.origin+location.pathname+'?start='+ts;
    document.getElementById('link').innerHTML=
      '<a style="color:white" href="'+url+'">'+url+'</a>';
}

const params=new URLSearchParams(location.search);
const start=params.get('start');

if(start){
    function update(){
        const diff=Date.now()-Number(start);

        const s=Math.floor(diff/1000)%60;
        const m=Math.floor(diff/60000)%60;
        const h=Math.floor(diff/3600000)%24;
        const d=Math.floor(diff/86400000);

        document.getElementById('timer').innerHTML=
          `<div style="margin-bottom:12px;">
             Minęło już tyle, a ja nadal będę czekał
           </div>
           <strong>${d} dni ${h} godz ${m} min ${s} sek</strong>`;
    }

    update();
    setInterval(update,1000);
}
</script>

</body>
</html>
