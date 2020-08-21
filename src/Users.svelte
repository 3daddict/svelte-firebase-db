<script>
import { db } from './firestore.js';
import User from './User.svelte';

let users = [];
let email = "";
let name = "";

// get data from db collection, order by date created and assign to users array
db.collection('users').orderBy('createdAt').onSnapshot(data => {
    users = data.docs;
});

const addUser = () => {
    // create timestamp
    const createdAt = new Date().getTime();

    // add user as firebase document
    db.collection('users').add({ createdAt, email, name });
    // remove values on submit after added
    email = "";
    name = "";
}
    
</script>

<div class="user">
    <form on:submit|preventDefault={addUser}>
        <input type="text" bind:value={email} />
        <input type="text" bind:value={name} />
        <button>Add</button>
    </form>
</div>

<div id="users">
    {#each users as user}
        <User
            id={user.id}
            user={user.data()}
        />
    {/each}
</div>

<style>
    .user form {
        display: flex;
    }

</style>