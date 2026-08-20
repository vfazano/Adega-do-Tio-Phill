<template>
  <div class="app">
    <!-- HEADER -->
    <header class="header">
      <div class="header-content">
        <div class="brand">
          <img src="/logo-tio-phill.png" alt="Adega do Tio Phill" />
          <div>
            <h1>Adega do Tio Phill</h1>
            <span>Seu copão, sua bebida, seu momento 🍻</span>
          </div>
        </div>

        <button class="cart-button" @click="mostrarCarrinho = true">
          🛒
          <span>Meu pedido</span>
          <strong>{{ quantidadeTotal }}</strong>
        </button>
      </div>
    </header>

    <!-- HERO -->
    <section class="hero">
      <div class="hero-content">
        <span class="hero-tag">🍻 ADEGA DO TIO PHILL</span>

        <h2>
          Seu rolê começa
          <span>aqui.</span>
        </h2>

        <p>
          Escolha suas bebidas, monte seu pedido
          e deixe o resto com a gente.
        </p>

        <a href="#produtos" class="hero-button">Ver produtos</a>
      </div>
    </section>

    <!-- CATEGORIAS -->
    <section class="categories">
      <h2>O que você procura?</h2>

      <div class="category-list">
        <button
          @click="categoriaSelecionada = 'Todos'"
          :class="{ active: categoriaSelecionada === 'Todos' }"
        >
          🍻 Todos
        </button>

        <button
          @click="categoriaSelecionada = 'Copões'"
          :class="{ active: categoriaSelecionada === 'Copões' }"
        >
          🥤 Copões
        </button>

        <button
          @click="categoriaSelecionada = 'Cervejas'"
          :class="{ active: categoriaSelecionada === 'Cervejas' }"
        >
          🍺 Cervejas
        </button>

        <button
          @click="categoriaSelecionada = 'Destilados'"
          :class="{ active: categoriaSelecionada === 'Destilados' }"
        >
          🥃 Destilados
        </button>

        <button
          @click="categoriaSelecionada = 'Energéticos'"
          :class="{ active: categoriaSelecionada === 'Energéticos' }"
        >
          ⚡ Energéticos
        </button>
      </div>
    </section>

    <!-- PRODUTOS -->
    <main id="produtos" class="products-section">
      <div class="section-title">
        <span>MENU</span>
        <h2>Nossos produtos</h2>
      </div>

      <div class="products-grid">
        <article
          v-for="produto in produtosFiltrados"
          :key="produto.id"
          class="product-card"
        >
          <div class="product-image">
            <span class="product-emoji">{{ produto.emoji }}</span>
          </div>

          <div class="product-info">
            <span class="product-category">{{ produto.categoria }}</span>
            <h3>{{ produto.nome }}</h3>
            <p>{{ produto.descricao }}</p>

            <div class="product-footer">
              <strong>
                R$ {{ produto.preco.toFixed(2).replace('.', ',') }}
              </strong>

              <button @click="adicionarProduto(produto)">
                + Adicionar
              </button>
            </div>
          </div>
        </article>
      </div>
    </main>

    <!-- BANNER -->
    <section class="order-banner">
      <div>
        <span>🛒 MONTE SEU PEDIDO</span>
        <h2>
          Escolha suas bebidas
          e peça pelo WhatsApp.
        </h2>
      </div>

      <button @click="mostrarCarrinho = true">Ver meu pedido</button>
    </section>

    <!-- FOOTER -->
    <footer class="footer">
      <img src="/logo-tio-phill.png" alt="Adega do Tio Phill" />

      <div>
        <h3>Adega do Tio Phill</h3>
        <p>Bebidas, copões e aquele rolê de respeito. 🍻</p>
      </div>
