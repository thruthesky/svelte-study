<script lang="ts">
	import { goto } from '$app/navigation';
	import { getFirestore, doc, setDoc, serverTimestamp } from 'firebase/firestore';
	import { getAuth, createUserWithEmailAndPassword } from 'firebase/auth';

	let display_name: string;
	let email: string;
	let password: string;

	const auth = getAuth();

	async function register() {
		const credential = await createUserWithEmailAndPassword(auth, email, password);

		await setDoc(doc(getFirestore(), 'users', credential.user.uid), {
			display_name,
			email,
			uid: credential.user.uid,
			registered_at: serverTimestamp()
		});
		goto('/');
	}
</script>

<h1>Register</h1>

<form on:submit|preventDefault={register}>
	<div>
		<label for="display_name">display_name</label>
		<input type="text" id="display_name" bind:value={display_name} />
	</div>
	<div>
		<label for="email">email</label>
		<input type="text" id="email" bind:value={email} />
	</div>
	<div>
		<label for="password">password</label>
		<input type="text" id="password" bind:value={password} />
	</div>

	<button type="submit">Register</button>
</form>
