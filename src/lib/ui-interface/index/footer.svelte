<script lang="ts">
	import { resolve } from '$app/paths';

	const year = new Date().getFullYear();
</script>

<footer class="relative z-10 px-8 py-10 mt-8" style="border-top: 1px solid var(--border-subtle)">
	<div class="max-w-6xl mx-auto flex flex-col md:flex-row md:items-center md:justify-between gap-6">

		<div class="flex flex-col gap-2">
			<a href={resolve('/')} class="flex items-center gap-2.5 no-underline w-fit">
				<div class="w-8 h-8 rounded-lg grid place-items-center text-white shrink-0" style="background: var(--accent)">
					<svg width="15" height="15" viewBox="0 0 24 24" fill="currentColor">
						<path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
					</svg>
				</div>
				<span class="font-bold text-white text-base">Fluxon</span>
			</a>
			<p class="m-0 text-xs" style="color: var(--text-muted)">© {year} Fluxon-Inc. All rights reserved.</p>
		</div>

		<div class="flex items-center gap-6">
			<a href="#about" class="text-sm no-underline transition-colors duration-200 hover:text-white" style="color: var(--text-muted)">About</a>
			<a href="#features" class="text-sm no-underline transition-colors duration-200 hover:text-white" style="color: var(--text-muted)">Docs</a>
			<a href={resolve('/register')} class="text-sm no-underline transition-colors duration-200 hover:text-white" style="color: var(--text-muted)">Register</a>
			<a href={resolve('/login')} class="text-sm no-underline transition-colors duration-200 hover:text-white" style="color: var(--text-muted)">Login</a>
		</div>

	</div>
</footer>