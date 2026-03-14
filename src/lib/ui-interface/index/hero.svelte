<script lang="ts">
	import { resolve } from '$app/paths';
</script>

<section class="min-h-screen flex flex-col items-center justify-center pt-16 pb-16 relative z-10 px-6 text-center">

	<div
		class="inline-flex items-center gap-2 rounded-full px-4 py-1.5 text-xs font-semibold uppercase tracking-widest border mb-8"
		style="color: var(--accent); background: var(--accent-dim); border-color: rgba(79,142,240,0.25)"
	>
		<svg width="11" height="11" viewBox="0 0 24 24" fill="currentColor">
			<path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
		</svg>
		Real talk. Real time.
	</div>

	<h1
		class="font-black text-white m-0 mb-6 leading-none"
		style="font-size: clamp(3.5rem, 10vw, 7rem); letter-spacing: -0.04em"
	>
		Chat without<br />
		<span style="color: var(--accent)">the clutter</span>
	</h1>

	<p
		class="font-light leading-relaxed mb-10 mx-auto"
		style="font-size: clamp(1rem, 2vw, 1.2rem); color: var(--text-secondary); max-width: 48ch"
	>
		Fluxon is a fast, minimal chat platform for communities and friends.
		Clean interface, real conversations — nothing in the way.
	</p>

	<div class="flex items-center gap-4 flex-wrap justify-center">
		<a
			href={resolve('/register')}
			class="inline-flex items-center gap-2 font-semibold text-white px-8 py-3.5 rounded-full no-underline transition-all duration-200 hover:-translate-y-0.5 hover:brightness-110"
			style="background: var(--accent); font-size: 0.95rem"
		>
			Open Fluxon
			<svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
				<path d="M5 12h14M12 5l7 7-7 7"/>
			</svg>
		</a>
		<a
			href="#features"
			class="inline-flex items-center font-semibold px-8 py-3.5 rounded-full border no-underline transition-all duration-200 hover:bg-white/5 hover:text-white hover:border-white/20"
			style="color: var(--text-secondary); border-color: rgba(255,255,255,0.12); font-size: 0.95rem"
		>
			Learn more
		</a>
	</div>

	<div class="absolute bottom-8 flex flex-col items-center gap-2" style="color: var(--text-muted)">
		<span class="text-xs uppercase tracking-widest">Scroll</span>
		<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
			<path d="M12 5v14M5 12l7 7 7-7"/>
		</svg>
	</div>

</section>