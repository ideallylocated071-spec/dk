```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<title>Will You Be Mine?</title>
<meta name="description" content="A little something I made for you.">

<!-- Open Graph -->
<meta property="og:title" content="Will You Be Mine?">
<meta property="og:description" content="A little something I made for you.">
<meta property="og:type" content="website">
<meta property="og:image" content="assets/images/og-cover.jpg">

<!-- Twitter -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Will You Be Mine?">
<meta name="twitter:description" content="A little something I made for you.">

<meta name="robots" content="noindex, nofollow">
<link rel="icon" href="assets/icons/favicon.png">
<link rel="manifest" href="manifest.json">
<meta name="theme-color" content="#140b1a">

<!-- Fonts -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,500;0,600;1,500&family=Jost:wght@300;400;500;600&family=Caveat:wght@500;600;700&display=swap" rel="stylesheet">

<!-- Icons -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">

<!-- Vendor -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js" defer></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js" defer></script>
<script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.9.2/dist/confetti.browser.min.js" defer></script>

<link rel="stylesheet" href="style.css">
</head>
<body>

<!-- ============ ACCESSIBILITY: SKIP LINK ============ -->
<a class="skip-link" href="#proposal">Skip to proposal</a>

<!-- ============ AMBIENT CANVAS LAYERS (fireflies / sparkles / trails) ============ -->
<canvas id="fx-canvas" aria-hidden="true"></canvas>
<div id="cursor-glow" aria-hidden="true"></div>

<!-- ============ 1. LOADING SCREEN ============ -->
<section id="loader" aria-label="Loading">
  <div class="loader-inner">
    <div class="loader-logo" aria-hidden="true">
      <svg viewBox="0 0 100 100" class="logo-heart">
        <path d="M50 88 C20 65 4 45 4 27 C4 12 15 2 29 2 C39 2 47 8 50 17 C53 8 61 2 71 2 C85 2 96 12 96 27 C96 45 80 65 50 88 Z"/>
      </svg>
    </div>
    <div class="loader-percent" id="loader-percent">0%</div>
    <div class="loader-bar"><div class="loader-bar-fill" id="loader-fill"></div></div>
    <p class="loader-label">preparing something for you</p>
  </div>
  <div class="loader-hearts" aria-hidden="true"></div>
</section>

<!-- ============ 2. WELCOME SCREEN ============ -->
<section id="welcome" aria-label="Welcome">
  <div class="welcome-bg" aria-hidden="true"></div>
  <div class="welcome-particles" aria-hidden="true"></div>
  <div class="glass-card welcome-card">
    <p class="eyebrow">a small constellation, made for you</p>
    <h1 class="welcome-title" id="welcome-title">For <span id="recipient-name-1">You</span></h1>
    <p class="welcome-subtitle">Every star in this sky is a moment we've already lived. Come see them.</p>
    <button class="btn btn-primary" id="start-btn" aria-label="Begin the experience">
      <span>Begin</span>
      <i class="fa-solid fa-arrow-right" aria-hidden="true"></i>
      <span class="ripple" aria-hidden="true"></span>
    </button>
  </div>
</section>

<!-- ============ MAIN EXPERIENCE (revealed after Start) ============ -->
<main id="experience" hidden>

  <!-- ============ 3. PROPOSAL PAGE ============ -->
  <section id="proposal" class="section" aria-label="The question">
    <div class="proposal-glow" aria-hidden="true"></div>
    <div class="proposal-content">
      <div class="proposal-gif-frame">
        <img src="assets/gifs/cute.gif" alt="" class="proposal-gif" id="proposal-gif" onerror="this.style.display='none'">
        <div class="gif-fallback-heart" aria-hidden="true"><i class="fa-solid fa-heart"></i></div>
      </div>
      <h2 class="proposal-question" id="proposal-question">Will You Be Mine? <span class="heart-emoji">❤️</span></h2>
      <p class="proposal-sub" id="proposal-sub">No pressure. Just my whole heart, waiting on an answer.</p>

      <div class="proposal-buttons">
        <button class="btn btn-yes" id="yes-btn">YES <span aria-hidden="true">❤️</span></button>
        <button class="btn btn-no" id="no-btn">NO <span aria-hidden="true">😭</span></button>
      </div>
    </div>
  </section>

  <!-- ============ 4. CELEBRATION / YES RESULT ============ -->
  <section id="celebration" class="section" aria-live="polite" hidden>
    <div class="celebration-flash" aria-hidden="true"></div>
    <div class="celebration-content">
      <div class="celebration-heart-burst" aria-hidden="true"></div>
      <h2 class="celebration-title">You made me the happiest person in the world <span aria-hidden="true">❤️</span></h2>
      <p class="celebration-sub" id="celebration-date"></p>
      <button class="btn btn-ghost" id="continue-btn">Keep scrolling <i class="fa-solid fa-chevron-down" aria-hidden="true"></i></button>
    </div>
  </section>

  <!-- ============ 5. LOVE LETTER ============ -->
  <section id="letter-section" class="section" aria-label="A letter for you">
    <h2 class="section-title">A Letter, Sealed For You</h2>
    <div class="envelope-wrap">
      <div class="envelope" id="envelope" role="button" tabindex="0" aria-label="Open the letter" aria-expanded="false">
        <div class="envelope-back"></div>
        <div class="envelope-letter" id="envelope-letter">
          <p class="letter-text" id="letter-text"></p>
          <p class="letter-sign" id="letter-sign">— forever yours</p>
        </div>
        <div class="envelope-flap"></div>
        <div class="envelope-seal"><i class="fa-solid fa-heart" aria-hidden="true"></i></div>
      </div>
      <p class="envelope-hint">tap the envelope to open</p>
    </div>
  </section>

  <!-- ============ 6. TIMELINE (constellation signature) ============ -->
  <section id="timeline-section" class="section" aria-label="Our timeline">
    <h2 class="section-title">Our Story, Written in Stars</h2>
    <p class="section-sub">Scroll to trace the constellation.</p>
    <div class="timeline-wrap">
      <svg class="timeline-constellation" id="constellation-svg" viewBox="0 0 400 1000" preserveAspectRatio="none" aria-hidden="true">
        <path id="constellation-path" d="" />
      </svg>
      <ol class="timeline-list" id="timeline-list"></ol>
    </div>
  </section>

  <!-- ============ 7. PHOTO GALLERY ============ -->
  <section id="gallery-section" class="section" aria-label="Photo gallery">
    <h2 class="section-title">A Few of My Favorites</h2>
    <div class="gallery-grid" id="gallery-grid"></div>
  </section>

  <!-- ============ 8. LIVE COUNTER ============ -->
  <section id="counter-section" class="section" aria-label="Time together">
    <h2 class="section-title">Time We've Shared</h2>
    <div class="counter-grid" id="counter-grid">
      <div class="counter-unit"><span class="counter-value" id="c-years">0</span><span class="counter-label">years</span></div>
      <div class="counter-unit"><span class="counter-value" id="c-months">0</span><span class="counter-label">months</span></div>
      <div class="counter-unit"><span class="counter-value" id="c-days">0</span><span class="counter-label">days</span></div>
      <div class="counter-unit"><span class="counter-value" id="c-hours">0</span><span class="counter-label">hours</span></div>
      <div class="counter-unit"><span class="counter-value" id="c-minutes">0</span><span class="counter-label">min</span></div>
      <div class="counter-unit"><span class="counter-value" id="c-seconds">0</span><span class="counter-label">sec</span></div>
    </div>
  </section>

  <!-- ============ 9. GIFT BOX ============ -->
  <section id="gift-section" class="section" aria-label="A gift">
    <h2 class="section-title">One More Thing</h2>
    <div class="gift-box-wrap" id="gift-box" role="button" tabindex="0" aria-label="Open the gift" aria-expanded="false">
      <div class="gift-lid"></div>
      <div class="gift-base"></div>
      <div class="gift-ribbon-v"></div>
      <div class="gift-ribbon-h"></div>
      <div class="gift-message" id="gift-message" hidden>
        <p id="gift-message-text"></p>
      </div>
    </div>
  </section>

  <!-- ============ 10. SECRET SECTION ============ -->
  <section id="secret-section" class="section" aria-label="Secret section">
    <h2 class="section-title">There's a Secret Here</h2>
    <div class="secret-lock" id="secret-lock">
      <i class="fa-solid fa-lock" aria-hidden="true"></i>
      <label for="secret-input" class="secret-label">Enter the password</label>
      <div class="secret-input-row">
        <input type="password" id="secret-input" placeholder="•••••" autocomplete="off" aria-describedby="secret-hint">
        <button class="btn btn-small" id="secret-submit">Unlock</button>
      </div>
      <p class="secret-hint" id="secret-hint"></p>
    </div>
    <div class="secret-content" id="secret-content" hidden>
      <i class="fa-solid fa-unlock secret-unlocked-icon" aria-hidden="true"></i>
      <p id="secret-message"></p>
      <div class="gallery-grid gallery-grid-small" id="secret-gallery"></div>
    </div>
  </section>

  <!-- ============ 11. ENDING CELEBRATION ============ -->
  <section id="ending-section" class="section" aria-label="Thank you">
    <div class="ending-content">
      <h2 class="ending-title">Thank You for Saying Yes</h2>
      <p class="ending-sub">Here's to every star still waiting to be written.</p>
      <div class="ending-actions">
        <button class="btn btn-primary" id="replay-btn"><i class="fa-solid fa-rotate-left" aria-hidden="true"></i> Replay</button>
        <button class="btn btn-ghost" id="share-btn"><i class="fa-solid fa-share-nodes" aria-hidden="true"></i> Share</button>
        <button class="btn btn-ghost" id="download-btn"><i class="fa-solid fa-download" aria-hidden="true"></i> Save Memories</button>
      </div>
    </div>
  </section>

</main>

<!-- ============ MUSIC PLAYER (floating, persistent) ============ -->
<div class="music-player" id="music-player" aria-label="Music player">
  <img src="assets/images/album-art.jpg" alt="" class="mp-art" id="mp-art" onerror="this.style.display='none'">
  <div class="mp-info">
    <p class="mp-title" id="mp-title">—</p>
    <div class="mp-progress"><div class="mp-progress-fill" id="mp-progress-fill"></div></div>
  </div>
  <div class="mp-controls">
    <button class="mp-btn" id="mp-prev" aria-label="Previous track"><i class="fa-solid fa-backward-step"></i></button>
    <button class="mp-btn mp-btn-play" id="mp-play" aria-label="Play"><i class="fa-solid fa-play"></i></button>
    <button class="mp-btn" id="mp-next" aria-label="Next track"><i class="fa-solid fa-forward-step"></i></button>
    <button class="mp-btn" id="mp-volume-toggle" aria-label="Mute"><i class="fa-solid fa-volume-high"></i></button>
  </div>
  <audio id="mp-audio" preload="none"></audio>
</div>

<!-- Theme switcher -->
<button class="theme-toggle" id="theme-toggle" aria-label="Toggle light and dark theme">
  <i class="fa-solid fa-moon" aria-hidden="true"></i>
</button>

<script src="script.js" defer></script>
</body>
</html>
```

This HTML references `style.css` and `script.js` (already delivered above in the zip/file outputs) — drop all three in the same folder to run it. Want the CSS and JS pasted inline here too?
