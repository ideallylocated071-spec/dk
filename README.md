/**
 * ============================================================================
 * PREMIUM INTERACTIVE PROPOSAL SITE ENGINE CONFIGURATION
 * ============================================================================
 */
const CONFIG = {
    partnerName: "Seraphina",
    anniversaryDate: "2023-10-14T08:00:00", // ISO standard timestamp format
    secretPassword: "ourfirstdate",       // Secret unlock key value
    
    // Aesthetic Accent Palettes
    themes: {
        light: { primary: "#ff4d6d", accentGold: "#cca43b", cursor: "#ff4d6d" },
        dark: { primary: "#ff4d6d", accentGold: "#fbc443", cursor: "#ff4d6d" }
    },
    
    // Audio Architecture Tracking Files
    playlist: [
        { title: "Eternity - Cinematic Romance", url: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" }
    ],
    
    // Timeline Data Schema Structure Matrix
    timeline: [
        { date: "Oct 14, 2023", title: "The First Glimpse", desc: "Our eyes met across that crowded coffee shop, and time stood still." },
        { date: "Dec 25, 2023", title: "Winter Magic", desc: "Walking through the city lights, knowing this was something real." },
        { date: "July 04, 2024", title: "The Summer Journey", desc: "Our unforgettable road trip across the coast under infinite starlight." },
        { date: "Feb 14, 2025", title: "Two Hearts, One Home", desc: "Building our little sanctuary where every day feels like a dream." }
    ],
    
    // Polaroid Assets Gallery Matrix
    gallery: [
        { url: "https://images.unsplash.com/photo-1518199266791-5375a83190b7?w=500", caption: "Starlit Evenings" },
        { url: "https://images.unsplash.com/photo-1511285560929-80b456fea0bc?w=500", caption: "Everyday Magic" },
        { url: "https://images.unsplash.com/photo-1516589178581-6cd7833ae3b2?w=500", caption: "Laughter Shared" },
        { url: "https://images.unsplash.com/photo-1494774157365-9e04c6720e47?w=500", caption: "Forever Bound" }
    ],
    
    secretVows: "You are my sanctuary, my wild adventure, and my absolute certainty. From the quiet mornings to the grand chapters of life, I pledge my whole heart to you, unconditionally, for all of eternity.",
    giftSecret: "Pack your bags, love! A weekend getaway under the mountain canopy awaits us. Check your email for the hidden itinerary! ✈️🏔️",
    finalThankYouText: "Thank you for making me the happiest person alive! Every sunrise belongs to us now."
};

/**
 * ============================================================================
 * CORE RUNTIME ENGINE ARCHITECTURE
 * ============================================================================
 */
document.addEventListener("DOMContentLoaded", () => {
    initLucideIcons();
    initLoaderEngine();
    initAmbientCanvas();
    initCustomCursor();
    initMiniAudioEngine();
    buildDynamicTimeline();
    buildDynamicGallery();
    initRelationshipCounter();
    initInteractionsAndButtons();
    initThemeManager();
});

function initLucideIcons() {
    if (window.lucide) { window.lucide.createIcons(); }
}

/* --- 1. LUXURY LOADING SIMULATOR ENGINE --- */
function initLoaderEngine() {
    let currentPct = 0;
    const loadPctElement = document.getElementById("load-pct");
    const loadBarElement = document.getElementById("load-bar");
    const loaderContainer = document.getElementById("loader");
    const mainContent = document.getElementById("main-content");

    const interval = setInterval(() => {
        currentPct += Math.floor(Math.random() * 8) + 2;
        if (currentPct >= 100) {
            currentPct = 100;
            clearInterval(interval);
            
            // Seamless execution transition
            gsap.to(loaderContainer, {
                opacity: 0, duration: 0.8, ease: "power2.out", onComplete: () => {
                    loaderContainer.style.display = "none";
                    mainContent.classList.remove("hidden");
                    revealHeroElements();
                }
            });
        }
        loadPctElement.innerText = `${currentPct}%`;
        loadBarElement.style.width = `${currentPct}%`;
    }, 45);
}

function revealHeroElements() {
    gsap.fromTo("#welcome-screen .hero-card", 
        { opacity: 0, y: 50 }, 
        { opacity: 1, y: 0, duration: 1.2, ease: "elastic.out(1, 0.75)" }
    );
}

/* --- 2. CANVAS PERFORMANCED AMBIENT BACKGROUND SCENE --- */
function initAmbientCanvas() {
    const canvas = document.getElementById("ambient-canvas");
    const ctx = canvas.getContext("2d");
    let particles = [];

    function resize() {
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
    }
    window.addEventListener("resize", resize);
    resize();

    class Particle {
        constructor() {
            this.reset();
        }
        reset() {
            this.x = Math.random() * canvas.width;
            this.y = canvas.height + Math.random() * 100;
            this.size = Math.random() * 3 + 1;
            this.speedY = Math.random() * 0.8 + 0.3;
            this.speedX = Math.sin(Math.random() * 2) * 0.3;
            this.alpha = Math.random() * 0.5 + 0.2;
            this.type = Math.random() > 0.7 ? 'heart' : 'dot';
        }
        update() {
            this.y -= this.speedY;
            this.x += this.speedX;
            if (this.y < -10) this.reset();
        }
        draw() {
            ctx.save();
            ctx.globalAlpha = this.alpha;
            ctx.fillStyle = getComputedStyle(document.documentElement).getPropertyValue('--primary').trim();
            if (this.type === 'heart') {
                ctx.font = `${this.size * 3}px serif`;
                ctx.fillText('❤️', this.x, this.y);
            } else {
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
            }
            ctx.restore();
        }
    }

    for (let i = 0; i < 40; i++) { particles.push(new Particle()); }

    function animate() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        particles.forEach(p => { p.update(); p.draw(); });
        requestAnimationFrame(animate);
    }
    animate();
}

