<script>
import { db } from './firestore.js';

export let id = "";
export let user = {};

const deleteUser = () => {
    // remove user document from firestore
    db.collection('users').doc(id).delete();
}
    
const updateUser = () => {
    // update user document data in firestore
    db.collection('users').doc(id).update({
        email: user.email,
        name: user.name
    });
}
</script>

<div class="user">
    <input type="text" bind:value={user.email} on:input={updateUser} />
    <input type="text" bind:value={user.name} on:input={updateUser} />
    <button on:click={deleteUser}>🗑️</button>
</div>

<style>
    .user {
        display: flex;
    }

</style>
