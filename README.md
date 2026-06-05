[index.html](https://github.com/user-attachments/files/28656176/index.html)
<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<title>Feliz Aniversário Juin</title>

<style>

body{
margin:0;
font-family:Arial;
background:linear-gradient(180deg,#0b0b0b,#1a1a1a,#0b0b0b);
color:white;
overflow-y:auto;
}

/* CONTAINER */
.container{
text-align:center;
padding:20px;
max-width:700px;
margin:auto;
}

/* INPUT */
input{
padding:12px;
width:90%;
max-width:280px;
border-radius:10px;
border:none;
background:#2b2b2b;
color:white;
outline:none;
}

/* BOTÕES */
button{
padding:10px 15px;
margin:6px;
border:none;
border-radius:10px;
cursor:pointer;
color:white;
background:#444;
font-size:14px;
}

#btnSim{background:#145a32;}
#btnNao{background:#641e16;}

/* MENSAGEM */
#msg{
min-height:20px;
margin-top:10px;
font-weight:bold;
font-size:14px;
}

/* LISTA */
#lista{
display:grid;
grid-template-columns:repeat(3,1fr);
gap:6px;
margin-top:15px;
}

.tag{
background:#2a2a2a;
padding:8px;
border-radius:8px;
font-size:13px;
}

/* LISTA FINAL */
#listaFinal{
display:none;
margin-top:20px;
display:grid;
grid-template-columns:repeat(3,1fr);
gap:6px;
}

.tagFinal{
background:#0b1f3a;
padding:8px;
border-radius:8px;
font-size:13px;
}

/* SIM NÃO */
#simNao{display:none;margin-top:20px;}

/* FRASES */
.frase{
opacity:0;
transform:translateY(10px);
transition:0.6s ease;
margin-top:10px;
font-size:15px;
}

.frase.show{
opacity:1;
transform:translateY(0);
}

/* IMAGENS */
img{
width:90%;
max-width:260px;
margin:10px auto;
display:block;
border-radius:10px;
opacity:0;
transform:translateY(10px);
transition:0.8s;
}

img.show{
opacity:1;
transform:translateY(0);
}

/* TEXTO FINAL */
#final{
display:none;
margin-top:30px;
text-align:left;
font-family:Georgia, "Times New Roman", serif;
line-height:1.6;
font-size:16px;
}

.blue{
color:#1f4e79;
font-weight:bold;
text-shadow:0 1px 6px rgba(0,0,0,0.4);
}

/* CONFETE LEVE */
.confete{
position:fixed;
top:-10px;
width:6px;
height:6px;
background:red;
animation:fall 2.5s linear forwards;
opacity:0.8;
}

@keyframes fall{
to{
transform:translateY(100vh) rotate(360deg);
opacity:0;
}
}

</style>
</head>

<body>

<div class="container">

<h1>Feliz niversáro Juin</h1>

<p>As veiz parece que você se esquece das suas qualidades</p>

<p>Para te incentivar, digite 10 qualidades suas.. aí você vai ver sua mensagem de aniversario</p>

<input id="input">
<br>

<button onclick="verificar()">Enviar</button>
<button onclick="desistir()">Desistir</button>

<div id="msg"></div>

<h3>O que você lembrou</h3>
<div id="lista"></div>

<!-- SIM NÃO -->
<div id="simNao">
<p id="pergunta"></p>
<button id="btnSim" onclick="escolha('sim')">SIM</button>
<button id="btnNao" onclick="escolha('nao')">NÃO</button>
</div>

<!-- LISTA FINAL -->
<div id="listaFinal"></div>

<!-- FRASES -->
<div id="frases"></div>

<!-- IMAGENS -->
<div id="imagens">
<img src="foto1.png">
<img src="foto2.jpeg">
<img src="foto3.jpeg">
</div>

<!-- TEXTO FINAL -->
<div id="final"></div>

</div>

<script>

const qualidades = [
"Trabalhador","Honesto","Dedicado","Inteligente","Disciplinado",
"Viril","Destemido","Imponente","Divertido","Inspirador",
"Responsável","Determinado","Corajoso","Generoso","Motivado",
"Ambicioso","Focado","Engraçado","Discreto","Franco",
"Maduro","Esforçado","Autêntico","Batalhador","Calmo"
];

const defeitos = ["chato","feio","horrivel","inutil", "arrogante","estranho","horroroso","grosso"];

const autoestima = ["lindo","gato","gostoso","bonito","lindao","gatao","gostosao","bom","bonitao","sensual","sexy"];

let encontradas = [];

/* NORMALIZAÇÃO */
function norm(t){
return t.toLowerCase()
.normalize("NFD").replace(/[\u0300-\u036f]/g,"")
.replace(/[^a-z ]/g,"")
.trim();
}

/* MENSAGEM */
function msg(t){
document.getElementById("msg").innerText=t;
setTimeout(()=>document.getElementById("msg").innerText="",1200);
}

/* LISTA */
function atualizar(){
document.getElementById("lista").innerHTML =
encontradas.map(q=>`<div class="tag">${q}</div>`).join("");
}

/* AUTOESTIMA */
function autoMsg(){
const m=[
"eita que autoestima boaa kk mas nao era isso",
"você sabe que é tudo isso né kk manda outra vai",
"eu concordo kkk mas não era bem isso que devia escrever"
];
return m[Math.floor(Math.random()*m.length)];
}

