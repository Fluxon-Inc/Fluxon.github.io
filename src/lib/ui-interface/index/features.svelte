<script>
  const features = [
    {
      id: 'realtime',
      title: 'Real-time Messaging',
      description: "Messages appear instantly — no refresh, no delay. Fluxon keeps every conversation feeling live and responsive no matter where you are.",
    },
    {
      id: 'channels',
      title: 'Channels & Threads',
      description: "Organise conversations into channels and keep discussions focused with threaded replies. No more losing context in a wall of messages.",
    },
    {
      id: 'presence',
      title: 'Presence & Status',
      description: "See who's online, away, or busy at a glance. Typing indicators and read receipts make every chat feel natural and human.",
    },
    {
      id: 'privacy',
      title: 'Private & Secure',
      description: "Your conversations stay yours. Fluxon is built with privacy in mind — direct messages, group chats, and everything in between.",
    },
  ];
</script>

<section class="features-section">
  <div class="container">

    <!-- Header -->
    <div class="section-header">
      <span class="eyebrow">WHAT WE OFFER</span>
      <h2 class="section-title">Everything you need<br/>to chat, connect & vibe.</h2>
      <p class="section-sub">
        Fluxon is built around real conversations — fast, organised, and genuinely enjoyable to use.
      </p>
    </div>

    <!-- Cards grid -->
    <div class="cards-grid">
      {#each features as feature, i (feature.id)}
        <div class="card" style="--delay: {i * 80}ms">

          <div class="card-icon">
            {#if feature.id === 'realtime'}
              <!-- Lightning bolt / instant -->
              <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                <path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z"/>
              </svg>
            {:else if feature.id === 'channels'}
              <!-- Chat bubbles / channels -->
              <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
              </svg>
            {:else if feature.id === 'presence'}
              <!-- Users / presence -->
              <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                <circle cx="9" cy="7" r="4"/>
                <path d="M3 21v-2a4 4 0 0 1 4-4h4a4 4 0 0 1 4 4v2"/>
                <path d="M16 3.13a4 4 0 0 1 0 7.75"/>
                <path d="M21 21v-2a4 4 0 0 0-3-3.85"/>
              </svg>
            {:else}
              <!-- Lock / privacy -->
              <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                <rect x="3" y="11" width="18" height="11" rx="2" ry="2"/>
                <path d="M7 11V7a5 5 0 0 1 10 0v4"/>
              </svg>
            {/if}
          </div>

          <h3 class="card-title">{feature.title}</h3>
          <p class="card-body">{feature.description}</p>
        </div>
      {/each}
    </div>

  </div>
</section>

<style>
  .features-section {
    padding: 96px 24px;
    position: relative;
  }

  .container {
    max-width: 1152px;
    margin: 0 auto;
  }

  .section-header {
    text-align: center;
    margin-bottom: 64px;
  }

  .eyebrow {
    display: inline-block;
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.2em;
    color: var(--accent);
    margin-bottom: 16px;
  }

  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: clamp(32px, 5vw, 52px);
    font-weight: 800;
    letter-spacing: -0.03em;
    line-height: 1.1;
    color: var(--fg);
    margin-bottom: 20px;
  }

  .section-sub {
    font-size: 16px;
    color: var(--fg-muted);
    max-width: 480px;
    margin: 0 auto;
    line-height: 1.65;
  }

  .cards-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 20px;
  }

  @media (max-width: 1024px) {
    .cards-grid { grid-template-columns: repeat(2, 1fr); }
  }
  @media (max-width: 560px) {
    .cards-grid { grid-template-columns: 1fr; }
  }

  .card {
    background: rgba(255, 255, 255, 0.75);
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    border: 1px solid var(--border);
    border-radius: 18px;
    padding: 32px 28px;
    display: flex;
    flex-direction: column;
    gap: 16px;
    transition: transform 0.25s cubic-bezier(.22,1,.36,1), box-shadow 0.25s, border-color 0.25s;
    animation: fadeUp 0.5s var(--delay, 0ms) both;
  }

  .card:hover {
    transform: translateY(-4px);
    box-shadow: 0 12px 32px rgba(0,0,0,0.08);
    border-color: rgba(37,99,235,0.18);
  }

  .card-icon {
    width: 46px;
    height: 46px;
    border-radius: 12px;
    background: var(--accent-light);
    color: var(--accent);
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
  }

  .card-title {
    font-family: 'Syne', sans-serif;
    font-size: 17px;
    font-weight: 700;
    letter-spacing: -0.02em;
    color: var(--fg);
  }

  .card-body {
    font-size: 14.5px;
    line-height: 1.7;
    color: var(--fg-muted);
    flex: 1;
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(18px); }
    to   { opacity: 1; transform: translateY(0); }
  }
</style>