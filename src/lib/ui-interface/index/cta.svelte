<script lang="ts">
  import { onMount } from 'svelte';
  import { resolve } from '$app/paths';

  type Msg = { user: string; text: string; side: 'left' | 'right' };

  let messages: Msg[] = [];
  let visibleCount = 0;
  let loading = true;
  let rateLimited = false;

  //  Session rate limit 
  const SESSION_KEY = 'fluxon_cta_calls';
  const MAX_CALLS   = 5;

  function getCallCount() { return parseInt(sessionStorage.getItem(SESSION_KEY) ?? '0', 10); }
  function incrementCallCount() { sessionStorage.setItem(SESSION_KEY, String(getCallCount() + 1)); }

  // Track used openers so refresh never repeats 
  // eslint-disable-next-line svelte/prefer-svelte-reactivity
  const usedOpeners = new Set<string>();

  const fallback: Msg[][] = [
    [
      { user: 'Alex', text: 'Hey, have you tried Fluxon yet?',         side: 'left'  },
      { user: 'Sam',  text: 'Just signed up — looks really clean!',    side: 'right' },
      { user: 'Alex', text: 'Right? Zero lag, feels instant.',          side: 'left'  },
      { user: 'Sam',  text: 'Already better than what we used before.', side: 'right' },
    ],
    [
      { user: 'Alex', text: 'You joining the call later?',              side: 'left'  },
      { user: 'Sam',  text: 'Yeah, give me five minutes.',              side: 'right' },
      { user: 'Alex', text: 'No rush, we just started.',                side: 'left'  },
      { user: 'Sam',  text: 'Cool, hopping on now!',                    side: 'right' },
    ],
    [
      { user: 'Alex', text: 'Did you see the latest update?',           side: 'left'  },
      { user: 'Sam',  text: 'Yeah threads are so much better now.',     side: 'right' },
      { user: 'Alex', text: 'Exactly what we needed.',                  side: 'left'  },
      { user: 'Sam',  text: 'Ship it honestly.',                        side: 'right' },
    ],
  ];
  let fallbackIndex = 0;

  function getUnusedFallback(): Msg[] {
    for (let i = 0; i < fallback.length; i++) {
      const idx = (fallbackIndex + i) % fallback.length;
      const key = fallback[idx][0].text;
      if (!usedOpeners.has(key)) {
        fallbackIndex = (idx + 1) % fallback.length;
        usedOpeners.add(key);
        return fallback[idx];
      }
    }
    usedOpeners.clear();
    usedOpeners.add(fallback[0][0].text);
    fallbackIndex = 1;
    return fallback[0];
  }

  async function loadMessages() {
    loading      = true;
    visibleCount = 0;
    messages     = [];

    if (getCallCount() >= MAX_CALLS) {
      rateLimited = true;
      messages    = getUnusedFallback();
      loading     = false;
      revealMessages();
      return;
    }

    try {
      incrementCallCount();

      const res = await fetch('/api/chat-messages', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ exclude: Array.from(usedOpeners) }),
      });

      if (res.status === 429) {
        rateLimited = true;
        messages    = getUnusedFallback();
      } else if (!res.ok) {
        messages = getUnusedFallback();
      } else {
        const data      = await res.json();
        const newMsgs: Msg[] = data.messages ?? [];
        const opener    = newMsgs[0]?.text ?? '';

        if (usedOpeners.has(opener)) {
          messages = getUnusedFallback();
        } else {
          usedOpeners.add(opener);
          messages = newMsgs;
        }
      }
    } catch {
      messages = getUnusedFallback();
    } finally {
      loading = false;
      revealMessages();
    }
  }

  async function revealMessages() {
    for (let i = 0; i < messages.length; i++) {
      await new Promise<void>(r => setTimeout(r, i === 0 ? 400 : 750));
      visibleCount = i + 1;
    }
  }

  onMount(() => { loadMessages(); });
</script>