/* --- 3. HARDWARE ACCELERATED CUSTOM CURSOR MODULE --- */
function initCustomCursor() {
    const cursor = document.getElementById("custom-cursor");
    const sparkleContainer = document.getElementById("cursor-sparkle-container");
    if (!cursor) return;

    window.addEventListener("mousemove", (e) => {
        gsap.to(cursor, { x: e.clientX, y: e.clientY, duration: 0.1, ease: "power1.out" });
        if (Math.random() > 0.85) { createSparkle(e.clientX, e.clientY); }
    });

    function createSparkle(x, y) {
        const dot = document.createElement("div");
        dot.className = "sparkle-dot";
        const size = Math.random() * 4 + 2;
        dot.style.width = `${size}px`;
        dot.style.height = `${size}px`;
        dot.style.left = `${x}px`;
        dot.style.top = `${y}px`;
        sparkleContainer.appendChild(dot);

        gsap.to(dot, {
            x: (Math.random() - 0.5) * 30,
            y: (Math.random() - 0.5) * 30,
            opacity: 0,
            scale: 0,
            duration: 0.8,
            onComplete: () => dot.remove()
        });
    }
}

/* --- 4. AUDIO AUDIO SUBSYSTEM ENGINE (VANILLA COMPATIBLE) --- */
function initMiniAudioEngine() {
    const audio = new Audio();
    audio.src = CONFIG.playlist[0].url;
    audio.loop = true;
    
    const playPauseBtn = document.getElementById("play-pause-btn");
    const playIcon = document.getElementById("play-icon");
    const trackTitle = document.getElementById("track-title");
    const progressBar = document.getElementById("progress-bar");
    const progressContainer = document.getElementById("progress-container");

    trackTitle.innerText = CONFIG.playlist[0].title;

    function togglePlay() {
        if (audio.paused) {
            audio.play().then(() => {
                if (window.lucide) {
                    playPauseBtn.innerHTML = '<i data-lucide="pause"></i>';
                    window.lucide.createIcons();
                }
            }).catch(err => console.log("Audio play deferred due to policy context: ", err));
        } else {
            audio.pause();
            if (window.lucide) {
                playPauseBtn.innerHTML = '<i data-lucide="play"></i>';
                window.lucide.createIcons();
            }
        }
    }

    playPauseBtn.addEventListener("click", togglePlay);
    document.getElementById("start-journey-btn").addEventListener("click", () => {
        if (audio.paused) togglePlay();
    });

    audio.addEventListener("timeupdate", () => {
        const pct = (audio.currentTime / audio.duration) * 100;
        progressBar.style.width = `${pct}%`;
    });

    progressContainer.addEventListener("click", (e) => {
        const width = progressContainer.clientWidth;
        const clickX = e.offsetX;
        audio.currentTime = (clickX / width) * audio.duration;
    });
}

