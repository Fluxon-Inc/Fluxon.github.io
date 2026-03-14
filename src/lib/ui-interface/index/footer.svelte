<script>
  import { resolve } from '$app/paths';

  const year = new Date().getFullYear();

  const nav = [
    {
      heading: 'Product',
      links: [
        { label: 'Features',   href: '/features'  },
        { label: 'Channels',   href: '/channels'  },
        { label: 'Pricing',    href: '/pricing'   },
        { label: 'Roadmap',    href: '/roadmap'   },
      ],
    },
    {
      heading: 'Company',
      links: [
        { label: 'About',    href: '/about'   },
        { label: 'Blog',     href: '/blog'    },
        { label: 'Careers',  href: '/careers' },
        { label: 'Contact',  href: '/contact' },
      ],
    },
    {
      heading: 'Support',
      links: [
        { label: 'Help Centre',  href: '/help'      },
        { label: 'Status',       href: '/status'    },
        { label: 'Community',    href: '/community' },
        { label: 'Changelog',    href: '/changelog' },
      ],
    },
    {
      heading: 'Legal',
      links: [
        { label: 'Privacy',   href: '/privacy'   },
        { label: 'Terms',     href: '/terms'     },
        { label: 'Cookies',   href: '/cookies'   },
        { label: 'Security',  href: '/security'  },
      ],
    },
  ];

  const socials = [
    {
      id: 'twitter',
      label: 'Twitter / X',
      href: 'https://x.com/FluxonInc',
    },
    {
      id: 'github',
      label: 'GitHub',
      href: 'https://github.com/Fluxon-Inc',
    },
    {
      id: 'discord',
      label: 'Discord',
      href: 'https://discord.com',
    },
  ];
</script>

