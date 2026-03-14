<script lang="ts">
	import { resolve } from '$app/paths';
	import { onMount } from 'svelte';

	let scrolled = $state(false);

	onMount(() => {
		const handler = () => (scrolled = window.scrollY > 20);
		window.addEventListener('scroll', handler);
		return () => window.removeEventListener('scroll', handler);
	});

	const navClass = $derived(
		scrolled ? 'bg-black/80 backdrop-blur-xl border-white/5' : 'border-transparent'
	);
</script>

<nav class="fixed top-0 left-0 right-0 z-50 border-b transition-all duration-300 {navClass}">
	<div class="max-w-6xl mx-auto px-8 h-16 flex items-center justify-between">

		<a href={resolve('/')} class="flex items-center gap-3 no-underline shrink-0">
			<div class="w-9 h-9 rounded-xl grid place-items-center text-white shrink-0" style="background: var(--accent)">
				<svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
					<path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
				</svg>
			</div>
			<span class="text-white font-bold text-lg tracking-tight">Fluxon</span>
		</a>

		<div class="flex items-center gap-8">
			<div class="flex items-center gap-6">
				<a href="#about" class="text-sm no-underline transition-colors duration-200 hover:text-white" style="color: var(--text-secondary)">About</a>
				<a href="#features" class="text-sm no-underline transition-colors duration-200 hover:text-white" style="color: var(--text-secondary)">Docs</a>
				<a href={resolve('/register')} class="text-sm no-underline transition-colors duration-200 hover:text-white" style="color: var(--text-secondary)">Register</a>
				<a href={resolve('/login')} class="text-sm no-underline transition-colors duration-200 hover:text-white" style="color: var(--text-secondary)">Login</a>
			</div>
			<a
				href={resolve('/register')}
				class="inline-flex items-center gap-2 text-sm font-semibold text-white px-5 py-2 rounded-full no-underline transition-all duration-200 hover:-translate-y-0.5 hover:brightness-110 shrink-0"
				style="background: var(--accent)"
			>
				Get Started
				<svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
					<path d="M5 12h14M12 5l7 7-7 7"/>
				</svg>
			</a>
		</div>

	</div>
</nav>