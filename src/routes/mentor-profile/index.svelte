<script>
    import { stores } from "@sapper/app";
    import * as api from 'api.js';
    const userData = {
        "Id": 2,
        "username": "prasad",
        "email": "p@d.com",
        "hash": "19ce325775cf80ec43b16531a849bbbd09f5e36d8ad1ea73da5322173337a6878fd05d776f98d112f14fa01676c4195cf3b8d4eeed7145e470c9fd921af5a84e46792090ccb590bcde53070241765571c088dd2c9641c7949d71f3cf85490438a322b59ba0527c0d68c938dbb0dbe310134b0ddfdbabb1dc25964a3dd5b05b5c1afb8e122586c9cef319395aaa564d3fb934aff3a8a4300513a55966274f35bc07f86981d39a7086cba4ccd45274ac4afb6b23e0c03b7eb143195fc1459ecc8d604f904737b3a1257e05c1908c2eab5709661473dc4eac829bc53f2b6d68eac19ebe405c7899d567f8fe62271d501f550e6e848a1f83c30391e5e538fa5427444a5359fe2182c0ce42f93f8aa56a45141bde88fa4b5350bd246488e0477f1e5542482bced1c4fd118a031e79c882bb5d325815c2ad48fd99c4025e16a9913d3d460865246eab1aefb3a98cf584f6bcb618a9316bd20c985563463915505d37f484851c4f46ff23538eadf55667f66e4569aea28b3da8ef46ef276119a8b3e25166e1c71f4cfe54f98e5abeb5d3dc983181f7c6cc7e065a30842f8fce0e32f8fb4fe4a7b661512e9fc6e9f071a7291fb5899ff30b11695c5d98d777b5c8c5d67c0d31f04d49398227b970ad1de72a27838721feec42d3c2b987e9dfe7e1003d1163b1640cda71c98d7092c64638b0b75a9c0a90e8c78f31fbb97fed2baacf519b",
        "salt": "d9a1b3194fb16731c85439dc2757d1b1",
        "firstname": "Prasad",
        "lastname": "Gurav",
        "country": null,
        "state": null,
        "city": null,
        "emailprivacy": 1,
        "phonenumber": null,
        "phonenumberprivacy": 1,
        "whatsappnumber": null,
        "whatsappnumberprivacy": 1,
        "birthdate": null,
        "gender": "male",
        "occupation": null,
        "photo": null,
        "islearner": true,
        "isguide": true,
        "bio": "Prasad is a 45-year-old former intern at a law firm who enjoys painting, meditation and drone photography. He is entertaining and smart.\r\nt is a long established fact that a reader will be distracted by the readable content of a page when looking at its layout. The point of using Lorem Ipsum is that it has a more-or-less normal distribution of letters, as opposed to using 'Content here, content here', making it look like readable English.",
        "iscolearner": true,
        "istermsandconditionschecked": true,
        "isemailverified": false,
        "languages": null,
        "guidingSkills": "Python",
        "learningSkills": "Gardening",
        "createdAt": "2020-08-29T16:54:01.348Z",
        "updatedAt": "2020-08-29T16:54:01.348Z"
    };
    const { session, page } = stores();
    const {
        firstname,
        lastname,
        iscolearner,
        isguide,
        city,
        emailprivacy,
        email,
        phonenumberprivacy,
        phonenumber,
        whatsappnumberprivacy,
        whatsappnumber,
        bio,
        guidingSkills
    } = userData;
    const skills = guidingSkills.includes(",") ? guidingSkills.split(",") : guidingSkills;
    const languages = "English, Hindi, Marathi";
    async function getData() {
        console.log($page.query);
        console.log($session.user);
    }
    getData();
</script>

<style>
.aoe-span{
	color: orange;
    font-weight: 600;
}
</style>

<svelte:head>
	<title>Mentor Profile</title>
</svelte:head>

<div class="request-connect-page">
    <div class="container page">
		<div class="row">
            <div class="col-md-6 offset-md-3 col-xs-12">
                <div class="row">
                    <div class="col-sm-4">
                        {firstname} {lastname}
                        <p>
                            <span class={`guide-span ${(isguide) ? '' : 'no-display'}`}>Guide</span>
                            <span class={`co-learner-span ${(iscolearner) ? '' : 'no-display'}`}>Co-Learner</span>
                        </p>
                    </div>
                    <div class="col-sm-8">
                        <div class="aoe-container row">
                            <div class="aoe-span col-xs-1">AOE:</div>
                            <div class="col-xs-10">
                                {#if guidingSkills.includes(",")}
                                    {#each skills as extertise, i}
                                        <div>{(i+1)}. {extertise}</div>
                                    {/each}
                                {:else}
                                    <div>1. {skills}</div>
                                {/if}
                            </div>
                        </div>
                        <div>
                            {city}
                        </div>
                        <div>
                            {languages}
                        </div>
                    </div>
                </div>
                <div class="row">
                    {#if phonenumberprivacy && whatsappnumberprivacy && emailprivacy}
                        <p>This is a Private Account</p>
                    {:else if !phonenumberprivacy}
                        <p>Phone No: {phonenumber}</p>
                    {:else if !whatsappnumberprivacy}
                        <p>Whatsapp Number: {whatsappnumber}</p>
                    {:else if !emailprivacy}
                        <p>Email: {email}</p>
                    {/if}
                </div>
                <div class="row">
                    <p>{firstname}'s Words:</p>
                    <p>{bio}</p>
                </div>
            </div>
        </div>
    </div>
</div>