<script>
  import { stores } from "@sapper/app";
  import * as api from "api.js";

  const { session, page } = stores();

  let mentorid,
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
    guidingSkills;

  let userData;

  let skills;
  const languages = "English, Hindi, Marathi";

  async function getData() {
    userData = await api.get(
      "users/" + $page.query.mentorId,
      $session.user.access_token
    );

    console.log("User data:" + userData);
    mentorid = userData.Id;
    console.log("User id:" + mentorid);
    firstname = userData.firstname;
    lastname = userData.lastname;
    iscolearner = userData.iscolearner;
    isguide = userData.isguide;
    city = userData.city;
    emailprivacy = userData.emailprivacy;
    email = userData.email;
    phonenumberprivacy = userData.phonenumberprivacy;
    phonenumber = userData.phonenumber;
    whatsappnumberprivacy = userData.whatsappnumberprivacy;
    whatsappnumber = userData.whatsappnumber;
    bio = userData.bio;
    guidingSkills = userData.guidingSkills;

    console.log("user guiding skills " + guidingSkills);
    console.log("first name " + firstname);
    skills = guidingSkills;
  }
  getData();

  console;
</script>

<style>
  .aoe-span {
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
          <div class="media-left">
            <img
              class="media-object img-circle"
              src="images/temp.jpg"
              alt="Profile"
              width="50"
              height="50" />
            <div class="col-sm-8">
              {firstname} {lastname}
              <p>
                (
                <span class={`guide-span ${isguide ? '' : 'no-display'}`}>
                  Guide
                </span>
                <span class={`co-learner-span ${isguide ? '' : 'no-display'}`}>
                  +
                </span>
                <span
                  class={`co-learner-span ${iscolearner ? '' : 'no-display'}`}>
                  Co-Learner
                </span>
                )
              </p>
            </div>
          </div>

          <div class="col-sm-8">
            <div class="aoe-container row">
              <div class="aoe-span col-xs-1">AOE:</div>

              <div class="col-xs-10">
                <!-- {#if guidingSkills.includes(',')}
                  {#each skills as extertise, i}
                    <div>{i + 1}. {extertise}</div>
                  {/each}
                {:else} -->
                <div>{skills}</div>
                <!-- {/if} -->
              </div>
            </div>
            <div>{city}</div>
            <div>{languages}</div>
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
        <div class="details-container">
          <a href="/request-connect?mentorId={mentorid}">
            <button type="button" class="btn btn-md btn-primary pull-xs-right">
              Connect with {firstname}
            </button>
          </a>
        </div>
      </div>

    </div>
  </div>
</div>
