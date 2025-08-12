# Create a simple, production-ready static website scaffold for an online sweepstakes-style casino.

# It includes: index.html, games.html, promos.html, how-it-works.html, responsible-gaming.html,

# terms.html, privacy.html, contact.html, /assets/css, /assets/js, and placeholder images.

# Then, it zips the folder for download.



import os, textwrap, zipfile, json, pathlib, datetime



site_root = "/mnt/data/texas_slots_casino_sweep_site"

assets_css = f"{site_root}/assets/css"

assets_js = f"{site_root}/assets/js"

assets_img = f"{site_root}/assets/img"

os.makedirs(assets_css, exist_ok=True)

os.makedirs(assets_js, exist_ok=True)

os.makedirs(assets_img, exist_ok=True)



brand = "Texas Slots Casino Sweep"

primary_color = "#6e2bff"

dark_bg = "#0c0e14"



# ---------- Create placeholder SVG images ----------

def write_svg(path, title):

    svg = f'''<svg xmlns="http://www.w3.org/2000/svg" width="1200" height="630" viewBox="0 0 1200 630">

  <defs>

    <linearGradient id="g" x1="0" x2="1">

      <stop offset="0%" stop-color="{primary_color}"/>

      <stop offset="100%" stop-color="#14b8a6"/>

    </linearGradient>

  </defs>

  <rect width="1200" height="630" fill="{dark_bg}"/>

  <circle cx="950" cy="200" r="180" fill="url(#g)" opacity="0.25"/>

  <rect x="60" y="60" width="1080" height="510" rx="24" ry="24" fill="none" stroke="url(#g)" stroke-width="6"/>

  <text x="100" y="200" font-family="Segoe UI, Arial, sans-serif" font-size="64" fill="#fff" font-weight="700">{brand}</text>

  <text x="100" y="280" font-family="Segoe UI, Arial, sans-serif" font-size="42" fill="#a3a3a3">{title}</text>

  <text x="100" y="360" font-family="Segoe UI, Arial, sans-serif" font-size="28" fill="#d4d4d4">Placeholder artwork</text>

</svg>'''

    with open(path, "w") as f:

        f.write(svg)



write_svg(f"{assets_img}/hero.svg", "Play. Win. Celebrate.")

write_svg(f"{assets_img}/games.svg", "Games")

write_svg(f"{assets_img}/promos.svg", "Promotions")

write_svg(f"{assets_img}/hw.svg", "How it works")

write_svg(f"{assets_img}/rg.svg", "Responsible Gaming")

write_svg(f"{assets_img}/logo.svg", "Logo")



# ---------- Shared head & header/footer components ----------

head = f"""<!doctype html>

<html lang="en">

<head>

  <meta charset="utf-8">

  <meta name="viewport" content="width=device-width, initial-scale=1">

  <title>{brand}</title>

  <meta name="description" content="A sweepstakes-style online entertainment site. Play for fun with virtual coins. No purchase necessary.">

  <link rel="preload" href="/assets/css/styles.css" as="style">

  <link rel="stylesheet" href="/assets/css/styles.css">

  <link rel="icon" href="/assets/img/logo.svg" type="image/svg+xml">

</head>

<body>

<div class="age-gate" id="ageGate" aria-hidden="true" role="dialog" aria-modal="true">

  <div class="age-card" role="document">

    <h2>Are you 18 or older?</h2>

    <p>By entering, you confirm you are at least 18 years old and agree to our <a href="/terms.html">Terms</a> & <a href="/privacy.html">Privacy</a>.</p>

    <div class="age-actions">

      <button id="enterBtn" class="btn primary">Yes, Enter</button>

      <button id="leaveBtn" class="btn">No, Exit</button>

    </div>

  </div>

</div>

<header class="site-header">

  <a href="/index.html" class="logo">

    <img src="/assets/img/logo.svg" alt="{brand} logo" width="36" height="36">

    <span>{brand}</span>

  </a>

  <nav class="nav">

    <a href="/games.html">Games</a>

    <a href="/promos.html">Promos</a>

    <a href="/how-it-works.html">How it works</a>

    <a href="/responsible-gaming.html">Responsible</a>

    <a href="/contact.html">Contact</a>

  </nav>

  <div class="cta">

    <a class="btn ghost" href="/how-it-works.html">Learn</a>

    <a class="btn primary" href="#create-account" id="createAccountTop">Create account</a>

  </div>

</header>

<main>

"""



