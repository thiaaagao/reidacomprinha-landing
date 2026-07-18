<template>
  <div id="app" class="bg-surface">
    <!-- HERO -->
    <section class="hero">
      <div class="hero-content reveal-1">
        <div class="badge badge-gold">
          <span class="badge-dot"></span>Novas ofertas todo dia &middot; Gratis
        </div>
        <div class="hero-img">
          <img src="/img/rei-sem-fundo.png" alt="Rei da Comprinha">
        </div>
        <h1><span>Curadoria</span> que<br>vale a pena</h1>
        <p>O <strong class="text-gold">Rei</strong> filtra, compara e entrega as melhores ofertas direto no seu celular. Economia real, sem sensacionalismo.</p>
        <div class="flex gap-3 mb-8 justify-center flex-wrap">
          <div class="stat"><span class="stat-num tabular-nums">{{ metrics.offers }}</span><span class="stat-lbl">Ofertas hoje</span></div>
          <div class="stat"><span class="stat-num tabular-nums">{{ metrics.members }}</span><span class="stat-lbl">Membros</span></div>
        </div>
        <a href="https://t.me/MelPromoNandoBot" target="_blank" rel="noopener" class="btn btn-telegram">
          <svg class="w-5 h-5" fill="#0088cc" viewBox="0 0 24 24"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm4.64 6.8c-.15 1.58-.8 5.42-1.13 7.19-.14.75-.42 1-.68 1.03-.58.05-1.02-.38-1.58-.75-.88-.58-1.38-.94-2.23-1.5-.99-.65-.35-1.01.22-1.59.15-.15 2.71-2.48 2.76-2.69.01-.03.01-.14-.07-.2-.08-.06-.19-.04-.27-.02-.12.02-1.96 1.25-5.54 3.66-.52.36-1 .53-1.42.52-.47-.01-1.37-.26-2.03-.48-.82-.27-1.47-.42-1.41-.88.03-.24.37-.49 1.02-.74 4.01-1.75 6.69-2.9 8.04-3.46 3.83-1.59 4.63-1.87 5.15-1.88.11 0 .37.03.54.17.14.12.18.28.2.45-.01.06.01.24 0 .37z"/></svg>
          QUERO ENTRAR NO GRUPO &rarr;
        </a>
      </div>
    </section>

    <!-- TICKER -->
    <div class="ticker">
      <div class="ticker-track">
        <span class="ticker-item"><span class="dot"></span>Ofertas em tempo real</span>
        <span class="ticker-item"><span class="dot"></span>Bot proprio 24/7</span>
        <span class="ticker-item"><span class="dot"></span>100% gratuito</span>
        <span class="ticker-item"><span class="dot"></span>Links diretos</span>
        <span class="ticker-item"><span class="dot"></span>Zero pegadinha</span>
        <span class="ticker-item"><span class="dot"></span>Sem assinatura</span>
        <span class="ticker-item"><span class="dot"></span>Ofertas em tempo real</span>
        <span class="ticker-item"><span class="dot"></span>Bot proprio 24/7</span>
        <span class="ticker-item"><span class="dot"></span>100% gratuito</span>
        <span class="ticker-item"><span class="dot"></span>Links diretos</span>
        <span class="ticker-item"><span class="dot"></span>Zero pegadinha</span>
        <span class="ticker-item"><span class="dot"></span>Sem assinatura</span>
      </div>
    </div>

    <!-- CARROSSEL -->
    <section class="py-20 overflow-hidden" ref="carrosselRef">
      <div class="text-center mb-10 px-5 reveal-2">
        <h2 class="text-xl font-bold text-gold inline-flex items-center gap-2">
          <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M12 2l3.09 6.26L22 9.27l-5 4.87L18.18 22 12 18.56 5.82 22 7 14.14l-5-4.87 6.91-1.01L12 2z"/></svg>
          Ofertas que o Rei Compartilhou
        </h2>
      </div>
      <div class="overflow-hidden">
        <div class="carrossel-track" ref="carrosselTrack" @mouseenter="pauseCarrossel" @mouseleave="resumeCarrossel"
             @touchstart="onTouchStart" @touchend="onTouchEnd">
          <a v-for="o in carrosselItems" :key="o.id" :href="o.link" target="_blank" rel="noopener"
             class="carrossel-item no-underline">
            <div class="carrossel-card">
              <div class="carrossel-badge" v-if="o.desc">{{ o.desc }}</div>
              <div class="carrossel-img"><img :src="o.img" alt="" loading="lazy"></div>
              <div class="carrossel-body">
                <span class="carrossel-nome">{{ o.nome }}</span>
                <span class="carrossel-de">{{ o.de }}</span>
                <span class="carrossel-por">{{ o.por }}</span>
              </div>
            </div>
          </a>
        </div>
      </div>
    </section>

    <!-- CATEGORIAS -->
    <section class="py-16 px-5">
      <div class="max-w-xl mx-auto text-center">
        <span class="section-badge">Categorias</span>
        <h2 class="text-2xl font-black text-white mb-2">Tem oferta pra <span class="text-gold">todo mundo</span></h2>
        <div class="section-divider"></div>
        <p class="text-sub text-sm mb-8">O Rei caca promocoes em todas as categorias. Do celular ao tenis.</p>
        <div class="cat-grid reveal-3">
          <div class="cat-card" v-for="c in categorias" :key="c.name">
            <span class="cat-icon" v-html="c.icon"></span>
            <span class="cat-name">{{ c.name }}</span>
            <span class="cat-count">{{ c.count }}</span>
          </div>
        </div>
        <div class="text-center mt-8 reveal-3">
          <a href="https://t.me/MelPromoNandoBot" target="_blank" rel="noopener" class="inline-flex items-center gap-1 text-sm font-bold text-gold hover:text-white transition-colors">
            Ver todas as ofertas no Telegram &rarr;
          </a>
        </div>
      </div>
    </section>

    <!-- CTA MID-PAGE -->
    <section class="py-12 px-5 text-center" style="background:linear-gradient(135deg,rgba(212,168,75,.08),rgba(212,168,75,.02))">
      <div class="max-w-md mx-auto">
        <p class="text-lg font-bold text-white mb-2">Ofertas selecionadas para voce.</p>
        <p class="text-sub text-sm mb-6">Nosso bot varre o Mercado Livre 24h por dia. So chega no grupo o que realmente vale a pena.</p>
        <a href="https://t.me/MelPromoNandoBot" target="_blank" rel="noopener" class="btn btn-telegram">
          <svg class="w-5 h-5" fill="#0088cc" viewBox="0 0 24 24"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm4.64 6.8c-.15 1.58-.8 5.42-1.13 7.19-.14.75-.42 1-.68 1.03-.58.05-1.02-.38-1.58-.75-.88-.58-1.38-.94-2.23-1.5-.99-.65-.35-1.01.22-1.59.15-.15 2.71-2.48 2.76-2.69.01-.03.01-.14-.07-.2-.08-.06-.19-.04-.27-.02-.12.02-1.96 1.25-5.54 3.66-.52.36-1 .53-1.42.52-.47-.01-1.37-.26-2.03-.48-.82-.27-1.47-.42-1.41-.88.03-.24.37-.49 1.02-.74 4.01-1.75 6.69-2.9 8.04-3.46 3.83-1.59 4.63-1.87 5.15-1.88.11 0 .37.03.54.17.14.12.18.28.2.45-.01.06.01.24 0 .37z"/></svg>
          ENTRAR NO GRUPO GRATIS
        </a>
      </div>
    </section>

    <!-- O QUE VOCE RECEBE -->
    <section class="py-16 px-5">
      <div class="max-w-xl mx-auto">
        <div class="text-center mb-10 reveal-2">
          <span class="section-badge">O Que Voce Recebe</span>
          <h2 class="text-2xl font-black text-white mb-2">Tudo que o <span class="text-gold">Rei</span> entrega no grupo, de graca.</h2>
          <div class="section-divider"></div>
        </div>
        <div class="grid gap-3 max-w-md mx-auto benefits-grid">
          <div class="bg-card border border-card rounded-2xl p-5 reveal-3" v-for="b in benefits" :key="b.title">
            <div class="text-2xl mb-2" v-html="b.icon"></div>
            <h3 class="text-sm font-bold text-white mb-1">{{ b.title }}</h3>
            <p class="text-xs text-sub leading-relaxed">{{ b.desc }}</p>
          </div>
        </div>
        <div class="text-center mt-8 reveal-3">
          <a href="https://t.me/MelPromoNandoBot" target="_blank" rel="noopener" class="inline-flex items-center gap-1 text-sm font-bold text-gold hover:text-white transition-colors">
            Quero receber essas ofertas gratis &rarr;
          </a>
        </div>
      </div>
    </section>

    <!-- REINADO EM NUMEROS -->
    <section class="py-20 px-5 text-center">
      <div class="reveal-3 mb-12">
        <span class="section-badge">Numeros</span>
        <h2 class="text-2xl font-black text-white mb-2">O Reinado em <span class="text-gold">Numeros</span></h2>
        <div class="section-divider"></div>
      </div>
      <div class="flex gap-6 justify-center flex-wrap max-w-xl mx-auto mb-16 reveal-3">
        <div class="stat-card"><span class="stat-card-num tabular-nums">{{ metrics.posted }}</span><span class="stat-card-lbl">Ofertas Postadas</span><span class="stat-card-sub">Desde o lancamento</span></div>
        <div class="stat-card"><span class="stat-card-num tabular-nums">{{ metrics.members }}</span><span class="stat-card-lbl">Membros no Grupo</span><span class="stat-card-sub">Crescendo todo dia</span></div>
        <div class="stat-card"><span class="stat-card-num tabular-nums">32%</span><span class="stat-card-lbl">Economia Media</span><span class="stat-card-sub">vs. preco original</span></div>
      </div>
      <div class="flex gap-4 justify-center flex-wrap reveal-3">
        <span class="trust"><svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9 12.75L11.25 15 15 9.75m-3-7.036A11.959 11.959 0 013.598 6 11.99 11.99 0 003 9.749c0 5.592 3.824 10.29 9 11.623 5.176-1.332 9-6.03 9-11.622 0-1.31-.21-2.571-.598-3.751h-.152c-3.196 0-6.1-1.248-8.25-3.285z"/></svg>100% Gratis</span>
        <span class="trust"><svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M15.75 6a3.75 3.75 0 11-7.5 0 3.75 3.75 0 017.5 0zM4.501 20.118a7.5 7.5 0 0114.998 0A17.933 17.933 0 0112 21.75c-2.676 0-5.216-.584-7.499-1.632z"/></svg>Link Afiliado Transparente</span>
        <span class="trust"><svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M3 13.125C3 12.504 3.504 12 4.125 12h2.25c.621 0 1.125.504 1.125 1.125v6.75C7.5 20.496 6.996 21 6.375 21h-2.25A1.125 1.125 0 013 19.875v-6.75zM9.75 8.625c0-.621.504-1.125 1.125-1.125h2.25c.621 0 1.125.504 1.125 1.125v11.25c0 .621-.504 1.125-1.125 1.125h-2.25a1.125 1.125 0 01-1.125-1.125V8.625zM16.5 4.125c0-.621.504-1.125 1.125-1.125h2.25C20.496 3 21 3.504 21 4.125v15.75c0 .621-.504 1.125-1.125 1.125h-2.25a1.125 1.125 0 01-1.125-1.125V4.125z"/></svg>Voce Nao Paga Nada a Mais</span>
      </div>
    </section>

    <!-- FAQ -->
    <section class="py-16 px-5">
      <div class="max-w-xl mx-auto">
        <div class="text-center mb-10">
          <span class="section-badge">FAQ</span>
          <h2 class="text-2xl font-black text-white mb-2">Perguntas <span class="text-gold">Frequentes</span></h2>
          <div class="section-divider"></div>
        </div>
        <div class="reveal-3">
          <div class="faq-item" v-for="(faq, i) in faqs" :key="i">
            <button class="faq-q" :class="{ open: faq.open }" @click="faq.open = !faq.open">
              {{ faq.q }}
            </button>
            <div class="faq-a" :class="{ open: faq.open }">{{ faq.a }}</div>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA FINAL -->
    <section class="py-20 px-5 text-center cta-bg">
      <div class="reveal-4">
        <div class="badge badge-red">
          <span class="badge-dot-red"></span>Ofertas Expiram Rapido
        </div>
        <h2 class="text-cta">Sua economia<br><span class="text-gold">comeca aqui.</span></h2>
        <p class="text-sub mb-10 max-w-md mx-auto text-base">
          Milhares de pessoas ja estao economizando com as ofertas que o Rei encontra. Grupo gratuito. Links diretos. Sem pegadinha.
        </p>
        <div class="flex gap-3 justify-center flex-wrap mb-6">
          <a href="https://t.me/MelPromoNandoBot" target="_blank" rel="noopener" class="btn btn-telegram">
            <svg class="w-5 h-5" viewBox="0 0 24 24" fill="currentColor"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm4.64 6.8c-.15 1.58-.8 5.42-1.13 7.19-.14.75-.42 1-.68 1.03-.58.05-1.02-.38-1.58-.75-.88-.58-1.38-.94-2.23-1.5-.99-.65-.35-1.01.22-1.59.15-.15 2.71-2.48 2.76-2.69.01-.03.01-.14-.07-.2-.08-.06-.19-.04-.27-.02-.12.02-1.96 1.25-5.54 3.66-.52.36-1 .53-1.42.52-.47-.01-1.37-.26-2.03-.48-.82-.27-1.47-.42-1.41-.88.03-.24.37-.49 1.02-.74 4.01-1.75 6.69-2.9 8.04-3.46 3.83-1.59 4.63-1.87 5.15-1.88.11 0 .37.03.54.17.14.12.18.28.2.45-.01.06.01.24 0 .37z"/></svg>
            ENTRAR NO TELEGRAM
          </a>
          <a href="https://chat.whatsapp.com/JQ8tNZsTR9BGxJErWUTmEc" target="_blank" rel="noopener" class="btn btn-wpp" aria-label="Entrar no grupo do WhatsApp">
            <svg class="w-5 h-5" viewBox="0 0 24 24" fill="currentColor"><path d="M12.04 2C6.58 2 2.13 6.45 2.13 11.91c0 1.75.46 3.45 1.33 4.95L2.05 22l5.32-1.4c1.44.79 3.07 1.2 4.73 1.2 5.46 0 9.91-4.45 9.91-9.91 0-5.46-4.45-9.89-9.97-9.89zm5.24 14.14c-.22.62-1.27 1.18-1.74 1.25-.47.07-.97.16-1.56-.1-.37-.16-.84-.35-1.44-.68-2.54-1.09-4.2-3.64-4.32-3.81-.13-.17-1.03-1.38-1.03-2.63s.65-1.86.88-2.11c.23-.25.5-.32.67-.32.17 0 .34 0 .49.01.16.01.37-.06.58.44.22.51.73 1.78.79 1.91.06.13.1.29.02.46-.08.17-.13.28-.25.43-.12.15-.26.34-.37.46-.12.12-.24.26-.1.5.14.24.62 1.02 1.33 1.66.91.81 1.68 1.07 1.93 1.19.24.12.38.1.52-.06.14-.16.6-.7.76-.94.16-.24.32-.2.54-.12.22.08 1.39.66 1.63.78.24.12.4.18.46.28.06.1.06.59-.16 1.21z"/></svg>
            ENTRAR NO WHATSAPP
          </a>
        </div>
        <p class="text-xs text-sub3">Links de afiliado podem gerar comissao &middot; Voce nao paga nada a mais</p>
      </div>
    </section>

    <!-- FOOTER -->
    <footer class="footer">
      <span>Rei da Comprinha</span>&copy; 2026 &middot; Transparencia acima de tudo
    </footer>

    <!-- STICKY CTA MOBILE -->
    <div class="cta-sticky">
      <a href="https://t.me/MelPromoNandoBot" target="_blank" rel="noopener" class="btn btn-telegram flex-1 text-center justify-center"            aria-label="Entrar no grupo do Telegram">ENTRAR NO TELEGRAM</a>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted, onUnmounted } from 'vue'

