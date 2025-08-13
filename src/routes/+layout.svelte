<script lang="ts">
	import '../app.css';
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();

	import '../app.css';

	import { onMount } from 'svelte';
	import { page } from '$app/stores';
	import { derived } from 'svelte/store';
	import { goto } from '$app/navigation';

	let previousScrollY = 0;
	let showHeader = $state(true);

	// Scroll-based header toggle
	function handleScroll() {
		const currentScrollY = window.scrollY;
		showHeader = currentScrollY < previousScrollY;
		previousScrollY = currentScrollY;
	}

	function closeSideBar() {
		const drawerToggle = document.getElementById('my-drawer');
		// @ts-ignore
		if (drawerToggle) {
			drawerToggle.checked = false;
		}
	}

	onMount(() => {
		window.addEventListener('scroll', handleScroll);
		return () => window.removeEventListener('scroll', handleScroll);
	});

	const currentPath: any = derived(page, ($page) => $page.url.pathname);
</script>

<svelte:head>
	<link rel="icon" href={'/Screenshot from 2025-08-04 09-03-32.png'} />
</svelte:head>

<div class="min-h-screen w-screen select-none">
	<div class="fixed top-35 right-0 z-200 mr-4">
		<input type="checkbox" value="dark" class="theme-controller toggle text-[#FF9500]" />
	</div>

	<!-- NAVIGATION BAR -->
	<nav
		class="fixed top-0 left-0 z-50 hidden w-full justify-between gap-5 rounded-b-4xl bg-[#1F1F1F] p-4 px-15 transition-colors transition-transform duration-300 sm:flex [data-theme=dark]:bg-[#FF9500]"
		class:translate-y-[-100%]={!showHeader}
	>
		<div class="flex items-center justify-center gap-2">
			<img src="/Screenshot from 2025-08-04 09-03-32.png" class="h-15 w-15 rounded-full" alt="" />
			<!-- svelte-ignore a11y_invalid_attribute -->
			<a href="#"
				><h1 class="text-2xl font-bold text-white">
					Proxi<span class="text-[#FF9500]">Feast</span>
				</h1></a
			>
		</div>

		<div class="flex gap-2 font-bold text-white">
			<a href="/">
				<button
					class="btn btn-ghost"
					class:bg-[#FF9500]={$currentPath === '/'}
					class:text-black={$currentPath === '/'}
				>
					Home
				</button>
			</a>
			<a href="/about">
				<button
					class="btn btn-ghost"
					class:bg-[#FF9500]={$currentPath === '/about'}
					class:text-black={$currentPath === '/about'}
				>
					About
				</button>
			</a>
			<a href="/services">
				<button
					class="btn btn-ghost"
					class:bg-[#FF9500]={$currentPath === '/services'}
					class:text-black={$currentPath === '/services'}
				>
					Services
				</button>
			</a>
			<a href="/pricing">
				<button
					class="btn btn-ghost"
					class:bg-[#FF9500]={$currentPath === '/pricing'}
					class:text-black={$currentPath === '/pricing'}
				>
					Pricing
				</button>
			</a>
			<a href="/contact">
				<button
					class="btn btn-ghost"
					class:bg-[#FF9500]={$currentPath === '/contact'}
					class:text-black={$currentPath === '/contact'}
				>
					Contact
				</button>
			</a>
		</div>
	</nav>

	<!-- MOBILE DRAWER HEADER -->
	<div
		class="fixed top-0 right-0 left-0 z-50 drawer-content flex w-full items-center justify-between rounded-b-3xl bg-[#1F1F1F] px-4 py-2 pr-2 transition-transform duration-300 sm:hidden sm:px-0"
		class:translate-y-[-100%]={!showHeader}
		class:translate-y-0={showHeader}
	>
		<div class="flex gap-2">
			<img src="/Screenshot from 2025-08-04 09-03-32.png" class="h-8 w-8 rounded-full" alt="" />
			<!-- svelte-ignore a11y_invalid_attribute -->
			<a href="#"
				><p class="max-w-[100%] truncate text-xl font-bold whitespace-nowrap text-white">
					Proxi<span class="text-[#FF9500]">Feast</span>
				</p></a
			>
		</div>

		<label for="my-drawer" class="rounded-none border-none p-3 text-white">
			<svg
				class="cursor-pointer"
				xmlns="http://www.w3.org/2000/svg"
				width="25"
				height="25"
				viewBox="0 0 16 16"
			>
				<path
					fill="currentColor"
					d="M2 3.5a.5.5 0 0 1 .5-.5h11a.5.5 0 0 1 0 1h-11a.5.5 0 0 1-.5-.5m0 4a.5.5 0 0 1 .5-.5h11a.5.5 0 0 1 0 1h-11a.5.5 0 0 1-.5-.5m0 4a.5.5 0 0 1 .5-.5h11a.5.5 0 0 1 0 1h-11a.5.5 0 0 1-.5-.5"
				/>
			</svg>
		</label>
	</div>

	<!-- DRAWER SIDE BAR -->
	<section data-theme="lemonade">
		<div class="relative inset-0 z-100 mx-auto overflow-hidden">
			<input id="my-drawer" type="checkbox" class="drawer-toggle" />
			<div class="drawer-side sm:hidden">
				<label for="my-drawer" aria-label="close sidebar" class="drawer-overlay"></label>
				<!-- svelte-ignore a11y_missing_attribute -->
				<ul class="menu min-h-full w-80 bg-base-200 p-4 text-black">
					<li>
						<a onclick={closeSideBar} href="/"
							><button class:bg-[#FF9500]={$currentPath === '/'} class="rounded-lg p-2">Home</button
							></a
						>
					</li>
					<li>
						<a onclick={closeSideBar} href="/about"
							><button class:bg-[#FF9500]={$currentPath === '/about'} class="rounded-lg p-2"
								>About</button
							></a
						>
					</li>
					<li>
						<a onclick={closeSideBar} href="/services"
							><button class:bg-[#FF9500]={$currentPath === '/services'} class="rounded-lg p-2"
								>Services</button
							></a
						>
					</li>
					<li>
						<a onclick={closeSideBar} href="/pricing"
							><button class:bg-[#FF9500]={$currentPath === '/pricing'} class="rounded-lg p-2"
								>Pricing</button
							></a
						>
					</li>
					<li>
						<a onclick={closeSideBar} href="/contact"
							><button class:bg-[#FF9500]={$currentPath === '/contact'} class="rounded-lg p-2"
								>Contact</button
							></a
						>
					</li>
				</ul>
			</div>
		</div>
	</section>

	<div class="scroll-hidden min-h-screen w-full overflow-x-hidden">
		{@render children()}
	</div>

	<!-- FOOTER -->
	<!-- svelte-ignore a11y_missing_attribute -->
	<footer data-theme="" class="mt-8 footer bg-[#1F1F1F] p-10 text-white sm:footer-horizontal">
		<nav>
			<h6 class="footer-title">Services</h6>
			<a class="link link-hover">Branding</a>
			<a class="link link-hover">Design</a>
			<a class="link link-hover">Marketing</a>
			<a class="link link-hover">Advertisement</a>
		</nav>
		<nav>
			<h6 class="footer-title">Company</h6>
			<a class="link link-hover">About us</a>
			<a class="link link-hover">Contact</a>
			<a class="link link-hover">Jobs</a>
			<a class="link link-hover">Press kit</a>
		</nav>
		<nav>
			<h6 class="footer-title">Legal</h6>
			<a class="link link-hover">Terms of use</a>
			<a class="link link-hover">Privacy policy</a>
			<a class="link link-hover">Cookie policy</a>
		</nav>
		<!-- <form>
			<h6 class="footer-title">Newsletter</h6>
			<fieldset class="w-80">
				svelte-ignore a11y_label_has_associated_control
				<label class="text-white">Enter your email address</label>
				<div class="join">
					<input
						type="text"
						placeholder="username@site.com"
						class="input-bordered input join-item bg-white text-black"
					/>
					<button class="btn join-item bg-[#FF9500] text-white hover:bg-yellow-600"
						>Subscribe</button
					>
				</div>
			</fieldset>
		</form> -->
	</footer>
</div>
