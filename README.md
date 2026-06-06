Taqueria · HTML
<!DOCTYPE html>
<html lang="es">
<head>
 <meta charset="UTF-8" />
 <meta name="viewport" content="width=device-width, initial-scale=1.0" />
 <title>El Sabor de México – Taquería</title>
 <link rel="preconnect" href="https://fonts.googleapis.com" />
 <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;900&family=Lato:wght@400;700&display=swap" />
 <style>
   *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
   :root {
     --verde: #006847; --verde-oscuro: #004d34;
     --rojo: #CE1126; --rojo-oscuro: #a50d1e;
     --blanco: #FFFDF5; --dorado: #C8922A;
     --crema: #FFF8E7; --oscuro: #1A0A00;
     --gris: #6B5B4E; --borde: #E8DDD0;
   }
   body { background: var(--blanco); font-family: 'Lato', sans-serif; color: var(--oscuro); }
 
   /* HERO */
   .hero {
     background: linear-gradient(135deg, var(--verde) 0%, var(--verde-oscuro) 50%, var(--rojo) 100%);
     padding: 2.5rem 1rem 3rem; text-align: center; position: relative; overflow: hidden;
   }
   .hero::before {
     content: ''; position: absolute; inset: 0;
     background: repeating-linear-gradient(45deg, rgba(255,255,255,0.03) 0px, rgba(255,255,255,0.03) 1px, transparent 1px, transparent 20px);
     pointer-events: none;
   }
   .hero-badge {
     display: inline-block; background: var(--dorado); color: var(--oscuro);
     font-size: 11px; font-weight: 700; letter-spacing: 3px; text-transform: uppercase;
     padding: 4px 18px; border-radius: 20px; margin-bottom: 1rem;
   }
   .hero h1 {
     font-family: 'Playfair Display', serif; color: #fff;
     font-size: clamp(2rem, 8vw, 3rem); line-height: 1.1; margin-bottom: .5rem;
     text-shadow: 2px 2px 10px rgba(0,0,0,.4);
   }
   .hero > p { color: rgba(255,255,255,.85); font-size: .95rem; margin-bottom: 1.5rem; }
   .lluvia { font-size: 1.8rem; letter-spacing: 8px; opacity: .75; animation: caer 3s ease-in-out infinite; }
   @keyframes caer { 0%,100%{transform:translateY(0)} 50%{transform:translateY(7px)} }
 
   /* NAV PEDIDOS */
   .nav-pedidos {
     background: var(--oscuro); padding: .6rem 1rem;
     display: flex; align-items: center; gap: 10px; overflow-x: auto;
   }
   .nav-pedidos-label {
     color: var(--dorado); font-size: 11px; font-weight: 700; letter-spacing: 2px;
     text-transform: uppercase; white-space: nowrap; margin-right: 4px;
   }
   .nav-pedidos-scroll { display: flex; gap: 8px; align-items: center; flex: 1; overflow-x: auto; }
   .nav-pedidos-scroll::-webkit-scrollbar { height: 3px; }
   .nav-pedidos-scroll::-webkit-scrollbar-thumb { background: var(--dorado); border-radius: 2px; }
   .btn-pedido-guardado {
     background: rgba(255,255,255,.08); border: 1px solid rgba(255,255,255,.2);
     color: rgba(255,255,255,.8); border-radius: 20px; padding: 4px 14px;
     font-size: .78rem; font-weight: 700; cursor: pointer; white-space: nowrap;
     font-family: 'Lato', sans-serif; transition: background .2s, border-color .2s, color .2s;
   }
   .btn-pedido-guardado:hover { background: rgba(255,255,255,.16); color: #fff; border-color: rgba(255,255,255,.4); }
   .btn-pedido-guardado.activo { background: var(--dorado); border-color: var(--dorado); color: var(--oscuro); }
   .btn-nuevo-pedido {
     background: var(--verde); border: none; color: #fff; border-radius: 20px;
     padding: 4px 14px; font-size: .78rem; font-weight: 700; cursor: pointer;
     white-space: nowrap; font-family: 'Lato', sans-serif; transition: background .2s;
   }
   .btn-nuevo-pedido:hover { background: var(--verde-oscuro); }
 
   /* STRIP */
   .strip { display: flex; background: var(--rojo); }
   .strip span {
     flex: 1; text-align: center; padding: .45rem .25rem; color: #fff;
     font-size: 11px; font-weight: 700; letter-spacing: 1px; text-transform: uppercase;
     border-right: .5px solid rgba(255,255,255,.2);
   }
   .strip span:last-child { border-right: none; }
 
   /* SECCIÓN TÍTULO */
   .seccion-titulo { text-align: center; padding: 2rem 1rem 1rem; }
   .seccion-titulo h2 { font-family: 'Playfair Display', serif; font-size: 1.7rem; color: var(--oscuro); }
   .seccion-titulo p { color: var(--gris); font-size: .875rem; margin-top: .3rem; }
 
   /* CARDS */
   .cards-grid {
     display: grid; grid-template-columns: repeat(3,1fr); gap: 12px;
     padding: 0 1rem 2rem; max-width: 700px; margin: 0 auto;
   }
   .card {
     background: var(--blanco); border: 1.5px solid var(--borde); border-radius: 12px;
     padding: 1.25rem 1rem; text-align: center; cursor: pointer;
     transition: transform .2s, border-color .2s, box-shadow .2s;
     position: relative; overflow: hidden; outline: none;
   }
   .card::before {
     content: ''; position: absolute; top: 0; left: 0; right: 0; height: 4px;
     background: linear-gradient(90deg, var(--verde), var(--dorado), var(--rojo));
     opacity: 0; transition: opacity .2s;
   }
   .card:hover, .card:focus { transform: translateY(-3px); border-color: var(--dorado); box-shadow: 0 6px 20px rgba(200,146,42,.2); }
   .card:hover::before, .card:focus::before, .card.activo::before { opacity: 1; }
   .card.activo { border-color: var(--verde); box-shadow: 0 6px 20px rgba(0,104,71,.2); }
   .card-emoji { font-size: 2.3rem; margin-bottom: .5rem; display: block; }
   .card h3 { font-family: 'Playfair Display', serif; font-size: 1.05rem; color: var(--oscuro); margin-bottom: .25rem; }
   .card p { font-size: .75rem; color: var(--gris); }
 
   /* PANELES */
   .panel { max-width: 700px; margin: 0 auto; padding: 0 1rem 2rem; display: none; }
   .panel.visible { display: block; animation: aparecer .3s ease; }
   @keyframes aparecer { from{opacity:0;transform:translateY(10px)} to{opacity:1;transform:translateY(0)} }
   .panel-header {
     background: linear-gradient(135deg, var(--verde), var(--verde-oscuro));
     border-radius: 12px 12px 0 0; padding: 1rem 1.25rem; color: #fff;
     display: flex; align-items: center; gap: 14px;
   }
   .panel-header .icon { font-size: 2rem; }
   .panel-header h3 { font-family: 'Playfair Display', serif; font-size: 1.3rem; margin-bottom: 2px; }
   .panel-header p { font-size: .8rem; opacity: .85; }
   .sabores-lista {
     background: var(--crema); border: 1.5px solid var(--borde);
     border-top: none; border-radius: 0 0 12px 12px; overflow: hidden;
   }
   .sabor-item {
     display: flex; align-items: center; justify-content: space-between;
     padding: .9rem 1.25rem; border-bottom: .5px solid var(--borde); gap: 12px;
     transition: background .15s;
   }
   .sabor-item:last-child { border-bottom: none; }
   .sabor-item:hover { background: rgba(200,146,42,.06); }
   .sabor-info { flex: 1; }
   .sabor-nombre { font-weight: 700; font-size: .9rem; color: var(--oscuro); }
   .sabor-desc { font-size: .75rem; color: var(--gris); margin-top: 2px; }
   .sabor-precio { font-family: 'Playfair Display', serif; font-size: 1.1rem; color: var(--verde); font-weight: 700; min-width: 52px; text-align: right; white-space: nowrap; }
   .btn-add {
     background: var(--rojo); color: #fff; border: none; border-radius: 8px;
     padding: .4rem .8rem; font-size: .8rem; font-weight: 700; cursor: pointer;
     white-space: nowrap; transition: background .2s, transform .15s; font-family: 'Lato', sans-serif;
   }
   .btn-add:hover { background: var(--rojo-oscuro); transform: scale(1.05); }
   .btn-add:active { transform: scale(.97); }
 
   /* CARRITO */
   .carrito { max-width: 700px; margin: 0 auto; padding: 0 1rem 2rem; display: none; }
   .carrito.visible { display: block; animation: aparecer .3s ease; }
   .carrito-header {
     background: var(--oscuro); color: #fff; padding: .9rem 1.25rem;
     border-radius: 12px 12px 0 0; font-family: 'Playfair Display', serif; font-size: 1.15rem;
     display: flex; align-items: center; justify-content: space-between; gap: 10px;
   }
   .carrito-nombre-wrap { display: flex; align-items: center; gap: 8px; flex: 1; }
   .carrito-nombre-input {
     background: rgba(255,255,255,.12); border: 1px solid rgba(255,255,255,.25);
     color: #fff; border-radius: 8px; padding: 4px 10px; font-size: .85rem;
     font-family: 'Lato', sans-serif; font-weight: 700; width: 160px; outline: none;
   }
   .carrito-nombre-input::placeholder { color: rgba(255,255,255,.45); }
   .carrito-nombre-input:focus { border-color: var(--dorado); }
   .btn-guardar-pedido {
     background: var(--dorado); border: none; color: var(--oscuro); border-radius: 8px;
     padding: 5px 14px; font-size: .78rem; font-weight: 700; cursor: pointer;
     font-family: 'Lato', sans-serif; transition: opacity .2s; white-space: nowrap;
   }
   .btn-guardar-pedido:hover { opacity: .85; }
   .carrito-items { background: var(--crema); border: 1.5px solid var(--borde); border-top: none; }
   .carrito-item {
     display: flex; align-items: center; justify-content: space-between;
     padding: .75rem 1.25rem; border-bottom: .5px solid var(--borde); gap: 10px;
   }
   .carrito-item:last-child { border-bottom: none; }
   .item-info { flex: 1; }
   .item-nombre { font-size: .875rem; font-weight: 700; color: var(--oscuro); }
   .item-cat { font-size: .75rem; color: var(--gris); }
   .item-precio { font-family: 'Playfair Display', serif; color: var(--verde); font-weight: 700; font-size: 1rem; min-width: 52px; text-align: right; }
   .carrito-vacio { padding: 1.5rem; text-align: center; color: var(--gris); font-size: .875rem; font-style: italic; }
   .btn-quitar {
     background: none; border: 1.5px solid var(--rojo); color: var(--rojo);
     border-radius: 6px; padding: 3px 10px; font-size: .75rem; font-weight: 700;
     cursor: pointer; transition: background .2s, color .2s; white-space: nowrap;
     font-family: 'Lato', sans-serif;
   }
   .btn-quitar:hover { background: var(--rojo); color: #fff; }
   .carrito-footer {
     background: var(--oscuro); border-radius: 0 0 12px 12px;
     padding: 1rem 1.25rem; display: flex; align-items: center; justify-content: space-between;
   }
   .total-label { color: rgba(255,255,255,.65); font-size: .75rem; text-transform: uppercase; letter-spacing: 1.5px; margin-bottom: 2px; }
   .total-monto { font-family: 'Playfair Display', serif; color: var(--dorado); font-size: 1.7rem; font-weight: 700; }
   .btn-limpiar {
     background: none; border: 1.5px solid rgba(255,255,255,.3); color: rgba(255,255,255,.7);
     border-radius: 8px; padding: .45rem 1rem; font-size: .8rem; cursor: pointer;
     transition: border-color .2s, color .2s; font-family: 'Lato', sans-serif; font-weight: 700;
   }
   .btn-limpiar:hover { border-color: #fff; color: #fff; }
 
   /* MODAL PEDIDO GUARDADO */
   .modal-overlay {
     display: none; position: fixed; inset: 0;
     background: rgba(0,0,0,.55); z-index: 100;
     align-items: center; justify-content: center; padding: 1rem;
   }
   .modal-overlay.visible { display: flex; }
   .modal {
     background: var(--blanco); border-radius: 16px; width: 100%; max-width: 480px;
     overflow: hidden; animation: aparecer .25s ease;
   }
   .modal-header {
     background: linear-gradient(135deg, var(--verde), var(--verde-oscuro));
     padding: 1rem 1.25rem; color: #fff; display: flex; align-items: center; justify-content: space-between;
   }
   .modal-header h3 { font-family: 'Playfair Display', serif; font-size: 1.2rem; }
   .modal-header span { font-size: .8rem; opacity: .8; }
   .btn-cerrar-modal {
     background: none; border: none; color: #fff; font-size: 1.3rem; cursor: pointer; line-height: 1;
   }
   .modal-items { max-height: 320px; overflow-y: auto; background: var(--crema); border-bottom: 1px solid var(--borde); }
   .modal-item {
     display: flex; align-items: center; justify-content: space-between;
     padding: .75rem 1.25rem; border-bottom: .5px solid var(--borde); gap: 10px;
   }
   .modal-item:last-child { border-bottom: none; }
   .modal-item-info { flex: 1; }
   .modal-item-nombre { font-size: .875rem; font-weight: 700; color: var(--oscuro); }
   .modal-item-cat { font-size: .75rem; color: var(--gris); }
   .modal-item-precio { font-family: 'Playfair Display', serif; color: var(--verde); font-weight: 700; font-size: 1rem; min-width: 48px; text-align: right; }
   .modal-footer {
     padding: 1rem 1.25rem; background: var(--oscuro);
     display: flex; align-items: center; justify-content: space-between; gap: 10px;
   }
   .modal-total-label { color: rgba(255,255,255,.65); font-size: .75rem; text-transform: uppercase; letter-spacing: 1px; }
   .modal-total-monto { font-family: 'Playfair Display', serif; color: var(--dorado); font-size: 1.4rem; font-weight: 700; }
   .modal-actions { display: flex; gap: 8px; }
   .btn-modal-cargar {
     background: var(--verde); border: none; color: #fff; border-radius: 8px;
     padding: .45rem 1rem; font-size: .8rem; font-weight: 700; cursor: pointer;
     font-family: 'Lato', sans-serif; transition: background .2s;
   }
   .btn-modal-cargar:hover { background: var(--verde-oscuro); }
   .btn-modal-eliminar {
     background: none; border: 1.5px solid var(--rojo); color: var(--rojo); border-radius: 8px;
     padding: .45rem 1rem; font-size: .8rem; font-weight: 700; cursor: pointer;
     font-family: 'Lato', sans-serif; transition: background .2s, color .2s;
   }
   .btn-modal-eliminar:hover { background: var(--rojo); color: #fff; }
 
   /* TOAST */
   .toast {
     position: fixed; bottom: 1.5rem; left: 50%; transform: translateX(-50%) translateY(80px);
     background: var(--oscuro); color: #fff; padding: .6rem 1.25rem; border-radius: 20px;
     font-size: .85rem; font-weight: 700; z-index: 200; transition: transform .3s ease;
     border-left: 4px solid var(--dorado); white-space: nowrap;
   }
   .toast.show { transform: translateX(-50%) translateY(0); }
 
   /* FOOTER */
   .footer-mx { text-align: center; padding: 1.5rem 1rem; background: var(--verde); color: rgba(255,255,255,.8); font-size: .85rem; }
   .footer-mx span { color: var(--dorado); font-weight: 700; }
 
   @media (max-width: 480px) {
     .cards-grid { gap: 8px; }
     .card { padding: 1rem .5rem; }
     .card-emoji { font-size: 1.8rem; }
     .strip span { font-size: 9px; letter-spacing: 0; }
     .carrito-nombre-input { width: 110px; }
   }
 </style>
</head>
<body>
 
 <header class="hero">
   <div class="hero-badge">Desde 1985 · Jalisco, México</div>
   <h1>El Sabor<br>de México</h1>
   <p>Taquería tradicional · Hecho con amor</p>
   <div class="lluvia">🧅 🌿 🌶️</div>
 </header>
 
 <!-- BARRA DE PEDIDOS GUARDADOS -->
 <nav class="nav-pedidos" id="nav-pedidos">
   <span class="nav-pedidos-label">📋 Pedidos</span>
   <div class="nav-pedidos-scroll" id="pedidos-scroll">
     <!-- se genera con JS -->
   </div>
   <button class="btn-nuevo-pedido" onclick="nuevoPedido()">+ Nuevo</button>
 </nav>
 
 <div class="strip">
   <span>Cebolla siempre</span>
   <span>Cilantro fresco</span>
   <span>Salsa roja</span>
   <span>Salsa verde</span>
 </div>
 
 <section class="seccion-titulo">
   <h2>¿Qué se te antoja?</h2>
   <p>Elige una categoría para ver los sabores disponibles</p>
 </section>
 
 <div class="cards-grid">
   <div class="card" id="card-tacos" tabindex="0" onclick="abrirCategoria('tacos')" onkeydown="teclaCard(event,'tacos')">
     <span class="card-emoji">🌮</span>
     <h3>Tacos</h3>
     <p>Los clásicos de siempre</p>
   </div>
   <div class="card" id="card-aguas" tabindex="0" onclick="abrirCategoria('aguas')" onkeydown="teclaCard(event,'aguas')">
     <span class="card-emoji">🥤</span>
     <h3>Aguas</h3>
     <p>Frescas y naturales</p>
   </div>
   <div class="card" id="card-quesadillas" tabindex="0" onclick="abrirCategoria('quesadillas')" onkeydown="teclaCard(event,'quesadillas')">
     <span class="card-emoji">🧀</span>
     <h3>Quesadillas</h3>
     <p>Gratinadas al comal</p>
   </div>
 </div>
 
 <div class="panel" id="panel-tacos">
   <div class="panel-header">
     <span class="icon">🌮</span>
     <div><h3>Tacos</h3><p>Tortilla de maíz · cebolla · cilantro · salsa al gusto</p></div>
   </div>
   <div class="sabores-lista" id="lista-tacos"></div>
 </div>
 
 <div class="panel" id="panel-aguas">
   <div class="panel-header">
     <span class="icon">🥤</span>
     <div><h3>Aguas Frescas</h3><p>Preparadas en casa · sin conservadores</p></div>
   </div>
   <div class="sabores-lista" id="lista-aguas"></div>
 </div>
 
 <div class="panel" id="panel-quesadillas">
   <div class="panel-header">
     <span class="icon">🧀</span>
     <div><h3>Quesadillas</h3><p>Queso Oaxaca derretido · comal de barro</p></div>
   </div>
   <div class="sabores-lista" id="lista-quesadillas"></div>
 </div>
 
 <!-- CARRITO -->
 <section class="carrito" id="carrito">
   <div class="carrito-header">
     <div class="carrito-nombre-wrap">
       🛒
       <input class="carrito-nombre-input" id="carrito-nombre" type="text" placeholder="Nombre del pedido" maxlength="30" />
     </div>
     <button class="btn-guardar-pedido" onclick="guardarPedido()">💾 Guardar</button>
   </div>
   <div class="carrito-items" id="carrito-items">
     <div class="carrito-vacio">Aún no has agregado nada</div>
   </div>
   <div class="carrito-footer">
     <div>
       <div class="total-label">Total</div>
       <div class="total-monto" id="total-monto">$0.00</div>
     </div>
     <button class="btn-limpiar" onclick="limpiarCarrito()">Vaciar pedido</button>
   </div>
 </section>
 
 <!-- MODAL VER PEDIDO GUARDADO -->
 <div class="modal-overlay" id="modal-overlay" onclick="cerrarModal(event)">
   <div class="modal" id="modal">
     <div class="modal-header">
       <div>
         <h3 id="modal-titulo">Pedido</h3>
         <span id="modal-items-count"></span>
       </div>
       <button class="btn-cerrar-modal" onclick="cerrarModalDirecto()">✕</button>
     </div>
     <div class="modal-items" id="modal-items"></div>
     <div class="modal-footer">
       <div>
         <div class="modal-total-label">Total</div>
         <div class="modal-total-monto" id="modal-total"></div>
       </div>
       <div class="modal-actions">
         <button class="btn-modal-cargar" onclick="cargarPedido()">✏️ Modificar</button>
         <button class="btn-modal-eliminar" onclick="eliminarPedido()">🗑 Eliminar</button>
       </div>
     </div>
   </div>
 </div>
 
 <!-- TOAST -->
 <div class="toast" id="toast"></div>
 
 <footer class="footer-mx">
   Hecho con ❤️ en <span>México</span> · Cebolla y cilantro siempre incluidos
 </footer>
 
 <script>
   var menu = {
     tacos: [
       { nombre: 'Taco de Pastor',   desc: 'Piña, adobo rojo, marinación 24h',    precio: 22 },
       { nombre: 'Taco de Chorizo',  desc: 'Chorizo casero estilo Jalisco',         precio: 22 },
       { nombre: 'Taco de Bistec',   desc: 'Res a la plancha con especias',         precio: 25 },
       { nombre: 'Taco de Pollo',    desc: 'Pollo marinado en chipotle',            precio: 22 },
       { nombre: 'Taco de Suadero',  desc: 'Res cocida lentamente, muy jugosa',     precio: 24 },
     ],
     aguas: [
       { nombre: 'Agua de Jamaica',   desc: 'Flor de Jamaica con canela',           precio: 18 },
       { nombre: 'Agua de Horchata',  desc: 'Arroz, canela y vainilla',             precio: 18 },
       { nombre: 'Agua de Limón',     desc: 'Limón fresco con hojitas de menta',    precio: 15 },
       { nombre: 'Agua de Tamarindo', desc: 'Tamarindo natural con poca azúcar',    precio: 18 },
     ],
     quesadillas: [
       { nombre: 'Quesadilla de Pastor',    desc: 'Queso Oaxaca + pastor + salsa verde', precio: 38 },
       { nombre: 'Quesadilla de Chorizo',   desc: 'Queso derretido + chorizo picante',   precio: 38 },
       { nombre: 'Quesadilla de Flor',      desc: 'Flor de calabaza + epazote + queso',  precio: 35 },
       { nombre: 'Quesadilla Sincronizada', desc: 'Doble tortilla + jamón + queso',      precio: 40 },
     ],
   };
 
   var etiquetas = { tacos: 'Taco', aguas: 'Agua', quesadillas: 'Quesadilla' };
   var carrito = [];
   var panelActivo = null;
   var pedidosGuardados = JSON.parse(localStorage.getItem('taqueria_pedidos') || '[]');
   var pedidoAbierto = null; // id del pedido que está en el modal
 
   /* ---- RENDER LISTAS ---- */
   function renderLista(cat) {
     var el = document.getElementById('lista-' + cat);
     el.innerHTML = '';
     menu[cat].forEach(function(item, idx) {
       var div = document.createElement('div');
       div.className = 'sabor-item';
       div.innerHTML =
         '<div class="sabor-info">' +
           '<div class="sabor-nombre">' + item.nombre + '</div>' +
           '<div class="sabor-desc">' + item.desc + '</div>' +
         '</div>' +
         '<div class="sabor-precio">$' + item.precio + '</div>' +
         '<button class="btn-add" onclick="agregarItem(\'' + cat + '\',' + idx + ')">+ Agregar</button>';
       el.appendChild(div);
     });
   }
   Object.keys(menu).forEach(renderLista);
 
   /* ---- CATEGORÍAS ---- */
   function abrirCategoria(cat) {
     if (panelActivo === cat) {
       document.getElementById('panel-' + cat).classList.remove('visible');
       document.getElementById('card-'  + cat).classList.remove('activo');
       panelActivo = null;
       return;
     }
     if (panelActivo) {
       document.getElementById('panel-' + panelActivo).classList.remove('visible');
       document.getElementById('card-'  + panelActivo).classList.remove('activo');
     }
     document.getElementById('panel-' + cat).classList.add('visible');
     document.getElementById('card-'  + cat).classList.add('activo');
     panelActivo = cat;
     document.getElementById('panel-' + cat).scrollIntoView({ behavior: 'smooth', block: 'nearest' });
   }
 
   function teclaCard(e, cat) {
     if (e.key === 'Enter' || e.key === ' ') { e.preventDefault(); abrirCategoria(cat); }
   }
 
   /* ---- CARRITO ---- */
   function agregarItem(cat, idx) {
     carrito.push({ nombre: menu[cat][idx].nombre, desc: menu[cat][idx].desc, precio: menu[cat][idx].precio, cat: cat, id: Date.now() + Math.random() });
     actualizarCarrito();
     document.getElementById('carrito').classList.add('visible');
   }
 
   function quitarItem(id) {
     carrito = carrito.filter(function(i) { return i.id !== id; });
     actualizarCarrito();
     if (!carrito.length) {
       setTimeout(function() {
         if (!carrito.length) document.getElementById('carrito').classList.remove('visible');
       }, 200);
     }
   }
 
   function limpiarCarrito() {
     carrito = [];
     document.getElementById('carrito-nombre').value = '';
     actualizarCarrito();
     document.getElementById('carrito').classList.remove('visible');
   }
 
   function actualizarCarrito() {
     var cont = document.getElementById('carrito-items');
     if (!carrito.length) {
       cont.innerHTML = '<div class="carrito-vacio">Aún no has agregado nada</div>';
       document.getElementById('total-monto').textContent = '$0.00';
       return;
     }
     var html = '';
     carrito.forEach(function(item) {
       html +=
         '<div class="carrito-item">' +
           '<div class="item-info">' +
             '<div class="item-nombre">' + item.nombre + '</div>' +
             '<div class="item-cat">' + etiquetas[item.cat] + '</div>' +
           '</div>' +
           '<div class="item-precio">$' + item.precio + '</div>' +
           '<button class="btn-quitar" onclick="quitarItem(' + item.id + ')">Quitar</button>' +
         '</div>';
     });
     cont.innerHTML = html;
     var total = carrito.reduce(function(s, i) { return s + i.precio; }, 0);
     document.getElementById('total-monto').textContent = '$' + total.toFixed(2);
   }
 
   /* ---- GUARDAR PEDIDO ---- */
   function guardarPedido() {
     if (!carrito.length) { mostrarToast('Agrega algo al pedido primero 😅'); return; }
     var nombre = document.getElementById('carrito-nombre').value.trim();
     if (!nombre) { mostrarToast('Ponle un nombre al pedido 📝'); document.getElementById('carrito-nombre').focus(); return; }
 
     // Si ya existe un pedido con ese id (modo edición), actualizarlo
     var existeIdx = pedidosGuardados.findIndex(function(p) { return p.nombre === nombre; });
     var pedido = {
       id: Date.now(),
       nombre: nombre,
       items: JSON.parse(JSON.stringify(carrito)),
       fecha: new Date().toLocaleDateString('es-MX', { day:'2-digit', month:'short' })
     };
     if (existeIdx >= 0) {
       pedido.id = pedidosGuardados[existeIdx].id;
       pedidosGuardados[existeIdx] = pedido;
       mostrarToast('Pedido "' + nombre + '" actualizado ✅');
     } else {
       pedidosGuardados.push(pedido);
       mostrarToast('Pedido "' + nombre + '" guardado ✅');
     }
     localStorage.setItem('taqueria_pedidos', JSON.stringify(pedidosGuardados));
     renderNavPedidos();
   }
 
   /* ---- NUEVO PEDIDO ---- */
   function nuevoPedido() {
     limpiarCarrito();
     document.getElementById('carrito-nombre').value = '';
     mostrarToast('Nuevo pedido listo 🌮');
   }
 
   /* ---- NAV PEDIDOS ---- */
   function renderNavPedidos() {
     var scroll = document.getElementById('pedidos-scroll');
     scroll.innerHTML = '';
     if (!pedidosGuardados.length) {
       scroll.innerHTML = '<span style="color:rgba(255,255,255,.35);font-size:.78rem;font-style:italic;">Sin pedidos guardados</span>';
       return;
     }
     pedidosGuardados.forEach(function(p) {
       var btn = document.createElement('button');
       btn.className = 'btn-pedido-guardado';
       btn.textContent = p.nombre;
       btn.onclick = function() { abrirModalPedido(p.id); };
       scroll.appendChild(btn);
     });
   }
   renderNavPedidos();
 
   /* ---- MODAL ---- */
   function abrirModalPedido(id) {
     var p = pedidosGuardados.find(function(x) { return x.id === id; });
     if (!p) return;
     pedidoAbierto = id;
     document.getElementById('modal-titulo').textContent = p.nombre;
     document.getElementById('modal-items-count').textContent = p.items.length + ' producto' + (p.items.length !== 1 ? 's' : '') + ' · ' + p.fecha;
     var html = '';
     p.items.forEach(function(item) {
       html +=
         '<div class="modal-item">' +
           '<div class="modal-item-info">' +
             '<div class="modal-item-nombre">' + item.nombre + '</div>' +
             '<div class="modal-item-cat">' + etiquetas[item.cat] + '</div>' +
           '</div>' +
           '<div class="modal-item-precio">$' + item.precio + '</div>' +
         '</div>';
     });
     document.getElementById('modal-items').innerHTML = html;
     var total = p.items.reduce(function(s, i) { return s + i.precio; }, 0);
     document.getElementById('modal-total').textContent = '$' + total.toFixed(2);
     document.getElementById('modal-overlay').classList.add('visible');
   }
 
   function cerrarModal(e) {
     if (e.target === document.getElementById('modal-overlay')) cerrarModalDirecto();
   }
 
   function cerrarModalDirecto() {
     document.getElementById('modal-overlay').classList.remove('visible');
     pedidoAbierto = null;
   }
 
   function cargarPedido() {
     var p = pedidosGuardados.find(function(x) { return x.id === pedidoAbierto; });
     if (!p) return;
     carrito = JSON.parse(JSON.stringify(p.items));
     // restaurar ids únicos para que quitar funcione
     carrito.forEach(function(i) { i.id = Date.now() + Math.random(); });
     document.getElementById('carrito-nombre').value = p.nombre;
     actualizarCarrito();
     document.getElementById('carrito').classList.add('visible');
     cerrarModalDirecto();
     mostrarToast('Pedido "' + p.nombre + '" cargado para modificar ✏️');
     document.getElementById('carrito').scrollIntoView({ behavior: 'smooth', block: 'nearest' });
   }
 
   function eliminarPedido() {
     var p = pedidosGuardados.find(function(x) { return x.id === pedidoAbierto; });
     if (!p) return;
     pedidosGuardados = pedidosGuardados.filter(function(x) { return x.id !== pedidoAbierto; });
     localStorage.setItem('taqueria_pedidos', JSON.stringify(pedidosGuardados));
     renderNavPedidos();
     cerrarModalDirecto();
     mostrarToast('Pedido eliminado 🗑');
   }
 
   /* ---- TOAST ---- */
   var toastTimer;
   function mostrarToast(msg) {
     var t = document.getElementById('toast');
     t.textContent = msg;
     t.classList.add('show');
     clearTimeout(toastTimer);
     toastTimer = setTimeout(function() { t.classList.remove('show'); }, 2500);
   }
 </script>
</body>
</html>
