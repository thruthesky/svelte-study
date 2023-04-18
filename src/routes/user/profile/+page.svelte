<script lang="ts">
	import { getFirestore, doc, setDoc, serverTimestamp } from 'firebase/firestore';
	import { getAuth, createUserWithEmailAndPassword } from 'firebase/auth';

	let display_name: string;
	let email: string;
	let password: string;

	const auth = getAuth();

	async function update() {
		await setDoc(doc(getFirestore(), 'users', auth.currentUser!.uid), {
			display_name
		});
		alert('Updated!');
	}
</script>

<h1>Profile</h1>

<form on:submit|preventDefault={update}>
	<div>
		<label for="display_name">display_name</label>
		<input type="text" id="display_name" bind:value={display_name} />
	</div>
	<button>Update</button>
</form>
