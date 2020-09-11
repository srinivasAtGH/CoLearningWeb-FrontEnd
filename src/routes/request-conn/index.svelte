<script>
	import { goto, stores } from '@sapper/app';
	import ListErrors from '../_components/ListErrors.svelte';
	import * as api from 'api.js';
	import { post } from 'utils.js';	
	import { createEventDispatcher } from 'svelte';

	let searchText = '';
	let aboutYourself;
	let learningdomain = 'Csharp';
	let dailyTimeSpend = 0;
	let coLearnersPreferredMode = 'chat';
	let selfRating =1;
	let skill = ' ';
	let connection = ' ';
	let connections =['learner','co-learner'];
	let errors;
	let inProgress;
	let user = { };
	let mentor = { };
	let token = '';
	const { session, page } = stores();

	async function submit(event) {
	
		inProgress = true;
		console.log(connection);
		const response = await api.post(`learning_connection/send_request/`,
		 {
			"request":
				{
					"userId": user.userid,
					"partnerId": mentor.userid,
					"skillName": 'N language',
					"skillFluency": selfRating,
					"timeCommitment": dailyTimeSpend,
					"personalNoteRequest": aboutYourself,
					"connectionType": 'learner',
				}
		 }, token );
		
		 errors = response.errors;
		if (response.user) $session.user = response.user;
		inProgress = false
	}

	async function getData() {
		token = $session.user.access_token;
		console.log($session.user);
		user = await api.get('users/'+ $session.user.userid , token);
		//user = await api.get('users/$($session.user.userid)' , token);
		mentor = await api.get('users/8', token);
		console.log(user);
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

				<h1 class="text-xs-center">Request Connection</h1>

				<ListErrors {errors}/>
				<form on:submit|preventDefault={submit}>
				<fieldset>
					<p class="text-warning">Connection request from {(user.username)}</p>
						<table class="table">		
						<tbody>
							<tr>
								<td>Learning Domain:</td>
								<td>
									<select class="form-control form-control-md" value={skill}>
										<!-- {#each mentor.learningSkills as learningSkill} -->
											<option value={mentor.learningSkills}>
												{mentor.learningSkills}
											</option>
										<!-- {/each} -->
									</select>   
								</td>
							</tr>
							<tr>
								<td>Connection:</td>
								<td>
									<select class="form-control form-control-md" value={connection}>
										{#each connections as conn}
											<option value={conn}>
												{conn}
											</option>
										{/each}
									</select>   
								</td>
							</tr>
							<tr>
								<td>Communication Languages:</td>
								<td>{(mentor.languages)} </td>
							</tr>
							<tr>
								<td>Current City:</td>
								<td>{(user.city)}</td>
							</tr>
							<tr>
								<td>fluency in {learningdomain}:</td>
								<td><input type=range bind:value={selfRating} min=0 max=10> <br/>{selfRating} out of 10</td>
							</tr>
							<tr>
								<td>Time Time spend daily to learn this topic daily:</td>
								<td>
									<input type=range bind:value={dailyTimeSpend} min=0 max=360 step=5> 
									<br/> {dailyTimeSpend} Min(max 360 min).
								</td>
							</tr>			
						</tbody>
						  </table>
						
						<fieldset class="form-group">
							<p class="text-warning">write down something to {(mentor.username)} about yourself: </p>
							<textarea class="form-control form-control-lg" rows="8" placeholder="Add about yourself here" bind:value={aboutYourself}/>			
						</fieldset>			
						<button class="btn btn-outline-primary">
								send request
						</button>	
					</fieldset>
			
			
				</form>
			</div>
		</div>
	</div>
</div>