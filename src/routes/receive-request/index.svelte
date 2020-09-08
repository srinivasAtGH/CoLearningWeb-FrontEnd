<script>
	import { goto, stores } from '@sapper/app';
	import ListErrors from '../_components/ListErrors.svelte';
	import { post } from 'utils.js';
    import { createEventDispatcher } from 'svelte';

	 let acceptText, declineText, username='Aniket',coLearnerUser ='Nilesh';
	 let learningdomain = 'Csharp';
	 let connectionString = 'Co Learner';
	 let communicationLanguages = 'Marathi,Hindi';
	 let currentCity = 'Pune';
	 let fluencyrating = '7/10 (self rated)';
	 let dailyTimeSpendonLearningin = '90 min';
	 let coLearnersPreferredMode = 'chat';
	 
	const dispatch = createEventDispatcher();
	let inProgress;
	let errors;

	const { session } = stores();

	async function logout() {
		await post(`auth/logout`);
		$session.user = null;
		goto('/');
	}
    function submit(event) {
		dispatch('save', { image, username, bio, email, password }); 
	}
	async function save(event) {
		inProgress = true;

		const response = await post(`auth/save`, event.detail);

		errors = response.errors;
		if (response.user) $session.user = response.user;

		inProgress = false;
	}
</script>

<svelte:head>
	<title>Request</title>
</svelte:head>

<div class="settings-page">
	<div class="container page">
		<div class="row">
			<div class="col-md-6 offset-md-3 col-xs-12">

				<h1 class="text-xs-center">Request from..</h1>

				<ListErrors {errors}/>
                <form on:submit|preventDefault='{submit}'>
	
                    <fieldset>
                    <p class="text-warning">{coLearnerUser} wants to co-learn {learningdomain} with you:</p>
                        <table class="table">		
                        <tbody>
                            <tr>
                                <td>Learning Domain:</td>
                                <td>{learningdomain}</td>
                            </tr>
                            <tr>
                                <td>Connection String:</td>
                                <td>{connectionString}</td>
                            </tr>
                            <tr>
                                <td>Communication Languages:</td>
                                <td>{communicationLanguages}</td>
                            </tr>
                            <tr>
                                <td>Current City:</td>
                                <td>{currentCity}</td>
                            </tr>
                            <tr>
                                <td>fluency in {learningdomain}:</td>
                                <td>{fluencyrating}</td>
                            </tr>
                            <tr>
                                <td>Time {coLearnerUser} spend daily to learn {learningdomain}:</td>
                                <td>{dailyTimeSpendonLearningin}</td>
                            </tr>
                            <tr>
                                <td>{coLearnerUser} preferred mode of communication:</td>
                                <td>{coLearnersPreferredMode}</td>
                            </tr>
                        </tbody>
                          </table>
                        
                        <fieldset class="form-group">
                            <p class="text-warning">{coLearnerUser} words:</p>
                            <textarea class="form-control form-control-lg" rows="4" placeholder="Add your message here" bind:value={acceptText}/>
                            <p class="text-warning">{coLearnerUser} is open to share his/her ideas with his/her co-learners.</p>
                        </fieldset>			
                        <button class="btn btn-outline-primary">
                                Accept request
                        </button>
                        <p class="text-primary">Once you accept the request your email id will be shared with {coLearnerUser}.</p>
                        <hr/>		
                        <fieldset class="form-group">
                        <p class="text-danger">Don't want to accept the request? Please write down the reason so {coLearnerUser} can improve his/her skills.</p>
                            <textarea class="form-control form-control-lg" rows="2" placeholder= "reason to decline request?" bind:value={declineText}/>
                        </fieldset>
                        <button class="btn btn-outline-danger">
                                Decline request
                        </button>
                    </fieldset>
                </form>
			</div>
		</div>
	</div>
</div>