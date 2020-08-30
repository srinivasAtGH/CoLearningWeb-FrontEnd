<script>
	import { goto, stores } from "@sapper/app";
	import * as api from 'api.js';
	
	let searchText = '';
	export let user = { };
	export let mentor = { };
	
	const { session } = stores();

	async function getData() {
		skills = mentor.learningSkills.split(',')
		console.log(mentor);
	 }
	 getData();
	
	let acceptText, declineText;
	let learningdomain = 'Csharp';
	let connectionString = 'Co Learner';
	
	let fluencyrating = '7/10 (self rated)';
	let dailyTimeSpendonLearningin = 0;
	let coLearnersPreferredMode = 'chat';
	let selfRating =1;
	let skills = ' ';
	let connections =['learner','co-learner'];
	function submit(event) {
		//dispatch('save', { image, username, bio, email, password }); 
	}


</script>

<form on:submit|preventDefault='{submit}'>
	
	<fieldset>
	<p class="text-warning">Connection request to {(user.username)}</p>
		<table class="table">		
		<tbody>
			<tr>
				<td>Learning Domain:</td>
				<td> 
					<select>
						<!-- {#each user.learningSkills.split(',') as userskill} -->
							<option value={mentor.learningSkills}> {mentor.learningSkills} </option>
						<!-- {/each} -->
						
					</select>
					{(skills)}
				</td>
			</tr>
			<tr>
				<td>Connection:</td>
				<td>
					<select>
						{#each connections as connection}
							<option value={connection}> {connection} </option>
						{/each}	
						
					</select>
				</td>
			</tr>
			<tr>
				<td>Communication Languages:</td>
				<td>{(mentor.languages)}</td>
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
					<input type=range bind:value={dailyTimeSpendonLearningin} min=0 max=360 step=5> 
					<br/> {dailyTimeSpendonLearningin} Min(max 360 min).
				</td>
			</tr>			
		</tbody>
  		</table>
		
		<fieldset class="form-group">
			<p class="text-warning">write down something to {(mentor.username)} about yourself: </p>
			<textarea class="form-control form-control-lg" rows="8" placeholder="Add about yourself here" bind:value={acceptText}/>			
		</fieldset>			
		<button class="btn btn-outline-primary">
				send request
		</button>	
	</fieldset>
</form>