# Amazon-Clone
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Amazon Clone - HTML/CSS/JS</title>
  <style>
    :root{
      --bg:#0f1111; /* Amazon-like dark header */
      --bg-2:#131921;
      --accent:#febd69; /* Amazon search accent */
      --accent-2:#f3a847; 
      --text:#e6e6e6;
      --muted:#ddd;
      --link:#007185;
      --card:#ffffff;
      --card-muted:#fafafa;
      --star:#ffa41c;
      --success:#007600;
    }
    *{box-sizing:border-box}
    body{margin:0;font-family: system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, "Apple Color Emoji","Segoe UI Emoji"; background:#f1f2f4;color:#111}

    /* Header */
    .header{background:var(--bg-2);color:var(--text);}
    .header-top{display:flex;align-items:center;gap:.75rem;padding:.5rem 1rem}
    .logo{display:flex;align-items:center;gap:.4rem;text-decoration:none;color:var(--text);font-weight:700}
    .logo .smile{color:var(--accent)}
    .deliver{display:flex;align-items:center;gap:.4rem;font-size:.85rem;color:#ccc;white-space:nowrap}
    .deliver .pin{opacity:.8}

    .search{flex:1;display:flex;max-width:1000px;margin:0 .5rem}
    .search select{border:none;background:#e6e6e6;padding:.55rem .6rem;border-radius:.3rem 0 0 .3rem}
    .search input{flex:1;border:none;padding:.6rem .7rem;font-size:1rem}
    .search button{border:none;background:var(--accent);padding:.55rem .9rem;border-radius:0 .3rem .3rem 0;cursor:pointer}
    .search button:hover{background:var(--accent-2)}

    .header-links{display:flex;gap:1rem;align-items:center}
    .header-links a{color:var(--text);text-decoration:none;font-size:.9rem;white-space:nowrap}
    .cart{position:relative;display:flex;align-items:center;gap:.25rem}
    .cart-count{position:absolute;top:-8px;left:12px;background:#f08804;color:#111;font-weight:700;border-radius:999px;padding:0 .35rem;font-size:.75rem}

    .header-bottom{background:#232f3e;color:#ddd;display:flex;gap:1rem;align-items:center;padding:.35rem 1rem;overflow:auto}
    .menu-btn{display:none}
    .navlink{color:#ddd;text-decoration:none;font-size:.9rem;white-space:nowrap;padding:.35rem .5rem;border-radius:.25rem}
    .navlink:hover{background:#2f3f50}

    /* Hero */
    .hero{position:relative;background:linear-gradient(180deg,#e3e8ff, #f7f7f7 50%);height:320px;display:grid;place-items:end center;text-align:center}
    .hero .copy{margin-bottom:1rem;background:rgba(255,255,255,.9);padding:.6rem 1rem;border-radius:.5rem;box-shadow:0 10px 20px rgba(0,0,0,.05)}

    /* Layout */
    .container{max-width:1300px;margin:0 auto;padding:1rem}
    .grid{display:grid;grid-template-columns:repeat(4,1fr);gap:1rem}

    /* Card */
    .card{background:var(--card);border-radius:.6rem;box-shadow:0 6px 18px rgba(0,0,0,.06);overflow:hidden;display:flex;flex-direction:column}
    .card .thumb{height:200px;background:#eee;display:grid;place-items:center}
    .card .thumb img{width:100%;height:100%;object-fit:cover}
    .card .body{padding:1rem;display:flex;flex-direction:column;gap:.5rem}
    .card h3{margin:0;font-size:1rem}
    .price{font-size:1.1rem;font-weight:700}
    .old-price{color:#777;text-decoration:line-through;font-weight:400;margin-left:.35rem}
    .badge{display:inline-block;background:#eff5f1;color:var(--success);border:1px solid #cfe3d6;padding:.15rem .4rem;border-radius:.35rem;font-size:.75rem}
    .stars{color:var(--star);font-size:.95rem}
    .cta{display:flex;gap:.5rem;margin-top:.4rem}
    .btn{flex:1;border:1px solid #d5d9d9;border-radius:999px;background:#ffd814;padding:.5rem .75rem;cursor:pointer}
    .btn.secondary{background:#f0f2f2}
    .btn:hover{filter:brightness(.97)}

    /* Category pills + sort/search info */
    .toolbar{display:flex;flex-wrap:wrap;gap:.5rem;align-items:center;margin:1rem 0}
    .pill{border:1px solid #d5d9d9;border-radius:999px;padding:.35rem .75rem;background:#fff;cursor:pointer;font-size:.9rem}
    .pill.active{background:#232f3e;color:#fff;border-color:#232f3e}
    .results-info{margin-left:auto;font-size:.9rem;color:#444}

    /* Footer */
    footer{margin-top:2rem;background:#232f3e;color:#ddd}
    .footer-top{display:grid;grid-template-columns:repeat(4,1fr);gap:1rem;max-width:1200px;margin:0 auto;padding:2rem 1rem}
    .footer-top h4{margin:.2rem 0 .6rem}
    .footer-top a{display:block;color:#ddd;text-decoration:none;font-size:.9rem;margin:.25rem 0}
    .footer-bottom{background:#0f1111;color:#ccc;text-align:center;padding:1rem;font-size:.9rem}

    /* Responsive */
    @media (max-width: 1024px){
      .grid{grid-template-columns:repeat(3,1fr)}
      .deliver{display:none}
    }
    @media (max-width: 768px){
      .search select{display:none}
      .grid{grid-template-columns:repeat(2,1fr)}
      .header-bottom{position:relative}
      .menu-btn{display:inline-flex;align-items:center;gap:.4rem;border:1px solid #2f3f50;padding:.3rem .5rem;border-radius:.3rem;cursor:pointer}
      .nav-scroller{display:none}
      .nav-scroller.open{display:flex}
      .results-info{flex:1 0 100%}
    }
    @media (max-width: 520px){
      .grid{grid-template-columns:1fr}
      .header-links .hide-sm{display:none}
      .hero{height:240px}
      .card .thumb{height:180px}
    }
  </style>
</head>
<body>
  <!-- HEADER -->
  <header class="header">
    <div class="header-top">
      <a class="logo" href="#" aria-label="Home">
        <svg width="28" height="28" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 2a10 10 0 1 0 10 10A10.011 10.011 0 0 0 12 2Zm1 15h-2v-2h2Zm0-4h-2V7h2Z"/></svg>
        <span>amazn<span class="smile">🙂</span></span>
      </a>
      <div class="deliver">
        <span class="pin">📍</span>
        <div>
          <div style="font-size:.75rem;color:#aaa">Deliver to</div>
          <div><strong>India</strong></div>
        </div>
      </div>
      <form class="search" onsubmit="event.preventDefault(); applyFilters();">
        <select id="categorySelect" aria-label="Category">
          <option value="all">All</option>
          <option value="electronics">Electronics</option>
          <option value="fashion">Fashion</option>
          <option value="home">Home</option>
          <option value="books">Books</option>
          <option value="toys">Toys</option>
        </select>
        <input id="searchInput" type="search" placeholder="Search Amazn.in" aria-label="Search" />
        <button type="submit" aria-label="Search">🔍</button>
      </form>
      <nav class="header-links">
        <a class="hide-sm" href="#">Hello, sign in<br><strong>Account & Lists</strong></a>
        <a class="hide-sm" href="#">Returns<br><strong>& Orders</strong></a>
        <a class="cart" href="#" aria-label="Cart">
          <span class="cart-count" id="cartCount">0</span>
          🛒 <span><strong>Cart</strong></span>
        </a>
      </nav>
    </div>

    <div class="header-bottom">
      <button class="menu-btn" onclick="toggleMenu()">☰ All</button>
      <div class="nav-scroller" id="navScroller">
        <a class="navlink" href="#">Fresh</a>
        <a class="navlink" href="#">Amazon miniTV</a>
        <a class="navlink" href="#">Sell</a>
        <a class="navlink" href="#">Best Sellers</a>
        <a class="navlink" href="#">Mobiles</a>
        <a class="navlink" href="#">Customer Service</a>
        <a class="navlink" href="#">Electronics</a>
        <a class="navlink" href="#">Fashion</a>
        <a class="navlink" href="#">Home & Kitchen</a>
        <a class="navlink" href="#">Books</a>
        <a class="navlink" href="#">Toys & Games</a>
      </div>
    </div>
  </header>

  <!-- HERO -->
  <section class="hero">
    <div class="copy">
      <strong>Great Indian Festive Deals</strong> – Up to 70% off | Free delivery with Prime
    </div>
  </section>

  <main class="container">
    <!-- Toolbar: category pills + results count -->
    <div class="toolbar">
      <button class="pill active" data-filter="all" onclick="setCategory(this)">All</button>
      <button class="pill" data-filter="electronics" onclick="setCategory(this)">Electronics</button>
      <button class="pill" data-filter="fashion" onclick="setCategory(this)">Fashion</button>
      <button class="pill" data-filter="home" onclick="setCategory(this)">Home</button>
      <button class="pill" data-filter="books" onclick="setCategory(this)">Books</button>
      <button class="pill" data-filter="toys" onclick="setCategory(this)">Toys</button>
      <div class="results-info" id="resultsInfo">Showing all products</div>
    </div>

    <!-- Product Grid -->
    <div class="grid" id="productGrid"></div>
  </main>

  <footer>
    <div class="footer-top">
      <div>
        <h4>Get to Know Us</h4>
        <a href="#">About Us</a>
        <a href="#">Careers</a>
        <a href="#">Press Releases</a>
        <a href="#">Amazon Science</a>
      </div>
      <div>
        <h4>Connect with Us</h4>
        <a href="#">Facebook</a>
        <a href="#">Twitter</a>
        <a href="#">Instagram</a>
      </div>
      <div>
        <h4>Make Money with Us</h4>
        <a href="#">Sell on Amazon</a>
        <a href="#">Fulfilment by Amazon</a>
        <a href="#">Advertise Your Products</a>
        <a href="#">Amazon Pay on Merchants</a>
      </div>
      <div>
        <h4>Let Us Help You</h4>
        <a href="#">COVID-19 and Amazon</a>
        <a href="#">Your Account</a>
        <a href="#">Returns Centre</a>
        <a href="#">Help</a>
      </div>
    </div>
    <div class="footer-bottom">© 2025 Amazn clone • Built with HTML, CSS & JS</div>
  </footer>

  <script>
    // --- Mock product data ---
    const PRODUCTS = [
      {id:1, title:"Noise Buds VS104 Pro", category:"electronics", price:1799, oldPrice:4999, rating:4.3, reviews:12450, badge:"#1 Best Seller", img:"https://images.unsplash.com/photo-1585386959984-a415522316d0?q=80&w=1200&auto=format&fit=crop"},
      {id:2, title:"Samsung Galaxy M15 5G", category:"electronics", price:12999, oldPrice:15999, rating:4.2, reviews:5231, badge:"Deal", img:"https://images.unsplash.com/photo-1511707171634-5f897ff02aa9?q=80&w=1200&auto=format&fit=crop"},
      {id:3, title:"Cotton Regular Fit T‑Shirt", category:"fashion", price:399, oldPrice:799, rating:4.1, reviews:845, img:"https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?q=80&w=1200&auto=format&fit=crop"},
      {id:4, title:"Stainless Steel Water Bottle", category:"home", price:699, oldPrice:1199, rating:4.4, reviews:2109, img:"https://images.unsplash.com/photo-1540575467063-178a50c2df87?q=80&w=1200&auto=format&fit=crop"},
      {id:5, title:"The Alchemist – Paulo Coelho", category:"books", price:299, oldPrice:499, rating:4.6, reviews:99999, badge:"Amazon's Choice", img:"https://images.unsplash.com/photo-1519681393784-d120267933ba?q=80&w=1200&auto=format&fit=crop"},
      {id:6, title:"LEGO Classic Creative Bricks", category:"toys", price:1499, oldPrice
