<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Flag Drop Spin Game</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body{
    margin:0;
    background:#020617;
    font-family:system-ui;
    display:flex;
    flex-direction:column;
    align-items:center;
}
#top{
    margin-top:10px;
    color:white;
    font-size:18px;
}
#game{
    margin-top:10px;
    width:320px;
    height:320px;
    position:relative;
}
#circle{
    width:100%;
    height:100%;
    border-radius:50%;
    border:6px solid #38bdf8;
    position:relative;
    overflow:hidden;
}
.flag{
    position:absolute;
    font-size:28px;
}
#mouth{
    position:absolute;
    right:-10px;
    top:50%;
    transform:translateY(-50%);
    width:40px;
    height:60px;
    background:black;
    clip-path: polygon(0 0,100% 50%,0 100%);
}
#dropzone{
    margin-top:15px;
    width:100%;
    min-height:80px;
    border-top:2px dashed #334155;
    display:flex;
    flex-wrap:wrap;
    justify-content:center;
    gap:10px;
    padding:10px;
}
.drop-flag{
    font-size:32px;
    animation: drop 0.6s ease-out;
}
@keyframes drop{
    from{ transform:translateY(-40px); opacity:0;}
    to{ transform:translateY(0); opacity:1;}
}
#winner{
    margin-top:10px;
    color:#22c55e;
    font-size:20px;
}
</style>
</head>

<body>

<div id="top">🌍 Auto Spin Flag Game</div>

<div id="game">
    <div id="circle">
        <div id="mouth"></div>
    </div>
</div>

<div id="dropzone"></div>

<div id="winner"></div>

<script>
let flags = ["🇧🇩","🇮🇳","🇵🇰","🇺🇸","🇬🇧","🇯🇵","🇨🇳","🇷🇺","🇫🇷","🇩🇪","🇧🇷","🇮🇹","🇨🇦","🇦🇺","🇰🇷","🇲🇾"];
let circle = document.getElementById("circle");
let dropzone = document.getElementById("dropzone");
let winner = document.getElementById("winner");

let angle = 0;

function render(){
    circle.querySelectorAll(".flag").forEach(e=>e.remove());

    let total = flags.length;
    let r = 120;

    flags.forEach((f,i)=>{
        let a = (i/total)*Math.PI*2 + angle;
        let x = Math.cos(a)*r + 160 - 14;
        let y = Math.sin(a)*r + 160 - 14;

        let d = document.createElement("div");
        d.className="flag";
        d.innerText=f;
        d.style.left=x+"px";
        d.style.top=y+"px";
        circle.appendChild(d);
    });
}

render();

function spinRound(){
    let spinTime = 2000;
    let start = Date.now();

    let spin = setInterval(()=>{
        angle += 0.25;
        render();

        if(Date.now() - start > spinTime){
            clearInterval(spin);

            if(flags.length > 1){
                eliminate();
                setTimeout(spinRound, 700);
            } else {
                winner.innerHTML = "🏆 Winner: " + flags[0];
            }
        }
    },30);
}

function eliminate(){
    let removeIndex = Math.floor(Math.random() * flags.length);
    let removed = flags.splice(removeIndex,1)[0];

    let d = document.createElement("div");
    d.className="drop-flag";
    d.innerText = removed;
    dropzone.appendChild(d);

    render();
}

setTimeout(spinRound, 800);
</script>

</body>
</html><br >
![](https://github.com/ymrdf/html-2-apk/raw/master/pic/15.png)