const carrosselTrack = ref(null)
const carrosselRef = ref(null)
let scrollPos = 0
let speed = 0.7
let animFrame
let touchStartX = 0

const ofertas = [
  { id:1, img:'https://http2.mlstatic.com/D_NQ_NP_764877-MLA99508673360_112025-F.webp', nome:'Soundbar 2.1 240W Bluetooth HDMI', de:'R$ 913,33', por:'R$ 549,90', desc:'39% OFF', link:'https://meli.la/2DvnMVZ' },
  { id:2, img:'https://http2.mlstatic.com/D_NQ_NP_807651-MLB73392451315_122023-O.webp', nome:'Tenis Qix Allan Mesquita Casual', de:'R$ 389,99', por:'R$ 241,53', desc:'38% OFF', link:'https://meli.la/1LvdB97' },
  { id:3, img:'https://http2.mlstatic.com/D_NQ_NP_955166-MLB81931889512_022025-O.webp', nome:'Tenis Slip On Casual Confortavel', de:'R$ 74,49', por:'R$ 46,15', desc:'38% OFF', link:'https://meli.la/2gqBRXw' },
  { id:4, img:'https://http2.mlstatic.com/D_NQ_NP_746749-MLB105881775269_012026-O.webp', nome:'Chinelo Coca-Cola Antiderrapante', de:'R$ 78,90', por:'R$ 49,99', desc:'36% OFF', link:'https://meli.la/1T69Z7N' },
  { id:5, img:'https://http2.mlstatic.com/D_NQ_NP_670362-MLA112394939715_052026-F.webp', nome:'Soundbar 2.1 400W Home Theater', de:'R$ 569,69', por:'R$ 370,30', desc:'34% OFF', link:'https://meli.la/2P26vwU' },
  { id:6, img:'https://http2.mlstatic.com/D_NQ_NP_682375-MLA99975151063_112025-F.webp', nome:'Bicicleta Aro 26 Rebaixada 18 Marchas', de:'R$ 939,21', por:'R$ 666,54', desc:'29% OFF', link:'https://meli.la/2Spgzyc' },
  { id:7, img:'https://http2.mlstatic.com/D_NQ_NP_625481-MLB100590029558_122025-O.webp', nome:'Chuteira Society + Meiao + Caneleira', de:'R$ 98,90', por:'R$ 76,75', desc:'22% OFF', link:'https://meli.la/2kYbvAg' },
  { id:8, img:'https://http2.mlstatic.com/D_NQ_NP_662414-MLA96175373155_102025-F.webp', nome:'Tenis Up Puma Geometrico 42', de:'R$ 299,99', por:'R$ 237,39', desc:'20% OFF', link:'https://meli.la/1n55Jq5' },
  { id:9, img:'https://http2.mlstatic.com/D_NQ_NP_865221-MLA95661560248_102025-F.webp', nome:'Tenis Caven 2.0 Puma Liso 40', de:'R$ 449,99', por:'R$ 375,15', desc:'16% OFF', link:'https://meli.la/2YY1tw8' },
  { id:10, img:'https://http2.mlstatic.com/D_NQ_NP_925892-MLA99439725512_112025-F.webp', nome:'Tenis Dynamic Olympikus Casual', de:'R$ 349,99', por:'R$ 299,99', desc:'14% OFF', link:'https://meli.la/2TCcstA' },
]

