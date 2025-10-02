<html lang="en"><head>
    <meta charset="UTF-8">
    <title>Axiom Docs — Developer Guide</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <!-- Swiper CSS -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.css">
    <style>
      @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&display=swap');
      * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Geist', 'Inter', system-ui, -apple-system, sans-serif; }
      html, body { height: 100%; overflow: auto; }
      .spline-container { position: fixed; inset: 0; z-index: -2; }
      .content-container { position: relative; z-index: 10; min-height: 100vh; }
      .glass { backdrop-filter: blur(14px); -webkit-backdrop-filter: blur(14px); }
      .ring-contrast { box-shadow: 0 0 0 1px rgba(255,255,255,0.08) inset; }
      .kbd { border: 1px solid rgba(255,255,255,.16); padding: 2px 6px; border-radius: 6px; font-size: 12px; background: rgba(255,255,255,.06); }
      .focus-ring:focus-visible { outline: 2px solid rgba(148,163,184,.5); outline-offset: 3px; }
      .title-gradient { background: linear-gradient(to right, rgb(96 165 250), rgb(167 139 250)); -webkit-background-clip: text; background-clip: text; color: transparent; }

      /* Parallax layers */
      .parallax-fixed { position: fixed; inset: 0; pointer-events: none; z-index: -1; }
      .p-layer { position: absolute; border-radius: 9999px; filter: blur(60px); opacity: 0.28; }
      .p1 { width: 520px; height: 520px; left: -120px; top: -120px; background: rgba(59,130,246,0.35); }
      .p2 { width: 620px; height: 620px; right: -140px; top: 30vh; background: rgba(217,70,239,0.35); }
      .p3 { width: 900px; height: 900px; left: 50%; top: 120vh; transform: translateX(-50%); background: rgba(99,102,241,0.32); }
      .p4 { position: absolute; inset: 0; background: radial-gradient(1200px 480px at 50% -120px, rgba(255,255,255,0.06), transparent 60%); }
      .p5 { position: absolute; inset: 0; background: linear-gradient(to bottom, rgba(255,255,255,0.05), transparent 35%, transparent 70%, rgba(255,255,255,0.05)); }

      /* In-view animation system */
      [data-animate] { opacity: 0.85; transform: translateY(18px); filter: blur(10px); }
      [data-animate].is-inview { animation: fadeIn 0.8s ease-out both, slideUp 0.8s ease-out both, blurIn 1s ease-out both; animation-delay: var(--d, 0s); }
      @keyframes fadeIn { from { opacity: 0.75; } to { opacity: 1; } }
      @keyframes slideUp { from { transform: translateY(18px); } to { transform: translateY(0); } }
      @keyframes blurIn { from { filter: blur(10px); } to { filter: blur(0); } }

      /* Marquee */
      .marquee-track { display: flex; gap: 16px; white-space: nowrap; }
      .marquee-inner { display: inline-flex; gap: 16px; }
      .marquee-animate { animation: marquee 28s linear infinite; }
      @keyframes marquee {
        0% { transform: translateX(0); }
        100% { transform: translateX(-50%); }
      }

      /* Table */
      .tbl th { text-align: left; font-weight: 500; color: rgba(255,255,255,0.85); }
      .tbl td, .tbl th { padding: 12px 16px; border-bottom: 1px solid rgba(255,255,255,0.08); }
      .tbl tr:hover td { background-color: rgba(255,255,255,0.04); }

      /* Edge masks for marquee */
      .edge-mask {
        mask-image: linear-gradient(to right, transparent, black 8%, black 92%, transparent);
        -webkit-mask-image: linear-gradient(to right, transparent, black 8%, black 92%, transparent);
      }
    </style>
  </head>
  <body class="bg-black text-white antialiased selection:bg-white/20 scroll-smooth">
    <!-- Parallax Background Layers -->
    <div aria-hidden="true" class="parallax-fixed">
      <div class="p-layer p1"></div>
      <div class="p-layer p2"></div>
      <div class="p-layer p3"></div>
      <div class="p4"></div>
      <div class="p5"></div>
    </div>

    <!-- Spline Background -->
    <div class="spline-container">
      <iframe src="https://my.spline.design/claritystream-a72K0KUwFoZV82QBzvu52Kai/" frameborder="0" width="100%" height="100%"></iframe>
    </div>

    <!-- Content Overlay -->
    <div class="content-container">
      <!-- Navigation -->
      <nav class="container mx-auto px-6 py-6" data-animate="" style="--d: .05s;">
        <div class="flex items-center justify-between glass rounded-xl border border-white/10 px-4 py-3 ring-contrast">
          <div class="flex items-center">
            <div class="w-8 h-8 rounded-lg bg-white/10 flex items-center justify-center ring-1 ring-white/10">
              <span class="text-sm sf-pro-display tracking-tight">AX</span>
            </div>
            <span class="ml-3 text-xl tracking-tight sf-pro-display">Axiom Docs</span>
          </div>
          <div class="hidden md:flex space-x-8 text-sm text-gray-300">
            <a href="#about" class="hover:text-white transition-colors">About</a>
            <a href="#sports" class="hover:text-white transition-colors">Sports</a>
            <a href="#registration" class="hover:text-white transition-colors">Registration</a>
            <a href="#sponsors" class="hover:text-white transition-colors">Sponsors</a>
            <a href="#gallery" class="hover:text-white transition-colors">Gallery</a>
            <a href="#team" class="hover:text-white transition-colors">Team</a>
            <a href="#contact" class="hover:text-white transition-colors">Contact</a>
          </div>
          <div class="flex items-center gap-2">
            <button class="hidden md:inline-flex text-sm border border-gray-700 rounded-md px-4 py-2 hover:bg-white/5 transition-all focus-ring">
              <i data-lucide="search" class="w-4 h-4 mr-2" stroke-width="1.5"></i>Search
              <span class="ml-2 kbd">/</span>
            </button>
            <button class="text-sm border border-gray-700 rounded-md px-4 py-2 hover:bg-white/5 transition-all focus-ring">Sign in</button>
          </div>
        </div>

        <!-- Mobile section nav -->
        <div class="mt-3 md:hidden">
          <div class="flex items-center gap-2 overflow-x-auto no-scrollbar whitespace-nowrap px-1">
            <a href="#about" class="px-3 py-1.5 text-xs rounded-lg bg-white/5 border border-white/10 hover:border-white/20 hover:bg-white/10 transition">About</a>
            <a href="#sports" class="px-3 py-1.5 text-xs rounded-lg bg-white/5 border border-white/10 hover:border-white/20 hover:bg-white/10 transition">Sports</a>
            <a href="#registration" class="px-3 py-1.5 text-xs rounded-lg bg-white/5 border border-white/10 hover:border-white/20 hover:bg-white/10 transition">Registration</a>
            <a href="#sponsors" class="px-3 py-1.5 text-xs rounded-lg bg-white/5 border border-white/10 hover:border-white/20 hover:bg-white/10 transition">Sponsors</a>
            <a href="#gallery" class="px-3 py-1.5 text-xs rounded-lg bg-white/5 border border-white/10 hover:border-white/20 hover:bg-white/10 transition">Gallery</a>
            <a href="#team" class="px-3 py-1.5 text-xs rounded-lg bg-white/5 border border-white/10 hover:border-white/20 hover:bg-white/10 transition">Team</a>
            <a href="#contact" class="px-3 py-1.5 text-xs rounded-lg bg-white/5 border border-white/10 hover:border-white/20 hover:bg-white/10 transition">Contact</a>
          </div>
        </div>
      </nav>

      <!-- Hero -->
      <header class="container mx-auto px-6 pt-10 md:pt-16">
        <div class="flex flex-col items-center text-center max-w-3xl mx-auto">
          <h1 class="text-5xl md:text-6xl lg:text-7xl font-light tracking-tight mb-6 leading-tight" data-animate="" style="--d: .1s;">
            <span class="title-gradient">Developer Documentation</span> for the Axiom platform
          </h1>
          <p class="text-gray-300 text-xl md:text-2xl mb-8 max-w-2xl font-light tracking-tight" data-animate="" style="--d: .18s;">
            Build, secure, and scale. Clear guides, robust APIs, and practical examples to help you ship with confidence.
          </p>
          <div class="flex flex-col sm:flex-row gap-4 mt-2" data-animate="" style="--d: .26s;">
            <button class="bg-white text-black font-light rounded-md px-8 py-3 hover:bg-opacity-90 transition-all focus-ring">
              Get started
            </button>
            <a href="#about" class="flex items-center text-gray-300 hover:text-white transition-colors py-3 px-2 group focus-ring rounded-md">
              Browse sections
              <i data-lucide="arrow-right" class="w-4 h-4 ml-2 transition-transform group-hover:translate-x-1" stroke-width="1.5"></i>
            </a>
          </div>

          <!-- Stats -->
          <div class="grid grid-cols-2 md:grid-cols-4 gap-6 mt-14 max-w-4xl mx-auto w-full">
            <div class="glass rounded-xl border border-white/10 p-4 ring-contrast" data-animate="" style="--d: .1s;">
              <p class="text-4xl font-light mb-1 tracking-tight">99.99%</p>
              <p class="text-gray-400 font-extralight">API uptime</p>
            </div>
            <div class="glass rounded-xl border border-white/10 p-4 ring-contrast" data-animate="" style="--d: .15s;">
              <p class="text-4xl font-light mb-1 tracking-tight">250ms</p>
              <p class="text-gray-400 font-extralight">Global p95</p>
            </div>
            <div class="glass rounded-xl border border-white/10 p-4 ring-contrast" data-animate="" style="--d: .2s;">
              <p class="text-4xl font-light mb-1 tracking-tight">40+</p>
              <p class="text-gray-400 font-extralight">Endpoints</p>
            </div>
            <div class="glass rounded-xl border border-white/10 p-4 ring-contrast" data-animate="" style="--d: .25s;">
              <p class="text-4xl font-light mb-1 tracking-tight">12</p>
              <p class="text-gray-400 font-extralight">SDKs</p>
            </div>
          </div>
        </div>
      </header>

      <!-- Marquee -->
      <section class="container mx-auto px-6 mt-12">
        <div class="relative glass border border-white/10 rounded-xl ring-contrast overflow-hidden edge-mask" data-animate="" style="--d: .05s;">
          <div class="marquee-track marquee-animate">
            <div class="marquee-inner px-4 py-3">
              <span class="inline-flex items-center gap-2 px-3 py-1 rounded-lg bg-white/5 border border-white/10 hover:border-white/20 transition-colors">
                <i data-lucide="github" class="w-4 h-4" stroke-width="1.5"></i> GitHub Actions
              </span>
              <span class="inline-flex items-center gap-2 px-3 py-1 rounded-lg bg-white/5 border border-white/10 hover:border-white/20 transition-colors">
                <i data-lucide="npm" class="w-4 h-4" stroke-width="1.5"></i> npm
              </span>
              <span class="inline-flex items-center gap-2 px-3 py-1 rounded-lg bg-white/5 border border-white/10 hover:border-white/20 transition-colors">
                <i data-lucide="server" class="w-4 h-4" stroke-width="1.5"></i> Edge Runtime
              </span>
              <span class="inline-flex items-center gap-2 px-3 py-1 rounded-lg bg-white/5 border border-white/10 hover:border-white/20 transition-colors">
                <i data-lucide="database" class="w-4 h-4" stroke-width="1.5"></i> SQL
              </span>
              <span class="inline-flex items-center gap-2 px-3 py-1 rounded-lg bg-white/5 border border-white/10 hover:border-white/20 transition-colors">
                <i data-lucide="cloud" class="w-4 h-4" stroke-width="1.5"></i> Storage
              </span>
              <span class="inline-flex items-center gap-2 px-3 py-1 rounded-lg bg-white/5 border border-white/10 hover:border-white/20 transition-colors">
                <i data-lucide="shield" class="w-4 h-4" stroke-width="1.5"></i> OAuth
              </span>
              <span class="inline-flex items-center gap-2 px-3 py-1 rounded-lg bg-white/5 border border-white/10 hover:border-white/20 transition-colors">
                <i data-lucide="cpu" class="w-4 h-4" stroke-width="1.5"></i> Webhooks
              </span>
            </div>
            <!-- Duplicate for seamless loop -->
            <div class="marquee-inner px-4 py-3">
              <span class="inline-flex items-center gap-2 px-3 py-1 rounded-lg bg-white/5 border border-white/10 hover:border-white/20 transition-colors">
                <i data-lucide="github" class="w-4 h-4" stroke-width="1.5"></i> GitHub Actions
              </span>
              <span class="inline-flex items-center gap-2 px-3 py-1 rounded-lg bg-white/5 border border-white/10 hover:border-white/20 transition-colors">
                <i data-lucide="npm" class="w-4 h-4" stroke-width="1.5"></i> npm
              </span>
              <span class="inline-flex items-center gap-2 px-3 py-1 rounded-lg bg-white/5 border border-white/10 hover:border-white/20 transition-colors">
                <i data-lucide="server" class="w-4 h-4" stroke-width="1.5"></i> Edge Runtime
              </span>
              <span class="inline-flex items-center gap-2 px-3 py-1 rounded-lg bg-white/5 border border-white/10 hover:border-white/20 transition-colors">
                <i data-lucide="database" class="w-4 h-4" stroke-width="1.5"></i> SQL
              </span>
              <span class="inline-flex items-center gap-2 px-3 py-1 rounded-lg bg-white/5 border border-white/10 hover:border-white/20 transition-colors">
                <i data-lucide="cloud" class="w-4 h-4" stroke-width="1.5"></i> Storage
              </span>
              <span class="inline-flex items-center gap-2 px-3 py-1 rounded-lg bg-white/5 border border-white/10 hover:border-white/20 transition-colors">
                <i data-lucide="shield" class="w-4 h-4" stroke-width="1.5"></i> OAuth
              </span>
              <span class="inline-flex items-center gap-2 px-3 py-1 rounded-lg bg-white/5 border border-white/10 hover:border-white/20 transition-colors">
                <i data-lucide="cpu" class="w-4 h-4" stroke-width="1.5"></i> Webhooks
              </span>
            </div>
          </div>
        </div>
      </section>

      <!-- Removed Docs Layout (Overview, Authentication, Rate limits, API Endpoints, and the "On this page" box) -->

      <!-- About -->
      <section id="about" class="container mx-auto px-6 mt-16 scroll-mt-24">
        <div class="max-w-5xl mx-auto glass rounded-2xl border border-white/10 ring-contrast p-8 text-center" data-animate="" style="--d:.05s;">
          <h2 class="text-3xl tracking-tight font-light mb-4 title-gradient">About</h2>
          <p class="text-white/80 max-w-3xl mx-auto">
            Our event is built on innovation, teamwork, and excellence. We aim to bring
            athletes, partners, and the community together for an unforgettable experience.
          </p>
        </div>
      </section>

      <!-- Sports with 3D Coverflow Carousel -->
      <section id="sports" class="container mx-auto px-6 mt-16 scroll-mt-24">
        <div class="max-w-6xl mx-auto glass rounded-2xl border border-white/10 ring-contrast p-8" data-animate="" style="--d:.08s;">
          <h2 class="text-3xl tracking-tight font-light mb-2 title-gradient text-center">Sports</h2>
          <p class="text-center text-white/70 max-w-2xl mx-auto">Swipe or drag to explore featured sports.</p>

          <div class="swiper sportsSwiper w-full" style="padding-top: 40px; padding-bottom: 60px;">
            <div class="swiper-wrapper">
              <!-- Football -->
              <div class="swiper-slide w-[260px] h-[320px] sm:w-[300px] sm:h-[340px] md:w-[360px] md:h-[360px]">
                <div class="relative w-full h-full rounded-2xl overflow-hidden border border-white/10 glass ring-1 ring-white/10">
                  <img src="https://source.unsplash.com/800x600/?football" alt="Football" class="absolute inset-0 w-full h-full object-cover">
                  <div class="absolute inset-0 bg-gradient-to-t from-black/60 via-black/20 to-transparent"></div>
                  <div class="absolute bottom-0 w-full p-4">
                    <h3 class="text-lg font-medium tracking-tight">Football</h3>
                    <p class="text-xs text-white/70 mt-0.5">High-energy matches with top teams.</p>
                  </div>
                </div>
              </div>
              <!-- Basketball -->
              <div class="swiper-slide w-[260px] h-[320px] sm:w-[300px] sm:h-[340px] md:w-[360px] md:h-[360px]">
                <div class="relative w-full h-full rounded-2xl overflow-hidden border border-white/10 glass ring-1 ring-white/10">
                  <img src="https://source.unsplash.com/800x600/?basketball" alt="Basketball" class="absolute inset-0 w-full h-full object-cover">
                  <div class="absolute inset-0 bg-gradient-to-t from-black/60 via-black/20 to-transparent"></div>
                  <div class="absolute bottom-0 w-full p-4">
                    <h3 class="text-lg font-medium tracking-tight">Basketball</h3>
                    <p class="text-xs text-white/70 mt-0.5">Fast-paced and action-packed games.</p>
                  </div>
                </div>
              </div>
              <!-- Athletics -->
              <div class="swiper-slide w-[260px] h-[320px] sm:w-[300px] sm:h-[340px] md:w-[360px] md:h-[360px]">
                <div class="relative w-full h-full rounded-2xl overflow-hidden border border-white/10 glass ring-1 ring-white/10">
                  <img src="https://source.unsplash.com/800x600/?running" alt="Athletics" class="absolute inset-0 w-full h-full object-cover">
                  <div class="absolute inset-0 bg-gradient-to-t from-black/60 via-black/20 to-transparent"></div>
                  <div class="absolute bottom-0 w-full p-4">
                    <h3 class="text-lg font-medium tracking-tight">Athletics</h3>
                    <p class="text-xs text-white/70 mt-0.5">Track &amp; field competitions at their best.</p>
                  </div>
                </div>
              </div>
              <!-- Optional extra slides for depth -->
              <div class="swiper-slide w-[260px] h-[320px] sm:w-[300px] sm:h-[340px] md:w-[360px] md:h-[360px]">
                <div class="relative w-full h-full rounded-2xl overflow-hidden border border-white/10 glass ring-1 ring-white/10">
                  <img src="https://source.unsplash.com/800x600/?tennis" alt="Tennis" class="absolute inset-0 w-full h-full object-cover">
                  <div class="absolute inset-0 bg-gradient-to-t from-black/60 via-black/20 to-transparent"></div>
                  <div class="absolute bottom-0 w-full p-4">
                    <h3 class="text-lg font-medium tracking-tight">Tennis</h3>
                    <p class="text-xs text-white/70 mt-0.5">Singles and doubles tournaments.</p>
                  </div>
                </div>
              </div>
              <div class="swiper-slide w-[260px] h-[320px] sm:w-[300px] sm:h-[340px] md:w-[360px] md:h-[360px]">
                <div class="relative w-full h-full rounded-2xl overflow-hidden border border-white/10 glass ring-1 ring-white/10">
                  <img src="https://source.unsplash.com/800x600/?swimming" alt="Swimming" class="absolute inset-0 w-full h-full object-cover">
                  <div class="absolute inset-0 bg-gradient-to-t from-black/60 via-black/20 to-transparent"></div>
                  <div class="absolute bottom-0 w-full p-4">
                    <h3 class="text-lg font-medium tracking-tight">Swimming</h3>
                    <p class="text-xs text-white/70 mt-0.5">Relay and individual events.</p>
                  </div>
                </div>
              </div>
            </div>
          </div>

        </div>
      </section>

      <!-- Registration -->
      <section id="registration" class="container mx-auto px-6 mt-16 scroll-mt-24">
        <div class="max-w-5xl mx-auto glass rounded-2xl border border-white/10 ring-contrast p-8 text-center" data-animate="" style="--d:.1s;">
          <h2 class="text-3xl tracking-tight font-light mb-6 title-gradient">Registration</h2>
          <p class="text-white/80 mb-6">Sign up now to secure your spot in the competition!</p>
          <a href="#" class="bg-white text-black px-6 py3 rounded-lg hover:bg-opacity-90 transition focus-ring inline-flex items-center justify-center">
            Register Now
          </a>
        </div>
      </section>

      <!-- Sponsors & Partners -->
      <section id="sponsors" class="container mx-auto px-6 mt-16 scroll-mt-24">
        <div class="max-w-6xl mx-auto glass rounded-2xl border border-white/10 ring-contrast p-8 text-center" data-animate="" style="--d:.12s;">
          <h2 class="text-3xl tracking-tight font-light mb-6 title-gradient">Sponsors &amp; Partners</h2>
        <div class="grid grid-cols-2 md:grid-cols-4 gap-6 items-center">
            <img src="https://source.unsplash.com/200x100/?logo" alt="Sponsor" class="mx-auto opacity-90 hover:opacity-100 transition">
            <img src="https://source.unsplash.com/200x100/?brand" alt="Partner" class="mx-auto opacity-90 hover:opacity-100 transition">
            <img src="https://source.unsplash.com/200x100/?company" alt="Sponsor" class="mx-auto opacity-90 hover:opacity-100 transition">
            <img src="https://source.unsplash.com/200x100/?business" alt="Partner" class="mx-auto opacity-90 hover:opacity-100 transition">
          </div>
        </div>
      </section>

      <!-- Gallery / Highlights -->
      <section id="gallery" class="container mx-auto px-6 mt-16 scroll-mt-24">
        <div class="max-w-6xl mx-auto glass rounded-2xl border border-white/10 ring-contrast p-8" data-animate="" style="--d:.14s;">
          <h2 class="text-3xl tracking-tight font-light mb-6 title-gradient text-center">Gallery &amp; Highlights</h2>
          <div class="grid md:grid-cols-3 gap-6">
            <img src="https://source.unsplash.com/600x400/?stadium" class="rounded-lg object-cover w-full h-56 hover:brightness-110 transition" alt="Highlight">
            <img src="https://source.unsplash.com/600x400/?sports" class="rounded-lg object-cover w-full h-56 hover:brightness-110 transition" alt="Highlight">
            <img src="https://source.unsplash.com/600x400/?crowd" class="rounded-lg object-cover w-full h-56 hover:brightness-110 transition" alt="Highlight">
          </div>
        </div>
      </section>

      <!-- Team / Organizers -->
      <section id="team" class="container mx-auto px-6 mt-16 scroll-mt-24">
        <div class="max-w-6xl mx-auto glass rounded-2xl border border-white/10 ring-contrast p-8" data-animate="" style="--d:.16s;">
          <h2 class="text-3xl tracking-tight font-light mb-6 title-gradient text-center">Team &amp; Organizers</h2>
          <div class="grid md:grid-cols-3 gap-6">
            <div class="text-center">
              <img src="https://source.unsplash.com/200x200/?person" class="w-32 h-32 rounded-full mx-auto mb-3 object-cover ring-1 ring-white/10">
              <h3 class="text-lg font-medium">Jane Doe</h3>
              <p class="text-sm text-white/70">Event Director</p>
            </div>
            <div class="text-center">
              <img src="https://source.unsplash.com/200x200/?man" class="w-32 h-32 rounded-full mx-auto mb-3 object-cover ring-1 ring-white/10">
              <h3 class="text-lg font-medium">John Smith</h3>
              <p class="text-sm text-white/70">Sports Coordinator</p>
            </div>
            <div class="text-center">
              <img src="https://source.unsplash.com/200x200/?woman" class="w-32 h-32 rounded-full mx-auto mb-3 object-cover ring-1 ring-white/10">
              <h3 class="text-lg font-medium">Alex Kim</h3>
              <p class="text-sm text-white/70">Sponsorship Manager</p>
            </div>
          </div>
        </div>
      </section>

      <!-- Contact Us -->
      <section id="contact" class="container mx-auto px-6 mt-16 mb-24 scroll-mt-24">
        <div class="max-w-5xl mx-auto glass rounded-2xl border border-white/10 ring-contrast p-8" data-animate="" style="--d:.18s;">
          <h2 class="text-3xl tracking-tight font-light mb-6 title-gradient text-center">Contact Us</h2>
          <form class="max-w-xl mx-auto space-y-4">
            <input type="text" placeholder="Your Name" class="w-full rounded-md p-3 bg-white/5 border border-white/10 focus:outline-none focus:ring-2 focus:ring-white/20">
            <input type="email" placeholder="Your Email" class="w-full rounded-md p-3 bg-white/5 border border-white/10 focus:outline-none focus:ring-2 focus:ring-white/20">
            <textarea rows="4" placeholder="Your Message" class="w-full rounded-md p-3 bg-white/5 border border-white/10 focus:outline-none focus:ring-2 focus:ring-white/20"></textarea>
            <button class="bg-white text-black px-6 py-3 rounded-lg hover:bg-opacity-90 transition w-full focus-ring">Send Message</button>
          </form>
        </div>
      </section>
    </div>

    <!-- Swiper JS -->
    <script src="https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.js"></script>

    <script>
      document.addEventListener('DOMContentLoaded', () => {
        if (window.lucide) { lucide.createIcons(); }

        // In-view observer (CSS-driven animations)
        const io = new IntersectionObserver((entries) => {
          entries.forEach((entry) => {
            if (entry.isIntersecting) {
              entry.target.classList.add('is-inview');
              io.unobserve(entry.target);
            }
          });
        }, { rootMargin: '0px 0px -10% 0px', threshold: 0.14 });
        document.querySelectorAll('[data-animate]').forEach(el => io.observe(el));

        // Sports Swiper (3D Coverflow)
        if (window.Swiper) {
          const sportsSwiper = new Swiper(".sportsSwiper", {
            effect: "coverflow",
            grabCursor: true,
            centeredSlides: true,
            slidesPerView: "auto",
            loop: true,
            coverflowEffect: {
              rotate: 30,
              stretch: 0,
              depth: 160,
              modifier: 1,
              slideShadows: true,
            },
            autoplay: {
              delay: 2500,
              disableOnInteraction: false,
            },
          });
        }
      });
    </script>
  
</body></html>