''
      <div class="footer-links">
        <a href="#">Instagram</a>
        <a href="#">WhatsApp</a>
      </div>
    </footer>

    <!-- CARRINHO -->
    <div
      v-if="mostrarCarrinho"
      class="cart-overlay"
      @click.self="mostrarCarrinho = false"
    >
      <aside class="cart">
        <div class="cart-header">
          <div>
            <span>SEU PEDIDO</span>
            <h2>Meu carrinho 🛒</h2>
          </div>

          <button
            class="close-button"
            @click="mostrarCarrinho = false"
          >
            ×
          </button>
        </div>

        <!-- CARRINHO VAZIO -->
        <div v-if="carrinho.length === 0" class="empty-cart">
          <span>🛒</span>
          <h3>Seu pedido está vazio</h3>
          <p>Adicione algumas bebidas para começar.</p>
        </div>

        <!-- PRODUTOS DO CARRINHO -->
        <div v-else class="cart-content">
          <div
            v-for="item in carrinho"
            :key="item.id"
            class="cart-item"
          >
            <div class="cart-item-icon">{{ item.emoji }}</div>

            <div class="cart-item-info">
              <h3>{{ item.nome }}</h3>

              <strong>
                R$ {{ (item.preco * item.quantidade).toFixed(2).replace('.', ',') }}
              </strong>

              <div class="quantity">
                <button @click="diminuirQuantidade(item)">−</button>
                <span>{{ item.quantidade }}</span>
                <button @click="aumentarQuantidade(item)">+</button>
              </div>
            </div>

            <button
              class="remove-button"
              @click="removerProduto(item)"
            >
              🗑️
            </button>
          </div>

          <!-- TOTAL -->
          <div class="cart-total">
            <span>Total</span>
            <strong>
              R$ {{ totalCarrinho.toFixed(2).replace('.', ',') }}
            </strong>
          </div>

          <!-- DADOS DO CLIENTE -->
          <div class="customer-form">
            <h3>Seus dados</h3>

            <input
              v-model="cliente.nome"
              type="text"
              placeholder="Seu nome"
            />

            <input
              v-model="cliente.telefone"
              type="tel"
              placeholder="Telefone / WhatsApp"
            />

            <input
              v-model="cliente.endereco"
              type="text"
              placeholder="Endereço"
            />

            <select v-model="cliente.pagamento">
              <option value="">Forma de pagamento</option>
              <option value="Pix">Pix</option>
              <option value="Dinheiro">Dinheiro</option>
              <option value="Cartão">Cartão</option>
            </select>

            <textarea
              v-model="cliente.observacao"
              placeholder="Observação do pedido"
              rows="3"
            ></textarea>
          </div>

          <button class="finish-button" @click="finalizarPedido">
            📲 Enviar pedido
          </button>
        </div>
      </aside>
    </div>

    <!-- AVISO DE IDADE -->
    <div v-if="mostrarAvisoIdade" class="age-overlay">
      <div class="age-modal">
        <img src="/logo-tio-phill.png" alt="Adega do Tio Phill" />

        <h2>Você tem 18 anos ou mais?</h2>

        <p>
          A venda e o consumo de bebidas alcoólicas
          são destinados exclusivamente a maiores de 18 anos.
        </p>

        <div class="age-buttons">
          <button class="age-yes" @click="confirmarIdade">
            Sim, tenho 18+
          </button>

          <button class="age-no" @click="sairDoSite">
            Não
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue'

// =========================
// PRODUTOS
// =========================
const produtos = ref([
  {
    id: 1,
    nome: 'Copão Tio Phill',
    categoria: 'Copões',
    descricao: 'Copão especial da casa.',
    preco: 25.00,
    emoji: '🥤'
  },
  {
    id: 2,
    nome: 'Copão Red',
    categoria: 'Copões',
    descricao: 'Copão preparado com energético.',
    preco: 30.00,
    emoji: '🥤'
  },
  {
    id: 3,
    nome: 'Cerveja Long Neck',
    categoria: 'Cervejas',
    descricao: 'Cerveja long neck.',
    preco: 8.00,
    emoji: '🍺'
  },
  {
    id: 4,
    nome: 'Cerveja Lata',
    categoria: 'Cervejas',
    descricao: 'Cerveja em lata.',
    preco: 5.00,
    emoji: '🍺'
  },
  {
    id: 5,
    nome: 'Vodka',
    categoria: 'Destilados',
    descricao: 'Vodka.',
    preco: 45.00,
    emoji: '🥃'
  },
  {
    id: 6,
    nome: 'Whisky',
    categoria: 'Destilados',
    descricao: 'Whisky.',
    preco: 90.00,
    emoji: '🥃'
  },
  {
    id: 7,
    nome: 'Energético',
    categoria: 'Energéticos',
    descricao: 'Energético.',
    preco: 12.00,
    emoji: '⚡'
  }
])