const carrosselItems = [...ofertas, ...ofertas]

const categorias = [
  { icon:'&#x1F4F1;', name:'Celulares', count:'+120 ofertas' },
  { icon:'&#x1F4BB;', name:'Informatica', count:'+90 ofertas' },
  { icon:'&#x1F3AE;', name:'Games', count:'+65 ofertas' },
  { icon:'&#x1F3E0;', name:'Casa', count:'+80 ofertas' },
  { icon:'&#x1F45F;', name:'Moda', count:'+150 ofertas' },
  { icon:'&#x1F3CB;', name:'Esportes', count:'+70 ofertas' },
  { icon:'&#x1F50A;', name:'TV e Audio', count:'+55 ofertas' },
  { icon:'&#x2699;', name:'Eletrodomesticos', count:'+100 ofertas' },
]

const benefits = [
  { icon:'&#x1F4E1;', title:'Ofertas em Tempo Real', desc:'Nosso bot varre a internet 24h por dia. Oferta boa cai no grupo na hora.' },
  { icon:'&#x1F916;', title:'Tecnologia Propria', desc:'Robo exclusivo feito por nos. Nao depende de copiar grupo alheio.' },
  { icon:'&#x1F4B0;', title:'Zero Custo pra Voce', desc:'Sem assinatura, sem mensalidade. O grupo e 100% gratuito pra sempre.' },
  { icon:'&#x26A1;', title:'Compra em 1 Clique', desc:'Link direto pro Mercado Livre. Ve a oferta, clicou, comprou. Pronto.' },
]

