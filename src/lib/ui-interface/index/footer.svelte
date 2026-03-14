<script lang="ts">
	import { resolve } from '$app/paths';

	const year = new Date().getFullYear();
</script>

<footer class="relative z-10 border-t px-6 py-12" style="border-color: var(--border-subtle)">
	<div class="max-w-6xl mx-auto flex flex-col md:flex-row md:items-center md:justify-between gap-8">

		<div class="flex flex-col gap-3">
			<a href={resolve('/')} class="flex items-center gap-2.5 no-underline w-fit">
				<div class="w-7 h-7 rounded-lg grid place-items-center text-black" style="background: var(--accent)">
					<svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor">
						<path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
					</svg>
				</div>
				<span class="font-bold text-white text-sm" style="font-family: var(--font-display)">Fluxon</span>
			</a>
			<p class="m-0 text-xs" style="color: var(--text-muted)">© {year} Fluxon-Inc. All rights reserved.</p>
		</div>

		<nav class="flex flex-wrap gap-x-6 gap-y-2">
			<a href="#about"                class="text-sm no-underline transition-colors duration-200 hover:text-white" style="color: var(--text-muted)">About</a>
			<a href="#features"             class="text-sm no-underline transition-colors duration-200 hover:text-white" style="color: var(--text-muted)">Docs</a>
			<a href={resolve('/register')}  class="text-sm no-underline transition-colors duration-200 hover:text-white" style="color: var(--text-muted)">Register</a>
			<a href={resolve('/login')}     class="text-sm no-underline transition-colors duration-200 hover:text-white" style="color: var(--text-muted)">Login</a>
		</nav>

	</div>
</footer>