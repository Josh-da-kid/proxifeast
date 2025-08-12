<!-- <div class="hero mt-25 min-h-screen">
	<h1 class="text-4xl text-black md:text-5xl">Join the Waitlist</h1>

	<form action="">
		<label for="name">
			<p>Full-name</p>
			<input type="text" placeholder="John Doe" />
		</label>
	</form>
</div> -->

<script>
	import { fly } from 'svelte/transition';
	let name = '';
	let email = '';
	let country = '';

	function showModal() {
		if (name.length > 0 && email.length > 0 && country.length > 0) {
			my_modal_1.showModal();
		}
	}
</script>

<div
	class="hero min-h-screen"
	style="background-image: url(https://img.daisyui.com/images/stock/photo-1507358522600-9f71e620c44e.webp);"
>
	<div class="hero-overlay"></div>
	<div
		class="hero-content lg:flex-row-reversee w-full flex-col"
		transition:fly={{ x: -200, duration: 500 }}
	>
		<!-- <div class="text-center lg:text-left">
        <h1 class="text-5xl font-bold">Login now!</h1>
        <p class="py-6">
            Provident cupiditate voluptatem et in. Quaerat fugiat ut assumenda excepturi exercitationem
            quasi. In deleniti eaque aut repudiandae et a id nisi.
            </p>
            </div> -->
		<h1 class="text-4xl font-semibold text-white md:text-5xl">Join the Waitlist!!</h1>
		<div class="card bg-base-100 w-full max-w-sm shrink-0 shadow-2xl">
			<div class="card-body">
				<form action="" class="fieldset">
					<label class="label">Full Name</label>
					<input
						type="text"
						bind:value={name}
						class="rounded-lg border-2 border-gray-300 p-3 focus:ring-2 focus:ring-[#008753] focus:outline-none"
						placeholder="John Doe"
						required
					/>
					<label class="label">Email</label>
					<input
						type="email"
						bind:value={email}
						class="rounded-lg border-2 border-gray-300 p-3 focus:ring-2 focus:ring-[#008753] focus:outline-none"
						placeholder="Email"
						required
					/>
					<label class="label">Your Country</label>
					<input
						type="text"
						bind:value={country}
						class="rounded-lg border-2 border-gray-300 p-3 focus:ring-2 focus:ring-[#008753] focus:outline-none"
						placeholder="Nigeria"
						required
					/>

					<button type="submit" class="btn btn-neutral mt-4" onclick={showModal}
						>Join Waitlist</button
					>
				</form>
			</div>
		</div>
	</div>
</div>

<!-- modal -->
<!-- Open the modal using ID.showModal() method -->

<dialog id="my_modal_1" class="modal">
	<div class="modal-box">
		<h3 class="text-lg font-bold">Congrats!</h3>
		<p class="py-4">
			You have been successfully added to our waitlist, you'll be among the first persons to enjoy
			the glorious benefits AbujaSocialER has to offer!!
		</p>
		<div class="modal-action">
			<form method="dialog">
				<!-- if there is a button in form, it will close the modal -->
				<button class="btn">Close</button>
			</form>
		</div>
	</div>
</dialog>