<section class="cta-section">
  <div class="container">
    <div class="cta-card glass">

      <div class="blob blob-1" aria-hidden="true"></div>
      <div class="blob blob-2" aria-hidden="true"></div>

      <!-- Left: live AI chat preview -->
      <div class="cta-visual" aria-hidden="true">
        <div class="phone-frame">

          <!-- Chrome bar -->
          <div class="frame-header">
            <div class="frame-dots">
              <span></span><span></span><span></span>
            </div>
            <span class="frame-title">fluxon · general</span>
            <div class="frame-status">
              <span class="online-ring"></span>
              <span class="online-label">2 online</span>
            </div>
          </div>

          <!-- Messages -->
          <div class="frame-body">
            {#if loading}
              {#each [1,2,3,4] as n (n)}
                <div class="skeleton-row" class:sk-right={n % 2 === 0}>
                  <div class="sk-avatar"></div>
                  <div class="sk-bubble" style="width:{52 + (n * 11) % 28}%"></div>
                </div>
              {/each}
            {:else}
              {#each messages.slice(0, visibleCount) as msg, i (i)}
                <div class="msg" class:right={msg.side === 'right'}>
                  {#if msg.side === 'left'}
                    <div class="avatar av-blue">{msg.user[0]}</div>
                  {/if}
                  <div class="bubble" class:bubble-right={msg.side === 'right'} class:bubble-left={msg.side === 'left'}>
                    <span class="msg-author">{msg.user}</span>
                    <p>{msg.text}</p>
                  </div>
                  {#if msg.side === 'right'}
                    <div class="avatar av-purple">{msg.user[0]}</div>
                  {/if}
                </div>
              {/each}

              {#if visibleCount < messages.length}
                <div class="msg" class:right={messages[visibleCount]?.side === 'right'}>
                  {#if messages[visibleCount]?.side === 'left'}
                    <div class="avatar av-blue">{messages[visibleCount]?.user[0]}</div>
                  {/if}
                  <div class="typing-bubble">
                    <span class="dot"></span><span class="dot"></span><span class="dot"></span>
                  </div>
                  {#if messages[visibleCount]?.side === 'right'}
                    <div class="avatar av-purple">{messages[visibleCount]?.user[0]}</div>
                  {/if}
                </div>
              {/if}
            {/if}
          </div>

          <!-- Footer -->
          <div class="frame-footer">
            <button class="refresh-btn" onclick={loadMessages} disabled={loading} aria-label="Generate new conversation">
              <svg width="11" height="11" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" class:spin={loading}>
                <path d="M21 2v6h-6"/><path d="M3 12a9 9 0 0 1 15-6.7L21 8"/>
                <path d="M3 22v-6h6"/><path d="M21 12a9 9 0 0 1-15 6.7L3 16"/>
              </svg>
              {rateLimited ? 'showing preview' : 'new conversation'}
            </button>
          </div>

        </div>
      </div>

      <!-- Right: CTA content -->
      <div class="cta-content">
        <span class="eyebrow">GET STARTED</span>
        <h2 class="cta-title">A platform built<br/>for real conversation.</h2>
        <p class="cta-sub">
          Fluxon is a passion project focused on making chat feel
          fast, clean, and human. Jump in and see what we're building.
        </p>
        <div class="cta-actions">
          <!-- eslint-disable-next-line svelte/no-navigation-without-resolve -->
          <a href={resolve('/login')} class="btn-primary">
            Start Chatting
            <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M5 12h14M12 5l7 7-7 7"/>
            </svg>
          </a>
          <a href="#contact" class="btn-ghost">Get in Touch</a>
        </div>
      </div>

    </div>
  </div>
</section>

<style>
  .cta-section { padding: 64px 24px 96px; }
  .container { max-width: 1100px; margin: 0 auto; }

  .cta-card {
    position: relative; overflow: hidden; border-radius: 28px;
    border: 1px solid rgba(37,99,235,0.13);
    box-shadow: 0 8px 48px rgba(37,99,235,0.07), 0 1px 3px rgba(0,0,0,0.04);
    display: grid; grid-template-columns: 1fr 1fr;
    align-items: center; min-height: 380px;
  }
  @media (max-width: 768px) {
    .cta-card { grid-template-columns: 1fr; }
    .cta-visual { display: none; }
    .cta-content { padding: 48px 32px !important; align-items: center; text-align: center; }
  }

  .blob { position: absolute; border-radius: 50%; filter: blur(64px); pointer-events: none; z-index: 0; }
  .blob-1 { width: 280px; height: 280px; background: rgba(37,99,235,0.09);  top: -80px;    left: -40px;  }
  .blob-2 { width: 200px; height: 200px; background: rgba(124,58,237,0.07); bottom: -50px; right: -20px; }

  .cta-visual {
    position: relative; z-index: 1;
    display: flex; align-items: center; justify-content: center;
    padding: 36px 16px 36px 40px;
  }

  .phone-frame {
    width: 100%; max-width: 300px; border-radius: 20px; overflow: hidden;
    background: rgba(248,250,252,0.95); border: 1px solid rgba(0,0,0,0.09);
    box-shadow: 0 2px 4px rgba(0,0,0,0.04), 0 8px 24px rgba(0,0,0,0.09);
    display: flex; flex-direction: column;
  }

  .frame-header {
    display: flex; align-items: center; gap: 8px;
    padding: 10px 14px; background: rgba(255,255,255,0.98);
    border-bottom: 1px solid rgba(0,0,0,0.07); flex-shrink: 0;
  }
  .frame-dots { display: flex; gap: 4px; flex-shrink: 0; }
  .frame-dots span { width: 8px; height: 8px; border-radius: 50%; }
  .frame-dots span:nth-child(1) { background: #f87171; }
  .frame-dots span:nth-child(2) { background: #fbbf24; }
  .frame-dots span:nth-child(3) { background: #34d399; }
  .frame-title { flex: 1; font-size: 11px; font-weight: 600; color: var(--fg-muted); text-align: center; }
  .frame-status { display: flex; align-items: center; gap: 4px; flex-shrink: 0; }
  .online-ring {
    width: 7px; height: 7px; border-radius: 50%; background: #22c55e;
    animation: pulseGreen 2s ease-in-out infinite;
  }
  .online-label { font-size: 10px; color: #22c55e; font-weight: 600; }

  @keyframes pulseGreen {
    0%, 100% { box-shadow: 0 0 0 0 rgba(34,197,94,0.4); }
    50%       { box-shadow: 0 0 0 4px rgba(34,197,94,0); }
  }

  .frame-body {
    padding: 14px 12px; display: flex; flex-direction: column;
    gap: 10px; min-height: 216px; flex: 1;
  }

  .msg { display: flex; align-items: flex-end; gap: 7px; animation: msgIn 0.35s cubic-bezier(.22,1,.36,1) both; }
  .msg.right { flex-direction: row-reverse; }

  @keyframes msgIn {
    from { opacity: 0; transform: translateY(6px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  .avatar {
    width: 26px; height: 26px; border-radius: 50%;
    font-size: 10px; font-weight: 700;
    display: flex; align-items: center; justify-content: center; flex-shrink: 0;
  }
  .av-blue   { background: #dbeafe; color: #2563eb; border: 1.5px solid rgba(37,99,235,0.2); }
  .av-purple { background: #ede9fe; color: #7c3aed; border: 1.5px solid rgba(124,58,237,0.2); }

  .bubble { max-width: calc(100% - 40px); padding: 7px 11px; box-shadow: 0 1px 3px rgba(0,0,0,0.06); }
  .bubble-left  { background: #fff; border: 1px solid rgba(0,0,0,0.07); border-radius: 14px 14px 14px 3px; }
  .bubble-right { background: var(--accent); border-radius: 14px 14px 3px 14px; box-shadow: 0 2px 8px rgba(37,99,235,0.22); }

  .msg-author { display: block; font-size: 9.5px; font-weight: 600; margin-bottom: 2px; letter-spacing: 0.01em; }
  .bubble-left  .msg-author { color: var(--fg-muted); }
  .bubble-right .msg-author { color: rgba(255,255,255,0.6); }
  .bubble p { margin: 0; font-size: 12.5px; line-height: 1.4; }
  .bubble-left  p { color: var(--fg); }
  .bubble-right p { color: #fff; }

  .typing-bubble {
    display: flex; align-items: center; gap: 4px;
    background: #fff; border: 1px solid rgba(0,0,0,0.07);
    border-radius: 14px 14px 14px 3px; padding: 9px 13px;
    box-shadow: 0 1px 3px rgba(0,0,0,0.06);
  }
  .dot { width: 5px; height: 5px; border-radius: 50%; background: #94a3b8; animation: dotBounce 1.3s ease-in-out infinite; }
  .dot:nth-child(2) { animation-delay: 0.18s; }
  .dot:nth-child(3) { animation-delay: 0.36s; }

  @keyframes dotBounce {
    0%, 60%, 100% { transform: translateY(0);   opacity: 0.35; }
    30%            { transform: translateY(-4px); opacity: 1; }
  }

  .skeleton-row { display: flex; align-items: center; gap: 8px; animation: shimmer 1.5s ease-in-out infinite; }
  .skeleton-row.sk-right { flex-direction: row-reverse; }
  .sk-avatar { width: 26px; height: 26px; border-radius: 50%; background: #e2e8f0; flex-shrink: 0; }
  .sk-bubble { height: 36px; border-radius: 12px; background: #e2e8f0; }

  @keyframes shimmer {
    0%, 100% { opacity: 1; }
    50%       { opacity: 0.45; }
  }

  .frame-footer {
    padding: 8px 12px 10px; border-top: 1px solid rgba(0,0,0,0.06);
    background: rgba(255,255,255,0.9); display: flex; justify-content: center;
  }
  .refresh-btn {
    display: inline-flex; align-items: center; gap: 5px;
    font-size: 10.5px; font-weight: 500; color: var(--fg-muted);
    background: none; border: none; cursor: pointer;
    padding: 4px 8px; border-radius: 6px; transition: color 0.15s, background 0.15s;
  }
  .refresh-btn:hover:not(:disabled) { color: var(--accent); background: var(--accent-light); }
  .refresh-btn:disabled { opacity: 0.4; cursor: not-allowed; }
  .spin { animation: spinIcon 0.7s linear infinite; }
  @keyframes spinIcon { to { transform: rotate(360deg); } }

  .cta-content {
    position: relative; z-index: 1;
    padding: 48px 48px 48px 28px;
    display: flex; flex-direction: column; align-items: flex-start;
  }
  .eyebrow { font-size: 11px; font-weight: 600; letter-spacing: 0.2em; color: var(--accent); margin-bottom: 16px; }
  .cta-title {
    font-family: 'Syne', sans-serif; font-size: clamp(26px, 3.2vw, 42px);
    font-weight: 800; letter-spacing: -0.03em; line-height: 1.1; color: var(--fg); margin-bottom: 18px;
  }
  .cta-sub { font-size: 15px; line-height: 1.7; color: var(--fg-muted); max-width: 320px; margin-bottom: 36px; }
  .cta-actions { display: flex; gap: 12px; flex-wrap: wrap; }

  .btn-primary {
    display: inline-flex; align-items: center; gap: 8px;
    padding: 13px 26px; background: var(--accent); color: #fff;
    font-size: 14.5px; font-weight: 600; border-radius: 11px; text-decoration: none;
    box-shadow: 0 3px 12px rgba(37,99,235,0.32); letter-spacing: -0.01em;
    transition: background 0.18s, transform 0.15s, box-shadow 0.18s;
  }
  .btn-primary:hover { background: var(--accent-dark); transform: translateY(-2px); box-shadow: 0 7px 20px rgba(37,99,235,0.38); }
  .btn-primary svg { transition: transform 0.18s; }
  .btn-primary:hover svg { transform: translateX(3px); }

  .btn-ghost {
    display: inline-flex; align-items: center; padding: 13px 26px;
    background: rgba(255,255,255,0.65); color: var(--fg); font-size: 14.5px;
    font-weight: 500; border-radius: 11px; border: 1px solid var(--border);
    text-decoration: none; backdrop-filter: blur(8px); letter-spacing: -0.01em;
    transition: background 0.18s, transform 0.15s;
  }
  .btn-ghost:hover { background: rgba(255,255,255,0.92); transform: translateY(-1px); }
</style>