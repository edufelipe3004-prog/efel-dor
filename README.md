<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Efel D'or | Brigadeiros</title>

<style>
*{
  margin:0;
  padding:0;
  box-sizing:border-box;
  font-family:Arial, Helvetica, sans-serif;
}

body{
  background:#fffaf4;
  color:#3a2a1a;
}

header{
  background:linear-gradient(135deg,#4b2c1a,#b8860b);
  color:white;
  padding:20px;
  text-align:center;
}

header h1{
  font-size:36px;
}

header p{
  margin:10px 0;
  font-size:18px;
}

.btn{
  background:#b8860b;
  color:white;
  padding:12px 22px;
  border:none;
  border-radius:8px;
  cursor:pointer;
  font-size:16px;
  transition:.3s;
  margin:5px;
}

.btn:hover{
  background:#a17608;
}

.btn.active{
  background:#4b2c1a;
}

section{
  padding:50px 20px;
  max-width:1100px;
  margin:auto;
}

.hero{
  text-align:center;
}

.hero h2{
  font-size:32px;
}

.cards{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(230px,1fr));
  gap:20px;
  margin-top:25px;
}

.card{
  background:white;
  padding:20px;
  border-radius:15px;
  box-shadow:0 0 10px rgba(0,0,0,.1);
  text-align:center;
}

.rules{
  background:#fff1da;
  border-radius:15px;
  margin-top:30px;
}

.no-delivery{
  background:#ffe2e2;
  border:2px solid #ff6b6b;
  border-radius:15px;
  padding:20px;
  text-align:center;
  font-weight:bold;
  font-size:18px;
  color:#8b0000;
  margin-top:20px;
}

footer{
  background:#4b2c1a;
  color:white;
  text-align:center;
  padding:20px;
}

.cart{
  background:white;
  padding:20px;
  border-radius:15px;
  box-shadow:0 0 10px rgba(0,0,0,.1);
}
</style>
</head>

<body>

<header>
  <h1>Efel D'or</h1>
  <p>Qualidade de ouro que cabe no seu bolso.</p>
  <button class="btn" onclick="openWhats()">Peça agora pelo WhatsApp</button>
</header>

<section class="hero">
  <h2>Brigadeiros feitos para impressionar.</h2>
  <p>Produzidos com ingredientes selecionados, muito amor e uma pitada de magia.</p>
  <br>
  <button class="btn" onclick="scrollToProducts()">Quero experimentar agora</button>
</section>

<section id="produtos">
  <h2>Combos</h2>

  <div class="cards">

    <div class="card">
      <h3>Combo Tradicional (Todos brigadeiro)</h3>
      <p>Somente brigadeiros tradicionais.</p>
      <p><b>R$ 10,00</b></p>
      <button class="btn" onclick="addItem('Combo Tradicional (Todos brigadeiro)',10)">Comprar agora</button>
    </div>

    <div class="card">
      <h3>Combo Normal</h3>
      <p>2 tradicionais, 1 ninho com Nutella, 1 ninho e 1 de ninho misturado com tradicional</p>
      <p><b>R$ 10,00</b></p>
      <button class="btn" onclick="addItem('Combo Normal',10)">Comprar agora</button>
    </div>

    <div class="card">
      <h3>Caixa com 100</h3>
      <p>Sabores escolhidos no WhatsApp</p>
      <p><b>R$ 200,00</b></p>
      <button class="btn" onclick="addItem('Caixa com 100 (Sabores escolhidos no WhatsApp)',200)">Comprar agora</button>
    </div>

  </div>
</section>

<section class="rules">
  <h2>Regras e Detalhes do Pedido</h2>
  <p><b>Quantidade mínima:</b> 2 unidades por sabor em cada combo.</p>
  <p><b>Pedidos grandes:</b> mínimo de 15 unidades.</p>
  <p><b>Prazos:</b></p>
  <p>Pedidos grandes: mínimo de 5 dias de antecedência.</p>
  <p>Combos menores: prazo de 1 a 3 dias.</p>
</section>

<section class="no-delivery">
  ⚠️ NÃO FAZEMOS ENTREGAS ⚠️ <br>
  Retirada somente no local.
</section>

<section>
  <h2>Forma de Pagamento</h2>
  <button class="btn" id="pixBtn" onclick="setPayment('Pix')">Pagar com Pix</button>
  <button class="btn" id="dinheiroBtn" onclick="setPayment('Dinheiro')">Pagar em Dinheiro</button>
</section>

<section>
  <h2>Carrinho</h2>
  <div class="cart">
    <ul id="cartList"></ul>
    <p><b>Total:</b> R$ <span id="total">0</span></p>
    <p><b>Pagamento:</b> <span id="paymentText">Não selecionado</span></p>
    <br>
    <button class="btn" onclick="finishOrder()">Finalizar pedido pelo WhatsApp</button>
  </div>
</section>

<footer>
  <p>Efel D'or - Todos os direitos reservados</p>
</footer>

<script>
let cart = [];
let total = 0;
let paymentMethod = "";

function scrollToProducts(){
  document.getElementById("produtos").scrollIntoView({behavior:"smooth"});
}

function openWhats(){
  window.open("https://wa.me/5534991157477?text=Olá,%20gostaria%20de%20fazer%20um%20pedido%20na%20Efel%20D'or.","_blank");
}

function addItem(name,price){
  cart.push({name,price});
  total += price;
  updateCart();
}

function setPayment(method){
  paymentMethod = method;
  document.getElementById("paymentText").innerText = method;

  document.getElementById("pixBtn").classList.remove("active");
  document.getElementById("dinheiroBtn").classList.remove("active");

  if(method === "Pix"){
    document.getElementById("pixBtn").classList.add("active");
  }else{
    document.getElementById("dinheiroBtn").classList.add("active");
  }
}

function updateCart(){
  let list = document.getElementById("cartList");
  list.innerHTML = "";

  cart.forEach(item=>{
    let li = document.createElement("li");
    li.textContent = `${item.name} - R$ ${item.price}`;
    list.appendChild(li);
  });

  document.getElementById("total").innerText = total.toFixed(2);
}

function finishOrder(){
  if(cart.length==0){
    alert("Seu carrinho está vazio.");
    return;
  }

  if(paymentMethod==""){
    alert("Selecione a forma de pagamento.");
    return;
  }

  let message = "Olá, gostaria de fazer o seguinte pedido na Efel D'or:%0A";

  cart.forEach(item=>{
    message += `- ${item.name} (R$ ${item.price})%0A`;
  });

  message += `%0ATotal: R$ ${total.toFixed(2)}`;
  message += `%0AForma de pagamento: ${paymentMethod}`;
  message += `%0ARetirada no local. (Sem entrega)`;

  window.open(`https://wa.me/5534991157477?text=${message}`,"_blank");
}
</script>

</body>
</html>
