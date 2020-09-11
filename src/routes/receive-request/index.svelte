<script>
	import { goto, stores } from '@sapper/app';
    import ListErrors from '../_components/ListErrors.svelte';
    import * as api from 'api.js';
    import { createEventDispatcher } from 'svelte';

	 let acceptText, declineText, username='Aniket',coLearnerUser ='Nilesh';
	 let learningdomain = 'Csharp';
	 let connectionString = 'Co Learner';
	 let communicationLanguages = 'Marathi,Hindi';
	 let currentCity = 'Pune';
	 let fluencyrating = '7/10 (self rated)';
	 let dailyTimeSpendonLearningin = '90 min';
	 let coLearnersPreferredMode = 'chat';
	 let connectionDetail = { };
     let learner = { };
    let mentee ={};
    let mentor ={};
	const dispatch = createEventDispatcher();
	let inProgress;
	let errors;

	const { session } = stores();

	async function getData() {
        //token = $session.user.access_token;	
        //console.log($session.user);	
        connectionDetail = await api.get('learning_connections/'+ $session.user.userid , $session.user.access_token);
        mentee= connectionDetail.mentee;
        mentor = connectionDetail.mentor;
		//user = await api.get('users/$($session.user.userid)' , token);
		//learner = await api.get('users/8', token);
        console.log(connectionDetail);
        //console.log(learner);
	}
    getData();
    
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

				<h1 class="text-xs-center">Received Request</h1>

				<ListErrors {errors}/>
                <form on:submit|preventDefault='{submit}'>
	
                    <fieldset>
                    <p class="text-warning">{mentor.name} wants to co-learn {connectionDetail.skillname} with you:</p>
                        <table class="table">		
                        <tbody>
                            <tr>
                                <td>Learning Domain:</td>
                                <td>{connectionDetail.skillname}</td>
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
                                <td>{connectionDetail.skillfluency}</td>
                            </tr>
                            <tr>
                                <td>Time {mentee.name} spend daily to learn {connectionDetail.skillname}:</td>
                                <td>{connectionDetail.timecommitment}</td>
                            </tr>
                            <tr>
                                <td>{mentee.name} preferred mode of communication:</td>
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