const faqs = reactive([
  { q:'O grupo e gratuito mesmo?', a:'Sim. 100% gratuito. Voce nao paga nada pra entrar e nem pra receber as ofertas. O Rei ganha uma pequena comissao dos links de afiliado quando voce compra — mas voce nao paga nada a mais por isso.', open:false },
  { q:'Como o Rei acha as ofertas?', a:'Nosso bot varre a internet 24 horas por dia, monitorando dezenas de sites e grupos. Ele compara precos, filtra o que realmente vale a pena e descarta ofertas falsas. So chega no grupo o que presta.', open:false },
  { q:'Preciso ter Telegram ou WhatsApp?', a:'O Rei esta nos dois. O app do Telegram e gratuito e leva 30 segundos pra instalar. Funciona em Android, iPhone e ate no computador. Mas se preferir, tambem temos grupo no WhatsApp.', open:false },
  { q:'Os links sao seguros?', a:'Todos os links sao do Mercado Livre, a maior plataforma de e-commerce do Brasil. Voce compra direto no app ou site do Mercado Livre, com toda a seguranca e garantia da plataforma.', open:false },
  { q:'Quantas ofertas sao postadas por dia?', a:'Em media 200 ofertas por dia. O numero varia conforme a disponibilidade do mercado, mas nosso bot trabalha 24h pra voce nao perder nenhuma promocao boa.', open:false },
])

