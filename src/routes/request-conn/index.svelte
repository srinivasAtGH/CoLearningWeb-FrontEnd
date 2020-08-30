<script>
	import { goto, stores } from '@sapper/app';
	import ListErrors from '../_components/ListErrors.svelte';
	import RequestconnectionForm from './_request-conn.svelte';
	import * as api from 'api.js';

	//export let inProgress;
	let errors;
	let user = { };
	let mentor = { };
	//let mentorskills = { };
	//let communicationLanguages = {};
	//let response =null;
	const { session, page } = stores();

	async function save(event) {
		inProgress = true;

		const response = await post(`learningconnection`, event.detail);

		errors = response.errors;
		if (response.user) $session.user = response.user;

		inProgress = false;
	}

	async function getData() {
		let token = $session.user.access_token;
		user = await api.get('users/6', token);
		mentor = await api.get('users/8', token);
		
		console.log(user);
		console.log(mentor);
	}
	getData();

</script>

<svelte:head>
	<title>Request</title>
</svelte:head>

<div class="settings-page">
	<div class="container page">
		<div class="row">
			<div class="col-md-6 offset-md-3 col-xs-12">

				<h1 class="text-xs-center">request Connection</h1>

				<ListErrors {errors}/>
				<RequestconnectionForm on:save={save} user={user} mentor = {mentor} />
			</div>
		</div>
	</div>
</div>