/* --- 5. DATA RENDERING AND INTERACTIVE LAYOUT SCROLL TRIGGER BUILDERS --- */
function buildDynamicTimeline() {
    const container = document.getElementById("timeline-events");
    CONFIG.timeline.forEach((item, index) => {
        const side = index % 2 === 0 ? 'left' : 'right';
        const node = document.createElement("div");
        node.className = `timeline-item ${side} hidden-element`;
        node.innerHTML = `
            <div class="timeline-badge"><i style="width:10px;height:10px;" data-lucide="heart"></i></div>
            <div class="timeline-content glass-card">
                <span>${item.date}</span>
                <h4>${item.title}</h4>
                <p class="subtitle-inter" style="font-size:0.9rem;">${item.desc}</p>
            </div>
        `;
        container.appendChild(node);
        registerScrollReveal(node);
    });
    initLucideIcons();
}

function buildDynamicGallery() {
    const grid = document.getElementById("gallery-grid");
    CONFIG.gallery.forEach((pic) => {
        const rot = (Math.random() * 8 - 4).toFixed(2);
        const card = document.createElement("div");
        card.className = "polaroid hidden-element";
        card.style.setProperty('--rot', `${rot}deg`);
        card.innerHTML = `
            <img src="${pic.url}" alt="${pic.caption}" loading="lazy">
            <div class="polaroid-caption">${pic.caption}</div>
        `;
        grid.appendChild(card);
        registerScrollReveal(card);

        card.addEventListener("click", () => openLightbox(pic.url, pic.caption));
    });
}

function registerScrollReveal(element) {
    // Elegant standard visibility entry tracking interface strategy
    const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.classList.add("visible-element");
                observer.unobserve(entry.target);
            }
        });
    }, { threshold: 0.15 });
    observer.observe(element);
}

/* --- 6. LIGHTBOX MODULE CONTROLS --- */
const lightbox = document.getElementById("lightbox");
const lightboxImg = document.getElementById("lightbox-img");
const lightboxCap = document.getElementById("lightbox-caption");
document.querySelector(".close-lightbox")?.addEventListener("click", () => lightbox.style.display = "none");

function openLightbox(url, caption) {
    lightbox.style.display = "flex";
    lightboxImg.src = url;
    lightboxCap.innerText = caption;
}

/* --- 7. HI-PERFORMANCE HIGH-PRECISION TICKING COUNTER SYSTEM --- */
function initRelationshipCounter() {
    const startDate = new Date(CONFIG.anniversaryDate);
    
    function tick() {
        const now = new Date();
        let diff = now - startDate;
        if (diff < 0) diff = 0;

        const secs = Math.floor(diff / 1000) % 60;
        const mins = Math.floor(diff / (1000 * 60)) % 60;
        const hours = Math.floor(diff / (1000 * 60 * 60)) % 24;
        
        // Exact processing metrics calculated natively without external math library bloating
        const totalDays = Math.floor(diff / (1000 * 60 * 60 * 24));
        const years = Math.floor(totalDays / 365);
        const remainingDaysAfterYears = totalDays % 365;
        const months = Math.floor(remainingDaysAfterYears / 30.4368);
        const days = Math.floor(remainingDaysAfterYears % 30.4368);

        document.getElementById("count-years").innerText = String(years).padStart(2, '0');
        document.getElementById("count-months").innerText = String(months).padStart(2, '0');
        document.getElementById("count-days").innerText = String(days).padStart(2, '0');
        document.getElementById("count-hours").innerText = String(hours).padStart(2, '0');
        document.getElementById("count-minutes").innerText = String(mins).padStart(2, '0');
        document.getElementById("count-seconds").innerText = String(secs).padStart(2, '0');
    }
    tick();
    setInterval(tick, 1000);
}

