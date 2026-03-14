<script>
  import { onMount } from 'svelte';

  let mounted = false;
  onMount(() => {
    // Tiny delay so CSS animations feel intentional
    requestAnimationFrame(() => { mounted = true; });
  });
</script>

<section class="hero relative min-h-screen flex flex-col items-center justify-center px-6 pt-20 pb-16 overflow-hidden">

  <!-- Soft radial glow behind icon -->
  <div class="glow" aria-hidden="true"></div>

  <!-- Icon badge -->
  <div class="icon-badge glass" class:in={mounted}>
    <svg width="52" height="52" viewBox="0 0 52 52" fill="none">
      <!-- Abstract "flux" node icon -->
      <rect x="6" y="6" width="18" height="18" rx="5" fill="#2563eb" opacity="0.15"/>
      <rect x="28" y="6" width="18" height="18" rx="5" fill="#2563eb" opacity="0.35"/>
      <rect x="6" y="28" width="18" height="18" rx="5" fill="#2563eb" opacity="0.35"/>
      <rect x="28" y="28" width="18" height="18" rx="5" fill="#2563eb"/>
      <!-- connecting lines -->
      <line x1="15" y1="24" x2="15" y2="28" stroke="#2563eb" stroke-width="1.5" opacity="0.4"/>
      <line x1="37" y1="24" x2="37" y2="28" stroke="#2563eb" stroke-width="1.5" opacity="0.5"/>
      <line x1="24" y1="15" x2="28" y2="15" stroke="#2563eb" stroke-width="1.5" opacity="0.4"/>
      <line x1="24" y1="37" x2="28" y2="37" stroke="#2563eb" stroke-width="1.5" opacity="0.5"/>
    </svg>
  </div>

  <!-- Heading -->
  <h1 class="heading" class:in={mounted}>
    Fluxon
  </h1>

  <!-- Tagline -->
  <p class="tagline" class:in={mounted}>
    Built for everyone
  </p>

  <!-- Description -->
  <p class="description" class:in={mounted}>
    The platform that allows us to chat, hangout & study —<br class="hidden sm:block"/>
    so you can meet new friends & chat.
  </p>

  <!-- CTA buttons -->
  <div class="cta-row" class:in={mounted}>
    <a href="#products" class="btn-primary">
      Explore Platform
    </a>
    <a href="#contact" class="btn-ghost">
      Talk to us
    </a>
  </div>

  <!-- Scroll hint -->
  <div class="scroll-hint" class:in={mounted}>
    <span>SCROLL</span>
    <svg width="14" height="14" viewBox="0 0 14 14" fill="none">
      <path d="M7 1v12M2 8l5 5 5-5" stroke="currentColor" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round"/>
    </svg>
  </div>

</section>

<style>
  /* ── Glow orb ── */
  .glow {
    position: absolute;
    top: 18%;
    left: 50%;
    translate: -50% -50%;
    width: 520px;
    height: 320px;
    border-radius: 50%;
    background: radial-gradient(ellipse at center, rgba(37,99,235,0.12) 0%, transparent 70%);
    pointer-events: none;
    filter: blur(2px);
  }

  /* ── Icon badge ── */
  .icon-badge {
    width: 100px;
    height: 100px;
    border-radius: 24px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 36px;
    box-shadow: 0 4px 24px rgba(0,0,0,0.07), 0 1px 3px rgba(0,0,0,0.05);

    opacity: 0;
    transform: translateY(16px) scale(0.95);
    transition: opacity 0.55s cubic-bezier(.22,1,.36,1), transform 0.55s cubic-bezier(.22,1,.36,1);
  }
  .icon-badge.in {
    opacity: 1;
    transform: translateY(0) scale(1);
  }

  /* ── Heading ── */
  .heading {
    font-family: 'Syne', sans-serif;
    font-size: clamp(64px, 10vw, 112px);
    font-weight: 800;
    letter-spacing: -0.04em;
    line-height: 1;
    color: var(--fg);
    text-align: center;

    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.6s 0.1s cubic-bezier(.22,1,.36,1), transform 0.6s 0.1s cubic-bezier(.22,1,.36,1);
  }
  .heading.in { opacity: 1; transform: translateY(0); }

  /* ── Tagline ── */
  .tagline {
    margin-top: 16px;
    font-size: 12px;
    font-weight: 600;
    letter-spacing: 0.2em;
    color: var(--accent);
    text-align: center;

    opacity: 0;
    transform: translateY(12px);
    transition: opacity 0.6s 0.2s cubic-bezier(.22,1,.36,1), transform 0.6s 0.2s cubic-bezier(.22,1,.36,1);
  }
  .tagline.in { opacity: 1; transform: translateY(0); }

  /* ── Description ── */
  .description {
    margin-top: 24px;
    font-size: clamp(15px, 2vw, 17px);
    line-height: 1.7;
    color: var(--fg-muted);
    text-align: center;
    max-width: 480px;

    opacity: 0;
    transform: translateY(12px);
    transition: opacity 0.6s 0.3s cubic-bezier(.22,1,.36,1), transform 0.6s 0.3s cubic-bezier(.22,1,.36,1);
  }
  .description.in { opacity: 1; transform: translateY(0); }

  /* ── CTA row ── */
  .cta-row {
    margin-top: 40px;
    display: flex;
    gap: 12px;
    flex-wrap: wrap;
    justify-content: center;

    opacity: 0;
    transform: translateY(12px);
    transition: opacity 0.6s 0.4s cubic-bezier(.22,1,.36,1), transform 0.6s 0.4s cubic-bezier(.22,1,.36,1);
  }
  .cta-row.in { opacity: 1; transform: translateY(0); }

  .btn-primary {
    display: inline-flex;
    align-items: center;
    padding: 13px 28px;
    background: var(--accent);
    color: #fff;
    font-family: 'DM Sans', sans-serif;
    font-size: 15px;
    font-weight: 600;
    border-radius: 12px;
    text-decoration: none;
    box-shadow: 0 3px 12px rgba(37,99,235,0.32);
    transition: background 0.2s, transform 0.15s, box-shadow 0.2s;
    letter-spacing: -0.01em;
  }
  .btn-primary:hover {
    background: var(--accent-dark);
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(37,99,235,0.38);
  }
  .btn-primary:active { transform: translateY(0); }

  .btn-ghost {
    display: inline-flex;
    align-items: center;
    padding: 13px 28px;
    background: rgba(255,255,255,0.7);
    color: var(--fg);
    font-family: 'DM Sans', sans-serif;
    font-size: 15px;
    font-weight: 500;
    border-radius: 12px;
    border: 1px solid var(--border);
    text-decoration: none;
    backdrop-filter: blur(8px);
    transition: background 0.2s, transform 0.15s;
    letter-spacing: -0.01em;
  }
  .btn-ghost:hover {
    background: rgba(255,255,255,0.9);
    transform: translateY(-1px);
  }

  /* ── Scroll hint ── */
  .scroll-hint {
    position: absolute;
    bottom: 32px;
    left: 50%;
    translate: -50% 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 6px;
    color: var(--fg-muted);
    font-size: 10px;
    letter-spacing: 0.15em;
    font-weight: 500;

    opacity: 0;
    transition: opacity 0.6s 0.7s;
    animation: bob 2s 1.4s ease-in-out infinite;
  }
  .scroll-hint.in { opacity: 1; }

  @keyframes bob {
    0%, 100% { transform: translate(-50%, 0); }
    50%       { transform: translate(-50%, 5px); }
  }
</style>