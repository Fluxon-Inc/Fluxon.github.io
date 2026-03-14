<script>
  import { onMount } from 'svelte';
  import { resolve } from '$app/paths';

  let scrolled = false;
  let mobileOpen = false;

  onMount(() => {
    const handler = () => { scrolled = window.scrollY > 10; };
    window.addEventListener('scroll', handler, { passive: true });
    return () => window.removeEventListener('scroll', handler);
  });

  const links = ['Products', 'About', 'Docs', 'Services'];
</script>

<header class="navbar" class:scrolled>
  <div class="navbar-inner">

    <!-- Logo -->
    <a href={resolve('/')} class="logo">
      <div class="logo-icon">
        <svg width="20" height="20" viewBox="0 0 28 28" fill="none">
          <rect width="28" height="28" rx="7" fill="#2563eb"/>
          <path d="M8 7h12v3.5H11.5V13H19v3h-7.5v5H8V7z" fill="white" opacity="0.95"/>
          <rect x="13" y="13" width="7" height="3" fill="white" opacity="0.4"/>
        </svg>
      </div>
      <span class="logo-name">Fluxon</span>
    </a>

    <!-- Desktop nav -->
    <nav class="desktop-nav" aria-label="Main navigation">
      <ul>
        {#each links as link (link)}
          <li>
            <a href={`#${link.toLowerCase()}`} class="nav-link">{link}</a>
          </li>
        {/each}
      </ul>
    </nav>

    <!-- Desktop CTA -->
    <div class="desktop-cta">
      <a href="#contact" class="btn-cta">Get in Touch</a>
    </div>

    <!-- Mobile hamburger -->
    <button
      class="hamburger"
      class:open={mobileOpen}
      aria-label="Toggle menu"
      aria-expanded={mobileOpen}
      onclick={() => (mobileOpen = !mobileOpen)}
    >
      <span></span>
      <span></span>
      <span></span>
    </button>

  </div>

  <!-- Mobile drawer -->
  {#if mobileOpen}
    <div class="mobile-drawer" role="navigation" aria-label="Mobile navigation">
      {#each links as link (link)}
        <!-- eslint-disable-next-line svelte/no-navigation-without-resolve -->
        <a
          href={`#${link.toLowerCase()}`}
          class="mobile-link"
          onclick={() => (mobileOpen = false)}
        >{link}</a>
      {/each}
      <a href="#contact" class="btn-cta mobile-cta">Contact</a>
    </div>
  {/if}
</header>

<style>
  /* ── Shell ── */
  .navbar {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 100;
    transition: background 0.25s ease, box-shadow 0.25s ease;
  }

  .navbar.scrolled {
    background: rgba(240, 242, 245, 0.88);
    backdrop-filter: blur(18px);
    -webkit-backdrop-filter: blur(18px);
    box-shadow: 0 1px 0 rgba(0, 0, 0, 0.07);
  }

  /* ── Inner layout ── */
  .navbar-inner {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
    max-width: 1280px;
    margin: 0 auto;
    padding: 0 32px;
    height: 64px;
    box-sizing: border-box;
  }

  /* ── Logo ── */
  .logo {
    display: flex;
    align-items: center;
    gap: 10px;
    text-decoration: none;
    flex-shrink: 0;
  }

  .logo-icon {
    width: 36px;
    height: 36px;
    border-radius: 9px;
    background: #fff;
    border: 1px solid rgba(0,0,0,0.09);
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 1px 4px rgba(0,0,0,0.07);
    transition: transform 0.3s cubic-bezier(.34,1.56,.64,1);
  }
  .logo:hover .logo-icon {
    transform: rotate(-6deg) scale(1.07);
  }

  .logo-name {
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 17px;
    color: var(--fg);
    letter-spacing: -0.02em;
  }

  /* ── Desktop nav ── */
  .desktop-nav {
    display: flex;
    align-items: center;
  }

  .desktop-nav ul {
    list-style: none;
    margin: 0;
    padding: 0;
    display: flex;
    align-items: center;
    gap: 36px;
  }

  .nav-link {
    font-size: 15px;
    font-weight: 400;
    color: var(--fg-muted);
    text-decoration: none;
    transition: color 0.18s;
    position: relative;
  }
  .nav-link::after {
    content: '';
    position: absolute;
    left: 0;
    bottom: -3px;
    width: 0;
    height: 1.5px;
    background: var(--accent);
    transition: width 0.22s ease;
  }
  .nav-link:hover {
    color: var(--fg);
  }
  .nav-link:hover::after {
    width: 100%;
  }

  /* ── CTA button ── */
  .desktop-cta {
    flex-shrink: 0;
  }

  .btn-cta {
    display: inline-flex;
    align-items: center;
    padding: 10px 22px;
    background: var(--accent);
    color: #fff;
    font-size: 14.5px;
    font-weight: 600;
    border-radius: 10px;
    text-decoration: none;
    letter-spacing: -0.01em;
    box-shadow: 0 2px 10px rgba(37,99,235,0.28);
    transition: background 0.18s, transform 0.15s, box-shadow 0.18s;
    white-space: nowrap;
  }
  .btn-cta:hover {
    background: var(--accent-dark);
    transform: translateY(-1px);
    box-shadow: 0 4px 16px rgba(37,99,235,0.36);
  }
  .btn-cta:active {
    transform: translateY(0);
  }

  /* ── Hamburger ── */
  .hamburger {
    display: none;
    flex-direction: column;
    justify-content: center;
    gap: 5px;
    width: 36px;
    height: 36px;
    background: none;
    border: none;
    cursor: pointer;
    padding: 6px;
    border-radius: 8px;
    transition: background 0.15s;
  }
  .hamburger:hover {
    background: rgba(0,0,0,0.05);
  }
  .hamburger span {
    display: block;
    width: 100%;
    height: 2px;
    background: var(--fg);
    border-radius: 2px;
    transition: transform 0.25s, opacity 0.25s;
    transform-origin: center;
  }
  .hamburger.open span:nth-child(1) { transform: translateY(7px) rotate(45deg); }
  .hamburger.open span:nth-child(2) { opacity: 0; transform: scaleX(0); }
  .hamburger.open span:nth-child(3) { transform: translateY(-7px) rotate(-45deg); }

  /* ── Mobile drawer ── */
  .mobile-drawer {
    display: flex;
    flex-direction: column;
    gap: 4px;
    padding: 12px 24px 20px;
    background: rgba(240, 242, 245, 0.96);
    backdrop-filter: blur(18px);
    -webkit-backdrop-filter: blur(18px);
    border-top: 1px solid rgba(0,0,0,0.07);
  }

  .mobile-link {
    font-size: 15px;
    font-weight: 500;
    color: var(--fg-muted);
    text-decoration: none;
    padding: 10px 4px;
    border-bottom: 1px solid rgba(0,0,0,0.05);
    transition: color 0.15s;
  }
  .mobile-link:hover { color: var(--fg); }

  .mobile-cta {
    margin-top: 12px;
    justify-content: center;
  }

  /* ── Responsive breakpoints ── */
  @media (max-width: 768px) {
    .desktop-nav,
    .desktop-cta {
      display: none;
    }
    .hamburger {
      display: flex;
    }
    .navbar-inner {
      padding: 0 20px;
    }
  }
</style>