footer = f"""

</main>

<footer class="site-footer">

  <div class="f-grid">

    <div>

      <strong>{brand}</strong>

      <p class="muted">Entertainment only. Sweepstakes-style promotional games. No purchase necessary. Void where prohibited.</p>

    </div>

    <div class="f-links">

      <a href="/terms.html">Terms</a>

      <a href="/privacy.html">Privacy</a>

      <a href="/responsible-gaming.html">Responsible Gaming</a>

      <a href="/contact.html">Contact</a>

    </div>

  </div>

  <p class="fine">© {datetime.datetime.now().year} {brand}. All rights reserved.</p>

</footer>

<script src="/assets/js/app.js"></script>

</body>

</html>

"""



# ---------- Pages ----------

index_html = head + f"""

<section class="hero">

  <div class="hero-content">

    <h1>Play. Win. Celebrate.</h1>

    <p>Join our sweepstakes-style games. Collect virtual Coins, join giveaways, and have fun. No purchase necessary.</p>

    <div class="actions">

      <a class="btn primary" href="#create-account" id="createAccountHero">Create account</a>

      <a class="btn" href="/how-it-works.html">How it works</a>

    </div>

  </div>

  <img class="hero-img" src="/assets/img/hero.svg" alt="Casino-style neon shapes">

</section>



<section class="pillars">

  <article>

    <h3>Fair play</h3>

    <p>Randomized outcomes with independent seed, displayed odds, and transparent rules for each game.</p>

  </article>

  <article>

    <h3>Giveaways</h3>

    <p>Enter no-cost sweepstakes with free entry methods. Winners posted on our Promos page.</p>

  </article>

  <article>

    <h3>Responsible</h3>

    <p>Play limits, cool‑offs, and resources built-in. We put your wellbeing first.</p>

  </article>

</section>



<section class="featured">

  <header class="section-head">

    <h2>Featured games</h2>

    <a class="link" href="/games.html">See all</a>

  </header>

  <div class="cards">

    <a href="/games.html#lucky-7s" class="card">

      <img src="/assets/img/games.svg" alt="" loading="lazy">

      <div><h4>Lucky 7s</h4><p class="muted">Classic fruit reels</p></div>

    </a>

    <a href="/games.html#pirate-plunder" class="card">

      <img src="/assets/img/games.svg" alt="" loading="lazy">

      <div><h4>Pirate Plunder</h4><p class="muted">Bonus chests & cascades</p></div>

    </a>

    <a href="/games.html#blackjack-lite" class="card">

      <img src="/assets/img/games.svg" alt="" loading="lazy">

      <div><h4>Blackjack Lite</h4><p class="muted">Heads‑up to 21</p></div>

    </a>

  </div>

</section>



<section id="create-account" class="signup">

  <h2>Create a free account</h2>

  <form class="card form" onsubmit="return false" aria-describedby="acctHelp">

    <div class="two">

      <label>Email<input required type="email" placeholder="you@email.com"></label>

      <label>Username<input required type="text" minlength="3" maxlength="20" placeholder="YourNickname"></label>

    </div>

    <div class="two">

      <label>Password<input required type="password" minlength="8" placeholder="••••••••"></label>

      <label>Referral code (optional)<input type="text" placeholder="ABC123"></label>

    </div>

    <label class="checkbox"><input type="checkbox" required> I confirm I am 18+ and agree to the <a href="/terms.html">Terms</a> & <a href="/privacy.html">Privacy</a>.</label>

    <button class="btn primary" id="createAccountSubmit">Create account</button>

    <p id="acctHelp" class="fine">This is a demo form. Hook it to your backend/CRM later.</p>

  </form>

</section>

""" + footer



games_html = head + f"""

<section class="page-head">

  <h1>Games</h1>

  <p class="muted">All titles are for entertainment and sweepstakes‑style promotions only.</p>

</section>

<section class="cards grid-3">

  <article id="lucky-7s" class="card">

    <img src="/assets/img/games.svg" alt="Lucky 7s artwork">

    <h3>Lucky 7s</h3>

    <p>3x5 reels, 20 lines, RTP disclosed in game rules. Wilds expand on win.</p>

    <button class="btn">Play demo</button>

  </article>

  <article id="pirate-plunder" class="card">

    <img src="/assets/img/games.svg" alt="Pirate Plunder artwork">

    <h3>Pirate Plunder</h3>

    <p>Symbol cascades, multipliers, and treasure bonus. RTP disclosed in rules.</p>

    <button class="btn">Play demo</button>

  </article>

  <article id="blackjack-lite" class="card">

    <img src="/assets/img/games.svg" alt="Blackjack Lite artwork">

    <h3>Blackjack Lite</h3>

    <p>Single-deck heads‑up with standard Vegas rules. House edge disclosed in rules.</p>

    <button class="btn