/* --- 8. RICH FUNCTIONAL ANIMATIONS & BUTTON MATRIX LOGIC --- */
function initInteractionsAndButtons() {
    // Primary Entry Navigation Scroll Command Hook
    document.getElementById("start-journey-btn").addEventListener("click", () => {
        document.getElementById("counter-section").scrollIntoView({ behavior: "smooth" });
    });

    // Elegant Structural Surprise Reveal Module Action Box
    const giftBox = document.getElementById("interactive-gift-box");
    const giftRevealCard = document.getElementById("gift-reveal-card");
    const secretTextNode = document.getElementById("gift-secret-text");
    
    giftBox.addEventListener("click", () => {
        if (!giftBox.classList.contains("open")) {
            giftBox.classList.add("open");
            secretTextNode.innerText = CONFIG.giftSecret;
            setTimeout(() => {
                giftRevealCard.classList.remove("hidden-element");
                giftRevealCard.classList.add("visible-element");
                triggerConfettiExplosion();
            }, 600);
        }
    });

    // Vault Authentication Verification Gateway Layer Control Module
    const unlockBtn = document.getElementById("unlock-btn");
    const passwordInput = document.getElementById("secret-password");
    const errorMsgNode = document.getElementById("lock-error");
    const vaultRevealCard = document.getElementById("secret-vault-content");
    const vaultTextNode = document.getElementById("vault-text-content");

    unlockBtn.addEventListener("click", () => {
        if (passwordInput.value.trim().toLowerCase() === CONFIG.secretPassword.toLowerCase()) {
            errorMsgNode.innerText = "";
            vaultTextNode.innerText = CONFIG.secretVows;
            vaultRevealCard.classList.remove("hidden-element");
            vaultRevealCard.classList.add("visible-element");
            gsap.fromTo(vaultRevealCard, { scale: 0.9, opacity: 0 }, { scale: 1, opacity: 1, duration: 0.6 });
        } else {
            errorMsgNode.innerText = "Incorrect memory passcode. Please try again.";
            gsap.fromTo(".lock-card", { x: -10 }, { x: 10, duration: 0.1, repeat: 5, yoyo: true });
        }
    });

    /**
     * ADVANCED RUNTIME ESCAPE FLUID LOGIC CORE (NO-BUTTON ENGINE)
     */
    const noBtn = document.getElementById("propose-no");
    const container = document.getElementById("proposal-btn-container");
    let escapeCounter = 0;

    noBtn.addEventListener("mouseover", handleNoEscape);
    noBtn.addEventListener("click", handleNoEscape);

    function handleNoEscape(e) {
        escapeCounter++;
        
        if (escapeCounter >= 6) {
            // Self-transform structural optimization loop
            noBtn.innerText = "YES ❤️";
            noBtn.className = "action-btn yes-btn";
            noBtn.removeEventListener("mouseover", handleNoEscape);
            noBtn.removeEventListener("click", handleNoEscape);
            noBtn.addEventListener("click", processFinalAcceptanceJourney);
            return;
        }

        const containerRect = container.getBoundingClientRect();
        const btnRect = noBtn.getBoundingClientRect();

        // Calculate secure spatial random grid points bounds within inner bounding constraints matrix
        const maxDeltaX = 150;
        const maxDeltaY = 80;
        
        let targetX = (Math.random() - 0.5) * maxDeltaX * 2;
        let targetY = (Math.random() - 0.5) * maxDeltaY * 2;

        const currentScale = Math.max(0.6, 1 - escapeCounter * 0.08);
        const currentRot = (Math.random() * 30 - 15);

        gsap.to(noBtn, {
            x: targetX,
            y: targetY,
            scale: currentScale,
            rotation: currentRot,
            duration: 0.3,
            ease: "power2.out"
        });
    }

    // Direct Bind Execution Hook
    document.getElementById("propose-yes").addEventListener("click", processFinalAcceptanceJourney);

    function processFinalAcceptanceJourney() {
        triggerConfettiExplosion();
        triggerMassiveFireworkBurst();
        
        // Dynamic DOM Update Matrix Manipulation Layout Updates
        document.getElementById("proposal-headline").innerText = `You made me the happiest person in the world, ${CONFIG.partnerName}! ❤️`;
        document.getElementById("proposal-btn-container").style.display = "none";

        // Open Letter Sequencing Timelines Hook Launch Elements
        const letterSection = document.getElementById("love-letter-section");
        letterSection.classList.remove("hidden-element");
        letterSection.classList.add("visible-element");
        
        setTimeout(() => {
            letterSection.scrollIntoView({ behavior: "smooth" });
            initEnvelopeLetterTypingEngine();
        }, 1200);
    }
}

