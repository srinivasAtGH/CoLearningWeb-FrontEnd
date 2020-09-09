<script context="module">

    import * as api from 'api.js';


    export async function preload({ params }) {
            console.log("pre-load");
            const {requestId} = params;
            console.log(params);
            return {requestId};
        }

</script>

<script>
import { onMount } from 'svelte';
import { stores } from '@sapper/app';

export let requestId;
console.log("requestid" + requestId);
let learningConnectionRequest;

const { session } = stores();

onMount(() => {
    console.log("OnMount");
    console.log(requestId);
    api.get(`learning_connections/${requestId}`,$session.user.access_token).then((res) => {
        console.log(res);
        learningConnectionRequest = res;
    });
});

</script>

<div>
<h1>Connection Request</h1>

{#if learningConnectionRequest !== undefined}
{learningConnectionRequest.mentee.name}
{learningConnectionRequest.skillname}
{learningConnectionRequest.notesrequest}
{learningConnectionRequest.timecommitment}
{learningConnectionRequest.skillfluency}
{/if}
</div>