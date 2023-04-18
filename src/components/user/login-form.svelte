<script lang="ts">
	import {
		getAuth,
		signInWithEmailAndPassword,
		type User,
		signOut,
		onAuthStateChanged
	} from 'firebase/auth';
	import { onMount } from 'svelte';

	const auth = getAuth();

	let email: string;
	let password: string;
	let user: User | null;

	async function login() {
		const credential = await signInWithEmailAndPassword(auth, email, password);
	}

	onMount(() => {
		onAuthStateChanged(auth, (newUser) => {
			user = newUser;
		});
	});
</script>

{#if user}
	<h2>Welcome {user.email} / {user.uid}</h2>
	<button on:click={() => signOut(auth)}>Logout</button>
{:else}
	<form on:submit|preventDefault={login}>
		<div>
			<label for="email">Email</label>
			<input id="email" type="email" bind:value={email} />
		</div>
		<div>
			<label for="password">Password</label>
			<input id="password" type="password" bind:value={password} />
		</div>
		<button type="submit">Submit</button>
	</form>

	<hr />
	<a href="/user/register">Register</a>
{/if}
