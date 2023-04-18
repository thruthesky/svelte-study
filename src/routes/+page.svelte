<script lang="ts">
	import { initializeApp } from 'firebase/app';

	import {
		getAuth,
		signInWithEmailAndPassword,
		type User,
		signOut,
		onAuthStateChanged
	} from 'firebase/auth';
	import { onMount } from 'svelte';

	const firebaseConfig = {
		apiKey: 'AIzaSyBz2OFyac4LdNAA8jomtLlpSdBsO1BWyjY',
		authDomain: 'withcenter-test-2.firebaseapp.com',
		databaseURL: 'https://withcenter-test-2-default-rtdb.asia-southeast1.firebasedatabase.app',
		projectId: 'withcenter-test-2',
		storageBucket: 'withcenter-test-2.appspot.com',
		messagingSenderId: '817502397544',
		appId: '1:817502397544:web:c3089782f014d4032487dd'
	};

	const app = initializeApp(firebaseConfig);
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

<h1>SvelteKit Study Project By Withcenter</h1>

{#if user}
	<h2>Welcome {user.email}</h2>
	<button on:click={() => signOut(auth)}>Logout</button>
{:else}
	<form on:submit|preventDefault={login}>
		<input type="email" bind:value={email} />
		<input type="password" bind:value={password} />
		<button type="submit">Submit</button>
	</form>
{/if}
