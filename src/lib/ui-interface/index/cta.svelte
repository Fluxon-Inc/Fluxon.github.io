<script lang="ts">
	import { resolve } from '$app/paths';
</script>

<section class="relative z-10 py-12 px-8">
	<div class="max-w-6xl mx-auto">
		<div
			class="flex flex-col md:flex-row md:items-center md:justify-between gap-8 rounded-2xl px-10 py-10 border"
			style="background: var(--bg-surface); border-color: var(--border-default)"
		>
			<div class="flex flex-col gap-2">
				<h2 class="text-white font-black m-0 leading-tight" style="font-size: clamp(1.75rem, 3vw, 2.25rem); letter-spacing: -0.025em">
					Ready to start chatting?
				</h2>
				<p class="m-0 font-light" style="color: var(--text-secondary); font-size: 0.95rem; max-width: 44ch">
					Create your free account and be inside a conversation in under a minute.
				</p>
			</div>

			<div class="flex items-center gap-3 shrink-0">
				<a
					href={resolve('/register')}
					class="inline-flex items-center gap-2 font-semibold text-white text-sm px-6 py-3 rounded-full no-underline transition-all duration-200 hover:-translate-y-0.5 hover:brightness-110"
					style="background: var(--accent)"
				>
					Create account
					<svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
						<path d="M5 12h14M12 5l7 7-7 7"/>
					</svg>
				</a>
				<a
					href={resolve('/login')}
					class="inline-flex items-center font-semibold text-sm px-6 py-3 rounded-full border no-underline transition-all duration-200 hover:bg-white/5 hover:text-white hover:border-white/20"
					style="color: var(--text-secondary); border-color: rgba(255,255,255,0.1)"
				>
					Sign in
				</a>
			</div>
		</div>
	</div>
</section>