<footer class="footer">
  <div class="container">

    <!-- Top row: brand + newsletter -->
    <div class="top-row">

      <!-- Brand -->
      <div class="brand">
        <a href={resolve('/')} class="logo">
          <div class="logo-mark">
            <svg width="28" height="28" viewBox="0 0 28 28" fill="none">
              <rect width="28" height="28" rx="7" fill="#2563eb"/>
              <path d="M8 7h12v3.5H11.5V13H19v3h-7.5v5H8V7z" fill="white" opacity="0.95"/>
              <rect x="13" y="13" width="7" height="3" fill="white" opacity="0.4"/>
            </svg>
          </div>
          <span>Fluxon</span>
        </a>
        <p class="brand-tagline">
          Chat that feels fast, clean,<br/>and genuinely human.
        </p>

        <!-- Socials -->
        <div class="socials">
          {#each socials as s (s.id)}
            <button
              type="button"
              aria-label={s.label}
              class="social-btn"
              onclick={() => window.open(s.href, '_blank', 'noopener,noreferrer')}
            >
              {#if s.id === 'twitter'}
                <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/>
                </svg>
              {:else if s.id === 'github'}
                <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"/>
                </svg>
              {:else}
                <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M20.317 4.37a19.791 19.791 0 00-4.885-1.515.074.074 0 00-.079.037c-.21.375-.444.864-.608 1.25a18.27 18.27 0 00-5.487 0 12.64 12.64 0 00-.617-1.25.077.077 0 00-.079-.037A19.736 19.736 0 003.677 4.37a.07.07 0 00-.032.027C.533 9.046-.32 13.58.099 18.057a.082.082 0 00.031.057 19.9 19.9 0 005.993 3.03.078.078 0 00.084-.028c.462-.63.874-1.295 1.226-1.994a.076.076 0 00-.041-.106 13.107 13.107 0 01-1.872-.892.077.077 0 01-.008-.128 10.2 10.2 0 00.372-.292.074.074 0 01.077-.01c3.928 1.793 8.18 1.793 12.062 0a.074.074 0 01.078.01c.12.098.246.198.373.292a.077.077 0 01-.006.127 12.299 12.299 0 01-1.873.892.077.077 0 00-.041.107c.36.698.772 1.362 1.225 1.993a.076.076 0 00.084.028 19.839 19.839 0 006.002-3.03.077.077 0 00.032-.054c.5-5.177-.838-9.674-3.549-13.66a.061.061 0 00-.031-.03z"/>
                </svg>
              {/if}
            </button>
          {/each}
        </div>
      </div>

      <!-- Nav columns -->
      <div class="nav-columns">
        {#each nav as col (col.heading)}
          <div class="nav-col">
            <h4 class="col-heading">{col.heading}</h4>
            <ul class="col-links">
              {#each col.links as link (link.label)}
                <!-- eslint-disable-next-line svelte/no-navigation-without-resolve -->
                <li><a href={link.href} class="col-link">{link.label}</a></li>
              {/each}
            </ul>
          </div>
        {/each}
      </div>

    </div>

    <!-- Divider -->
    <div class="divider" aria-hidden="true"></div>

    <!-- Bottom row -->
    <div class="bottom-row">
      <p class="copyright">© {year} Fluxon. All rights reserved.</p>
      <p class="made-with">
        Built with
        <svg class="heart" width="13" height="13" viewBox="0 0 24 24" fill="currentColor">
          <path d="M12 21.593c-5.63-5.539-11-10.297-11-14.402C1 3.314 3.518 1 6.318 1c1.68 0 3.293.782 4.436 2.02.357.383.73.776 1.246.776.516 0 .889-.393 1.246-.776C14.389 1.782 16.002 1 17.682 1 20.482 1 23 3.314 23 7.191c0 4.105-5.37 8.863-11 14.402z"/>
        </svg>
        for people who love good conversation.
      </p>
    </div>

  </div>
</footer>

<style>
  .footer {
    position: relative;
    border-top: 1px solid var(--border);
    background: rgba(255, 255, 255, 0.55);
    backdrop-filter: blur(12px);
    -webkit-backdrop-filter: blur(12px);
    padding: 64px 24px 40px;
  }

  .container {
    max-width: 1152px;
    margin: 0 auto;
  }

  /* ── Top row ── */
  .top-row {
    display: grid;
    grid-template-columns: 280px 1fr;
    gap: 48px;
  }

  @media (max-width: 768px) {
    .top-row { grid-template-columns: 1fr; }
    .nav-columns { grid-template-columns: repeat(2, 1fr); }
  }

  /* ── Brand ── */
  .logo {
    display: inline-flex;
    align-items: center;
    gap: 10px;
    text-decoration: none;
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 17px;
    color: var(--fg);
    margin-bottom: 16px;
  }

  .logo-mark {
    transition: transform 0.3s cubic-bezier(.34,1.56,.64,1);
  }
  .logo:hover .logo-mark {
    transform: rotate(-6deg) scale(1.08);
  }

  .brand-tagline {
    font-size: 14px;
    line-height: 1.7;
    color: var(--fg-muted);
    margin-bottom: 24px;
  }

  /* ── Socials ── */
  .socials {
    display: flex;
    gap: 8px;
  }

  .social-btn {
    width: 36px;
    height: 36px;
    border-radius: 9px;
    border: 1px solid var(--border);
    background: rgba(255,255,255,0.6);
    display: flex;
    align-items: center;
    justify-content: center;
    color: var(--fg-muted);
    text-decoration: none;
    transition: color 0.2s, background 0.2s, border-color 0.2s, transform 0.15s;
  }
  .social-btn:hover {
    color: var(--accent);
    background: var(--accent-light);
    border-color: rgba(37,99,235,0.2);
    transform: translateY(-2px);
  }

  /* ── Nav columns ── */
  .nav-columns {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 32px;
  }

  @media (max-width: 560px) {
    .nav-columns { grid-template-columns: repeat(2, 1fr); }
  }

  .col-heading {
    font-family: 'Syne', sans-serif;
    font-size: 12px;
    font-weight: 700;
    letter-spacing: 0.1em;
    color: var(--fg);
    text-transform: uppercase;
    margin-bottom: 16px;
  }

  .col-links {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .col-link {
    font-size: 14px;
    color: var(--fg-muted);
    text-decoration: none;
    transition: color 0.2s, padding-left 0.2s;
    display: inline-block;
  }
  .col-link:hover {
    color: var(--accent);
    padding-left: 4px;
  }

  /* ── Divider ── */
  .divider {
    height: 1px;
    background: var(--border);
    margin: 48px 0 28px;
  }

  /* ── Bottom row ── */
  .bottom-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 12px;
  }

  .copyright,
  .made-with {
    font-size: 13px;
    color: var(--fg-muted);
  }

  .made-with {
    display: flex;
    align-items: center;
    gap: 5px;
  }

  .heart {
    color: #ef4444;
    animation: pulse 1.8s ease-in-out infinite;
  }

  @keyframes pulse {
    0%, 100% { transform: scale(1);    opacity: 1;    }
    50%       { transform: scale(1.25); opacity: 0.85; }
  }
</style>