/* CONFETE LEVE */
function confete(){
for(let i=0;i<40;i++){
let d=document.createElement("div");
d.className="confete";
d.style.left=Math.random()*100+"vw";
d.style.background=`hsl(${Math.random()*360},100%,60%)`;
document.body.appendChild(d);
setTimeout(()=>d.remove(),3000);
}
}

/* VERIFICAR */
function verificar(){

let v = norm(document.getElementById("input").value);
document.getElementById("input").value="";

/* AUTOESTIMA */
if(autoestima.includes(v)){
return msg(autoMsg());
}

/* DEFEITOS */
if(defeitos.includes(v)){
return msg("ta proibido de falar isso de você!");
}

/* QUALIDADES */
let ok = qualidades.find(q=>norm(q)===v);

if(!ok){
return msg("não alembrei dessa, manda outra!");
}

if(!encontradas.includes(ok)){
encontradas.push(ok);
atualizar();
msg(["acertou mosss","você é bom em tudo, como pode?","eita como alembra","iapois essa foi fácil né kk","isso mesmo Juin"][Math.floor(Math.random()*3)]);
}

if(encontradas.length>=10){
inicio();
}
}

function desistir(){
inicio();
}

function inicio(){
document.getElementById("simNao").style.display="block";
document.getElementById("pergunta").innerText="posso amostrar o que eu alembrei de você?";
}

/* FRASES SEM DIGITAÇÃO PESADA */
function showFrase(text){
return new Promise(r=>{
let el=document.createElement("div");
el.className="frase";
el.innerText=text;
document.getElementById("frases").appendChild(el);

setTimeout(()=>el.classList.add("show"),50);
setTimeout(r,1200);
});
}

/* ESCOLHA */
async function escolha(op){

document.getElementById("simNao").style.display="none";

confete();

msg("eeee moss, tu acertou foi é tudo!");

document.getElementById("listaFinal").style.display="grid";
document.getElementById("listaFinal").innerHTML =
qualidades.map(q=>`<div class="tagFinal">${q}</div>`).join("");

await new Promise(r=>setTimeout(r,800));

await showFrase("eu te amostreio quais qualidades eu alembrei de você.. então nunca esqueça delas");
await showFrase("As vezes parece dificil nos olhar com carinho e lembrar das nossas qualidades.. Mas nunca se esqueça das coisas boas que você carrega");

document.getElementById("imagens").scrollIntoView({behavior:"smooth"});

let imgs=document.querySelectorAll("img");

imgs.forEach((img,i)=>{
setTimeout(()=>img.classList.add("show"),i*600);
});

setTimeout(final,2500);
}

/* FINAL */
function final(){

document.getElementById("final").style.display="block";

document.getElementById("final").innerHTML=`
<p class="blue">Juin..</p>

 <div>

  

  
    <p>Você é a melhor pessoa que eu já conheci. Eu sempre vou te olhar com bons olhos e com muito carinho, por isso você tem um lugar especial no meu coração. Eu só         consigo pensar em coisas maravilhosas ao seu respeito</p>

    <p>Não sei o que a vida reservou para cada um de nós, mas eu queria fazer parte da sua vida até quando você ficasse velhinho e corcunda.. existem pessoas que o  tempo leva embora, e existem pessoas que a gente gostaria que o tempo preservasse para sempre. Você é essa pessoa!</p>

    <p>Eu nunca planejei ter você por tanto tempo na minha cabeça. Aliás, eu não planejava que ninguém ocupasse esse espaço, porque as pessoas costumam decepcionar, iludir, se aproveitar e machucar. Durante muito tempo eu achei que ninguém merecia permanecer ali.</p>

    <p>As pessoas hoje em dia parecem cada vez mais superficiais. Poucas valorizam caráter, princípios, esforço e bondade. Poucas se preocupam em se tornar alguém melhor.</p>

    <p>Mas você não...</p>

    <p>Você é uma boa pessoa. Rara de encontrar.</p>

    <p>Eu tenho orgulho do que você é! das suas metas, dos seus sonhos e da forma como enxerga o futuro. Você é muito batalhador e determinado. Mesmo quando as coisas são difíceis, você continua seguindo em frente. E isso te torna único aos meus olhos.</p>

    <p>Com olhar de amiga, de admiradora e de sua fã número #1..eu te desejo um feliz aniversário</p>

    <p>Que Deus lhe dê muita saúde, proteção, sabedoria e força para enfrentar os dias difíceis..Que Ele continue sendo sua paz nos momentos de angústia, sua alegria nos dias felizes e seu refúgio quando tudo parecer pesado.</p>

    <p>Que seus planos deem certo. Que sua vida financeira seja muito próspera. Que você conquiste tudo aquilo pelo que tem trabalhado e sonhado..</p>

    <p>Com muita prosperidade para você voltar para o Brasil para que eu possa te abraçar de novo<br><br>

    <p>Parabéns por ser quem você é! sou sua fã</p>


  </div>

</div>


<div class="blue" style="text-arial:center;margin-top:20px;">
Feliz aniversário, Juin ❤️
</div>
`;
}

/* ENTER */
document.addEventListener("keydown",(e)=>{
if(e.key==="Enter")verificar();
});

</script>

</body>
</html>