// =========================
// CATEGORIA
// =========================
const categoriaSelecionada = ref('Todos')

const produtosFiltrados = computed(() => {
  if (categoriaSelecionada.value === 'Todos') {
    return produtos.value
  }

  return produtos.value.filter(
    produto => produto.categoria === categoriaSelecionada.value
  )
})

// =========================
// CARRINHO
// =========================
const carrinho = ref([])

function adicionarProduto(produto) {
  const item = carrinho.value.find(
    item => item.id === produto.id
  )

  if (item) {
    item.quantidade++
  } else {
    carrinho.value.push({
      ...produto,
      quantidade: 1
    })
  }
}

function aumentarQuantidade(item) {
  item.quantidade++
}

function diminuirQuantidade(item) {
  if (item.quantidade > 1) {
    item.quantidade--
  } else {
    removerProduto(item)
  }
}

function removerProduto(item) {
  carrinho.value = carrinho.value.filter(
    produto => produto.id !== item.id
  )
}

const quantidadeTotal = computed(() => {
  return carrinho.value.reduce(
    (total, item) => total + item.quantidade,
    0
  )
})

const totalCarrinho = computed(() => {
  return carrinho.value.reduce(
    (total, item) => total + item.preco * item.quantidade,
    0
  )
})

// =========================
// CLIENTE
// =========================
const cliente = ref({
  nome: '',
  telefone: '',
  endereco: '',
  pagamento: '',
  observacao: ''
})

// =========================
// CARRINHO ABERTO
// =========================
const mostrarCarrinho = ref(false)

// =========================
// FINALIZAR PEDIDO
// =========================
function finalizarPedido() {
  if (carrinho.value.length === 0) {
    alert('Adicione algum produto ao pedido.')
    return
  }

  if (
    !cliente.value.nome ||
    !cliente.value.telefone ||
    !cliente.value.endereco ||
    !cliente.value.pagamento
  ) {
    alert('Preencha todos os seus dados.')
    return
  }

  let mensagem = '🍻 *NOVO PEDIDO - ADEGA DO TIO PHILL*%0A%0A'
  mensagem += `👤 *Cliente:* ${cliente.value.nome}%0A`
  mensagem += `📱 *Telefone:* ${cliente.value.telefone}%0A`
  mensagem += `📍 *Endereço:* ${cliente.value.endereco}%0A`
  mensagem += `💳 *Pagamento:* ${cliente.value.pagamento}%0A%0A`
  mensagem += '🛒 *PEDIDO:*%0A'

  carrinho.value.forEach(item => {
    mensagem += `${item.quantidade}x ${item.nome} - R$ ${(item.preco * item.quantidade).toFixed(2)}%0A`
  })

  mensagem += `%0A💰 *TOTAL: R$ ${totalCarrinho.value.toFixed(2)}*%0A`

  if (cliente.value.observacao) {
    mensagem += `%0A📝 *Observação:* ${cliente.value.observacao}`
  }

  // COLOQUE AQUI O WHATSAPP DA ADEGA
  const telefoneAdega = '5515997487428'

  const url = `https://wa.me/${telefoneAdega}?text=${mensagem}`

  window.open(url, '_blank')
}

// =========================
// IDADE
// =========================
const mostrarAvisoIdade = ref(
  !localStorage.getItem('idade-confirmada')
)

function confirmarIdade() {
  localStorage.setItem('idade-confirmada', 'true')
  mostrarAvisoIdade.value = false
}