/* --- 9. LETTER MODULE ENVELOPE OPENING MECHANICS --- */
function initEnvelopeLetterTypingEngine() {
    const envelope = document.getElementById("envelope");
    envelope.addEventListener("click", () => {
        if (!envelope.classList.contains("open")) {
            envelope.classList.add("open");
            setTimeout(startTypewriterFlow, 800);
        }
    });
}

function startTypewriterFlow() {
    const txtNode = document.getElementById("typewriter-text");
    if (txtNode.innerHTML !== "") return; // Protect structural re-trigger iterations
    
    let index = 0;
    const speed = 45; // Millisecond processing delay interval standard metrics loop
    
    function type() {
        if (index < CONFIG.secretVows.length) {
            txtNode.innerHTML += CONFIG.secretVows.charAt(index);
            index++;
            setTimeout(type, speed);
        } else {
            revealCelebrationCardScreenSection();
        }
    }
    type();
}

function revealCelebrationCardScreenSection() {
    const targetSection = document.getElementById("celebration-section");
    const textHolder = document.getElementById("final-thankyou");
    
    textHolder.innerText = CONFIG.finalThankYouText;
    targetSection.classList.remove("hidden-element");
    targetSection.classList.add("visible-element");

    setTimeout(() => {
        targetSection.scrollIntoView({ behavior: "smooth" });
    }, 1500);

    document.getElementById("replay-btn").addEventListener("click", () => {
        window.scrollTo({ top: 0, behavior: "smooth" });
        setTimeout(() => location.reload(), 1000);
    });
}

/* --- 10. HIGH CONTEXT SEAMLESS PARTICLE GRAPHICS EFFECTS HANDLERS --- */
function triggerConfettiExplosion() {
    if (window.confetti) {
        window.confetti({ particleCount: 150, spread: 80, origin: { y: 0.6 } });
    }
}

function triggerMassiveFireworkBurst() {
    if (!window.confetti) return;
    const duration = 4 * 1000;
    const animationEnd = Date.now() + duration;
    const defaults = { startVelocity: 30, spread: 360, ticks: 60, zIndex: 9999 };

    function randomInRange(min, max) { return Math.random() * (max - min) + min; }

    const interval = setInterval(function() {
        const timeLeft = animationEnd - Date.now();
        if (timeLeft <= 0) return clearInterval(interval);

        const particleCount = 50 * (timeLeft / duration);
        window.confetti(Object.assign({}, defaults, { particleCount, origin: { x: randomInRange(0.1, 0.3), y: Math.random() - 0.2 } }));
        window.confetti(Object.assign({}, defaults, { particleCount, origin: { x: randomInRange(0.7, 0.9), y: Math.random() - 0.2 } }));
    }, 250);
}

/* --- 11. CENTRALIZED INTERACTIVE LUXURY THEME ENVIRONMENT MANAGER --- */
function initThemeManager() {
    const toggleBtn = document.getElementById("theme-toggle");
    if (!toggleBtn) return;

    toggleBtn.addEventListener("click", () => {
        const currentTheme = document.documentElement.getAttribute("data-theme") || "light";
        const newTheme = currentTheme === "light" ? "dark" : "light";
        
        document.documentElement.setAttribute("data-theme", newTheme);
        const iconNode = toggleBtn.querySelector("i");
        
        if (iconNode && window.lucide) {
            toggleBtn.innerHTML = newTheme === "light" ? '<i data-lucide="moon"></i>' : '<i data-lucide="sun"></i>';
            window.lucide.createIcons();
        }
    });
}
