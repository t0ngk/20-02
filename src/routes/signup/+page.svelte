<script>
	let formData = {
		email: '',
		password: '',
		confirmPassword: ''
	};

	import { userLogin, addNotification } from '$lib/store.js';
	import { goto } from '$app/navigation';
	import { onMount } from 'svelte';

	onMount(async () => {
		if ($userLogin) {
			goto('/menu');
			return;
		}
	});
</script>

<svelte:head>
	<title>
		Sign Up
	</title>
</svelte:head>

<!--Video-->
<div class="2xl:container h-screen m-auto">
	<div hidden class="fixed inset-0 w-7/12 lg:block">
		<div
			class="absolute top-1/2 left-1/4 transform -translate-x-1/2 -translate-y-1/2 text-7xl text-white"
		>
			<p>20-02</p>
			<div class="w-20">
				<div class="mt-4 border-t-4  border-white">
					<span class="block w-4 mx-auto mt-4" />
				</div>
			</div>
		</div>
		<video class="w-full h-full object-cover" autoplay loop src="/video/Lines-4760.mp4">
			<track kind="captions" />
		</video>
	</div>

	<!-- Head Login 1 -->
	<div
		hidden
		class="fixed inset-0 w-6/12 ml-auto bg-white bg-opacity-70 backdrop-blur-xl lg:block"
	/>
	<div class="relative h-full ml-auto lg:w-6/12">
		<div class="m-auto py-12 px-6 sm:p-20 xl:w-10/12">
			<div class="space-y-4">
				<div class="w-40" />
				<p class="text-5xl text-black">Sign Up</p>
			</div>
			<div class="w-20">
				<div class="mt-4 border-t-4  border-black">
					<span class="block w-4 mx-auto mt-4" />
				</div>
			</div>
			<!--insert email-->
			<div class="space-y-6 py-6">
				<div>
					<input
						bind:value={formData.email}
						type="email"
						placeholder="Your Email"
						class="w-full py-3 px-6 ring-1 ring-gray-300 rounded-xl placeholder-gray-600 bg-transparent transition disabled:ring-gray-200 disabled:bg-gray-100 disabled:placeholder-gray-400 invalid:ring-red-400 focus:invalid:outline-none shadow-xl"
					/>
				</div>

				<div class="flex flex-col items-end">
					<input
						bind:value={formData.password}
						type="password"
						placeholder="Your Password"
						class="w-full py-3 px-6 ring-1 ring-gray-300 rounded-xl placeholder-gray-600 bg-transparent transition disabled:ring-gray-200 disabled:bg-gray-100 disabled:placeholder-gray-400 invalid:ring-red-400 focus:invalid:outline-none shadow-xl"
					/>
				</div>

				<div class="flex flex-col items-end">
					<input
						bind:value={formData.confirmPassword}
						type="password"
						placeholder="Confirm Password"
						class="w-full py-3 px-6 ring-1 ring-gray-300 rounded-xl placeholder-gray-600 bg-transparent transition disabled:ring-gray-200 disabled:bg-gray-100 disabled:placeholder-gray-400 invalid:ring-red-400 focus:invalid:outline-none shadow-xl"
					/>
				</div>

				<div class="w-full flex justify-center">
					<div class="w-44">
						<div class="w-full pt-3 border-t-4 border-black" />
					</div>
				</div>

				<div>
					<button
						class="w-full px-6 py-3 rounded-xl  bg-neutral-900 transition hover:bg-slate-800  active:bg-slate-900 shadow-xl"
						on:click={() => {
							let userData = localStorage.getItem('userData')
								? JSON.parse(localStorage.getItem('userData'))
								: [];
							if (formData.email == '') {
								addNotification('กรุณากรอกอีเมล', 'danger', 3000);
								return;
							}
							if (userData.find((user) => user.email === formData.email)) {
								addNotification('Email ถูกใช้ไปแล้ว', 'danger', 3000);
							} else {
								if (formData.password === formData.confirmPassword) {
									userData.push({
										email: formData.email,
										password: formData.password
									});
									localStorage.setItem('userData', JSON.stringify(userData));
									addNotification('สมัครสมาชิกสำเร็จ', 'success', 3000);
									goto('/login');
								} else {
									addNotification('รหัสผ่านไม่ตรงกัน', 'danger', 3000);
								}
							}
						}}
					>
						<span class="font-semibold text-white text-lg">Sign Up</span>
					</button>

					<div class="w-full flex justify-center">
						<a href="/login" type="reset" class="w-max p-10 ml-4 text-sm">
							Already have account?
							<span class="text-sm tracking-wide text-blue-600">Sign-In</span>
						</a>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>
