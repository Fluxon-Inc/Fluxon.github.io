<script lang="ts">
	import { resolve } from '$app/paths';
	import { onMount } from 'svelte';

	let scrolled = $state(false);

	onMount(() => {
		const handler = () => (scrolled = window.scrollY > 20);
		window.addEventListener('scroll', handler);
		return () => window.removeEventListener('scroll', handler);
	});

	const navClass = $derived(scrolled
		? 'bg-black/80 backdrop-blur-xl border-white/5'
		: 'border-transparent');
</script>

<nav class="fixed top-0 left-0 right-0 z-50 py-4 border-b transition-all duration-300 {navClass}">
	<div class="max-w-6xl mx-auto px-6 flex items-center">

		<a href={resolve('/')} class="flex items-center gap-2.5 no-underline flex-shrink-0">
			<div class="w-8 h-8 rounded-lg grid place-items-center text-black" style="background: var(--accent)">
				<svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
					<path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
				</svg>
			</div>
			<span class="font-bold text-base tracking-tight text-white" style="font-family: var(--font-display)">
				Fluxon
			</span>
		</a>

		<ul class="flex items-center gap-1 ml-auto list-none p-0 m-0 mr-4">
			<li>
				<a href="#about" class="text-sm px-3 py-2 rounded-md no-underline transition-all duration-200 hover:bg-white/5 hover:text-white" style="color: var(--text-secondary)">About</a>
			</li>
			<li>
				<a href="#features" class="text-sm px-3 py-2 rounded-md no-underline transition-all duration-200 hover:bg-white/5 hover:text-white" style="color: var(--text-secondary)">Docs</a>
			</li>
			<li>
				<a href={resolve('/register')} class="text-sm px-3 py-2 rounded-md no-underline transition-all duration-200 hover:bg-white/5 hover:text-white" style="color: var(--text-secondary)">Register</a>
			</li>
			<li>
				<a href={resolve('/login')} class="text-sm px-3 py-2 rounded-md no-underline transition-all duration-200 hover:bg-white/5 hover:text-white" style="color: var(--text-secondary)">Login</a>
			</li>
		</ul>

		<a
			href={resolve('/register')}
			class="flex-shrink-0 inline-flex items-center gap-2 text-sm font-semibold text-black px-5 py-2.5 rounded-full no-underline transition-all duration-200 hover:-translate-y-0.5 hover:brightness-110"
			style="background: var(--accent); font-family: var(--font-display)"
		>
			Get Started
			<svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
				<path d="M5 12h14M12 5l7 7-7 7"/>
			</svg>
		</a>

	</div>
</nav>