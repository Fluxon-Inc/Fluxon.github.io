<script lang="ts">
	import { resolve } from '$app/paths';
</script>

<section class="relative z-10 py-24 px-6">
	<div class="max-w-6xl mx-auto">
		<div
			class="flex flex-col md:flex-row md:items-center md:justify-between gap-8 rounded-2xl px-10 py-12 border"
			style="background: var(--bg-surface); border-color: var(--border-default)"
		>
			<div class="flex flex-col gap-3 max-w-lg">
				<h2
					class="m-0 font-extrabold text-white leading-tight"
					style="font-family: var(--font-display); font-size: clamp(1.6rem, 4vw, 2.4rem); letter-spacing: -0.025em"
				>
					Ready to start chatting?
				</h2>
				<p class="m-0 font-light leading-relaxed" style="color: var(--text-secondary)">
					Create your free account and be inside a conversation in under a minute.
				</p>
			</div>

			<div class="flex items-center gap-3 shrink-0">
				<a
					href={resolve('/register')}
					class="inline-flex items-center gap-2 text-sm font-semibold text-black px-7 py-3 rounded-full no-underline transition-all duration-200 hover:-translate-y-0.5 hover:brightness-110"
					style="background: var(--accent); font-family: var(--font-display)"
				>
					Create account
					<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
						<path d="M5 12h14M12 5l7 7-7 7"/>
					</svg>
				</a>
				<a
					href={resolve('/login')}
					class="inline-flex items-center text-sm font-semibold px-7 py-3 rounded-full border no-underline transition-all duration-200 hover:bg-white/5 hover:text-white hover:border-white/20"
					style="color: var(--text-secondary); border-color: rgba(255,255,255,0.1); font-family: var(--font-display)"
				>
					Sign in
				</a>
			</div>
		</div>
	</div>
</section>