function sairDoSite() {
  window.location.href = 'https://www.google.com'
}
</script>

<style scoped>
* {
  box-sizing: border-box;
}

.app {
  min-height: 100vh;
  background: #07152e;
  color: white;
  font-family: Arial, sans-serif;
}

/* HEADER */
.header {
  background: #091a38;
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
  padding: 15px 5%;
}

.header-content {
  max-width: 1200px;
  margin: auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
}

.brand {
  display: flex;
  align-items: center;
  gap: 12px;
}

.brand img {
  width: 65px;
  height: 65px;
  object-fit: contain;
}

.brand h1 {
  margin: 0;
  color: #ff2b2b;
  font-size: 24px;
}

.brand span {
  color: #aaa;
  font-size: 13px;
}

/* CARRINHO BUTTON */
.cart-button {
  border: none;
  background: #ff2929;
  color: white;
  padding: 12px 18px;
  border-radius: 10px;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 8px;
}

.cart-button strong {
  background: white;
  color: #ff2929;
  padding: 3px 7px;
  border-radius: 50%;
}

/* HERO */
.hero {
  min-height: 500px;
  display: flex;
  align-items: center;
  padding: 60px 8%;
  background:
    radial-gradient(
      circle at right,
      rgba(255, 40, 40, 0.25),
      transparent 40%
    );
}

.hero-content {
  max-width: 650px;
}

.hero-tag {
  color: #ff3030;
  font-weight: bold;
  letter-spacing: 2px;
}

.hero h2 {
  font-size: clamp(45px, 7vw, 80px);
  line-height: 0.95;
  margin: 20px 0;
}

.hero h2 span {
  color: #ff3030;
}

.hero p {
  color: #aaa;
  font-size: 18px;
  line-height: 1.7;
}

.hero-button {
  display: inline-block;
  margin-top: 20px;
  background: #ff3030;
  color: white;
  padding: 15px 25px;
  border-radius: 10px;
  text-decoration: none;
  font-weight: bold;
}

/* CATEGORIAS */
.categories {
  max-width: 1200px;
  margin: auto;
  padding: 30px 5%;
}

.categories h2 {
  margin-bottom: 20px;
}

.category-list {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
}

.category-list button {
  border: 1px solid #263a5d;
  background: #0d2040;
  color: white;
  padding: 12px 18px;
  border-radius: 30px;
  cursor: pointer;
}

.category-list button.active,
.category-list button:hover {
  background: #ff3030;
  border-color: #ff3030;
}

/* PRODUTOS */
.products-section {
  max-width: 1200px;
  margin: auto;
  padding: 60px 5%;
}

.section-title span {
  color: #ff3030;
  font-size: 13px;
  font-weight: bold;
}

.section-title h2 {
  font-size: 40px;
  margin-top: 8px;
}

.products-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 20px;
}

.product-card {
  background: #0d2040;
  border: 1px solid #1d3357;
  border-radius: 16px;
  overflow: hidden;
  transition: 0.3s;
}

.product-card:hover {
  transform: translateY(-5px);
  border-color: #ff3030;
}

.product-image {
  height: 220px;
  display: flex;
  align-items: center;
  justify-content: center;
  background:
    linear-gradient(
      135deg,
      #101f3c,
      #08142b
    );
}

.product-emoji {
  font-size: 90px;
}

.product-info {
  padding: 20px;
}

.product-category {
  color: #ff3030;
  font-size: 12px;
  font-weight: bold;
  text-transform: uppercase;
}

.product-info h3 {
  margin: 8px 0;
}

.product-info p {
  color: #8f9bb0;
  font-size: 14px;
}

.product-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 20px;
}

.product-footer strong {
  font-size: 20px;
}

.product-footer button {
  background: #ff3030;
  color: white;
  border: none;
  padding: 10px 12px;
  border-radius: 8px;
  cursor: pointer;
}

/* BANNER */
.order-banner {
  max-width: 1100px;
  margin: 40px auto;
  padding: 40px;
  background: #ff3030;
  border-radius: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 30px;
}

