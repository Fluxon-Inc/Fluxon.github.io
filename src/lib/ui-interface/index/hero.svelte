<script lang="ts">
	import { resolve } from '$app/paths';
</script>

<section class="min-h-screen flex items-center justify-center pt-24 pb-16 relative z-10">
	<div class="flex flex-col items-center text-center gap-6 max-w-3xl w-full px-6">

		<span
			class="inline-flex items-center gap-2 rounded-full px-4 py-1.5 text-xs font-semibold uppercase tracking-widest border"
			style="color: var(--accent); background: var(--accent-dim); border-color: rgba(200,240,79,0.2); font-family: var(--font-display)"
		>
			<svg width="11" height="11" viewBox="0 0 24 24" fill="currentColor">
				<path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
			</svg>
			Real talk. Real time.
		</span>

		<h1
			class="m-0 font-extrabold leading-none text-white"
			style="font-family: var(--font-display); font-size: clamp(3rem, 9vw, 6rem); letter-spacing: -0.03em"
		>
			Chat without<br />
			<span style="color: var(--accent)">the clutter</span>
		</h1>

		<p
			class="m-0 font-light leading-relaxed max-w-[50ch]"
			style="font-size: clamp(1rem, 2vw, 1.125rem); color: var(--text-secondary)"
		>
			Fluxon is a fast, minimal chat platform for communities and friends.
			Clean interface, real conversations — nothing in the way.
		</p>

		<div class="flex items-center gap-3 flex-wrap justify-center mt-2">
			<a
				href={resolve('/register')}
				class="inline-flex items-center gap-2 text-sm font-semibold text-black px-7 py-3 rounded-full no-underline transition-all duration-200 hover:-translate-y-0.5 hover:brightness-110"
				style="background: var(--accent); font-family: var(--font-display)"
			>
				Open Fluxon
				<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
					<path d="M5 12h14M12 5l7 7-7 7"/>
				</svg>
			</a>
			<a
				href="#features"
				class="inline-flex items-center gap-2 text-sm font-semibold px-7 py-3 rounded-full border no-underline transition-all duration-200 hover:bg-white/5 hover:text-white hover:border-white/20"
				style="color: var(--text-secondary); border-color: rgba(255,255,255,0.1); font-family: var(--font-display)"
			>
				Learn more
			</a>
		</div>

	</div>
</section>