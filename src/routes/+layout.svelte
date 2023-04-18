<script>
	import { initializeApp } from 'firebase/app';
	import { firebaseConfig } from '$lib/firebase-config';

	initializeApp(firebaseConfig);
</script>

<h1>SvelteKit Study Project By Withcenter</h1>

<a href="/about">About</a>
<a href="/posts">Posts</a>
<a href="/user/profile">Profile</a>

<slot />