.order-banner h2 {
  margin: 8px 0 0;
}

.order-banner button {
  border: none;
  padding: 15px 20px;
  border-radius: 10px;
  cursor: pointer;
  font-weight: bold;
}

/* FOOTER */
.footer {
  padding: 40px 5%;
  background: #050f20;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 30px;
  flex-wrap: wrap;
}

.footer img {
  width: 70px;
}

.footer p {
  color: #8895a9;
}

.footer-links {
  display: flex;
  gap: 20px;
}

.footer-links a {
  color: white;
  text-decoration: none;
}

/* CARRINHO */
.cart-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.75);
  z-index: 100;
  display: flex;
  justify-content: flex-end;
}

.cart {
  width: min(500px, 100%);
  height: 100%;
  background: #081832;
  overflow-y: auto;
  padding: 25px;
}

.cart-header {
  display: flex;
  justify-content: space-between;
}

.cart-header span {
  color: #ff3030;
  font-size: 12px;
}

.cart-header h2 {
  margin-top: 5px;
}

.close-button {
  background: none;
  border: none;
  color: white;
  font-size: 35px;
  cursor: pointer;
}

.cart-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 15px 0;
  border-bottom: 1px solid #1c3152;
}

.cart-item-icon {
  font-size: 40px;
}

.cart-item-info {
  flex: 1;
}

.cart-item-info h3 {
  margin: 0 0 5px;
}

.cart-item-info strong {
  color: #ff3030;
}

.quantity {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-top: 8px;
}

.quantity button {
  width: 28px;
  height: 28px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}

.remove-button {
  background: none;
  border: none;
  cursor: pointer;
}

.empty-cart {
  text-align: center;
  padding: 60px 20px;
}

.empty-cart > span {
  font-size: 50px;
}

.empty-cart p {
  color: #8f9bb0;
}

.cart-total {
  display: flex;
  justify-content: space-between;
  font-size: 22px;
  padding: 25px 0;
}

.cart-total strong {
  color: #ff3030;
}

/* FORM */
.customer-form {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.customer-form h3 {
  margin-bottom: 5px;
}

.customer-form input,
.customer-form select,
.customer-form textarea {
  width: 100%;
  padding: 13px;
  background: #102647;
  border: 1px solid #263d60;
  border-radius: 8px;
  color: white;
  outline: none;
}

.customer-form input:focus,
.customer-form select:focus,
.customer-form textarea:focus {
  border-color: #ff3030;
}

.finish-button {
  width: 100%;
  margin-top: 20px;
  padding: 16px;
  background: #25d366;
  color: white;
  border: none;
  border-radius: 10px;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
}

/* IDADE */
.age-overlay {
  position: fixed;
  inset: 0;
  z-index: 999;
  background: rgba(0, 0, 0, 0.9);
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
}

.age-modal {
  max-width: 430px;
  text-align: center;
  background: #0b1c38;
  border: 1px solid #ff3030;
  border-radius: 20px;
  padding: 35px;
}

.age-modal img {
  width: 120px;
}

.age-modal h2 {
  margin-top: 20px;
}

.age-modal p {
  color: #9da8b8;
  line-height: 1.6;
}

.age-buttons {
  display: flex;
  gap: 10px;
  margin-top: 25px;
}

.age-buttons button {
  flex: 1;
  padding: 13px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-weight: bold;
}

.age-yes {
  background: #ff3030;
  color: white;
}

.age-no {
  background: #253653;
  color: white;
}

/* RESPONSIVO */
@media (max-width: 700px) {
  .header-content {
    align-items: flex-start;
  }

  .brand span {
    display: none;
  }

  .cart-button span {
    display: none;
  }

  .hero {
    min-height: 450px;
    padding: 50px 7%;
  }

  .hero h2 {
    font-size: 50px;
  }

  .order-banner {
    margin: 30px 5%;
    padding: 30px;
    flex-direction: column;
    align-items: flex-start;
  }

  .footer {
    flex-direction: column;
    align-items: flex-start;
  }
}
</style>