const STORE_KEY = 'rc_metrics'
const metrics = reactive({ offers: 247, members: 3852, posted: 1247 })

function carregarMetrics() {
  try {
    const raw = localStorage.getItem(STORE_KEY)
    if (!raw) return saveMetrics()
    const saved = JSON.parse(raw)
    const hours = Math.max(0, (Date.now() - saved.ts) / 3600000)
    metrics.offers = Math.round(saved.offers * Math.pow(1.008, Math.min(hours, 72))).toLocaleString()
    metrics.members = Math.round(saved.members * Math.pow(1.005, Math.min(hours, 72))).toLocaleString()
    metrics.posted = Math.round(saved.posted * Math.pow(1.006, Math.min(hours, 72))).toLocaleString()
    saveMetrics()
  } catch(e) {}
}

function saveMetrics() {
  try {
    const o = parseInt(metrics.offers.toString().replace(/\D/g,'')) || 247
    const m = parseInt(metrics.members.toString().replace(/\D/g,'')) || 3852
    const p = parseInt(metrics.posted.toString().replace(/\D/g,'')) || 1247
    localStorage.setItem(STORE_KEY, JSON.stringify({ offers:o, members:m, posted:p, ts:Date.now() }))
  } catch(e) {}
}

onMounted(() => {
  carregarMetrics()
  animScroll()
})

function animScroll() {
  scrollPos += speed
  if (carrosselTrack.value) {
    const hw = carrosselTrack.value.scrollWidth / 2
    if (scrollPos >= hw) scrollPos -= hw
    carrosselTrack.value.style.transform = `translateX(-${scrollPos}px)`
  }
  animFrame = requestAnimationFrame(animScroll)
}

function pauseCarrossel() { speed = 0 }
function resumeCarrossel() { speed = 0.7 }
function onTouchStart(e) { touchStartX = e.touches[0].clientX; speed = 0 }
function onTouchEnd(e) { scrollPos += touchStartX - e.changedTouches[0].clientX; speed = 0.7 }

onUnmounted(() => { cancelAnimationFrame(animFrame) })
</script>
