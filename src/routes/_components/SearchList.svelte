<script>
    export let listData;
    export let onDismiss;
    export let index;
    export let selection;
    const {guidingSkills} = listData;
    let skills;
    $: skills = listData.guidingSkills.includes(",") ? listData.guidingSkills.split(",") : listData.guidingSkills;
    console.log("Skills:" + skills);
</script>

<style>
.remove{
	position: absolute;
	right: 20px;
    top: 10px;
}
.search-list{
	position: relative;
	padding-top: 15px;
}
.image-container{
	text-align: center;
}
.user-type{
	padding-top: 3px;
	font-weight: 600;
}
.guide-span{
    color: #8d8d8d;
}
.co-learner-span{
    color: #7ed5b7;
}
.name-container{
	width: 100%;
}
.name{
	font-size: 22px;
    color: gray;
    font-weight: 600;
}
.is-new-suggestion{
	color: deepskyblue;
	margin-left: 10px;
}
.aoe-span{  
	color: orange;
    font-weight: 600;
}
.no-display{
    display: none;
}
.selection-checkbox{
    position: relative;
    top: 40%;
}
.details-container{
    text-align: right;
    width: 90%;
}
</style>

<div class="search-list row">
    <div class="col-sm-1">
    </div>
    <div class="image-container col-sm-2">
        <img src="images/temp.jpg" class="img-circle" alt="Profile" width="80" height="80">
        <div class="user-type">
            <span class={`guide-span ${(listData.isguide) ? '' : 'no-display'}`}>Guide <span class="check-icon"><ion-icon name="checkmark-done-outline"></ion-icon></span></span>
            <span class={`co-learner-span ${(listData.iscolearner) ? '' : 'no-display'}`}>Co-Learner</span>
        </div>
    </div>
    <div class="desc-container col-sm-9">
        <div class="name-container">
            <span class="name">{listData.firstname} {listData.lastname}</span>
            <span class={`is-new-suggestion ${(listData.isNewSuggestion) ? '' : 'no-display'}`}>New Suggestion</span>
        </div>
        <div class="aoe-container row">
            <div class="aoe-span col-xs-2">AOE:</div>
            <div class="col-xs-10">
            {#if guidingSkills.includes(",")}
                {#each skills as expertise, i}
                    <div>{(i+1)}.&nbsp;{expertise}</div>
                {/each}
            {:else}
                <div>1.{skills}</div>
            {/if}
            </div>
        </div>
        <div class="details-container">
            <a href="/mentor-profile?mentorId={listData.Id}">
                <button type="button" class="btn btn-info btn-sm">View Profile</button>
            </a>
        </div>
    </div>
    <div class="remove">
        <button type="button" class="close" aria-label="Close" on:click={() => onDismiss(index)}>
            <span aria-hidden="true">&times;</span>
        </button>
    </div>
    <div class="col-xs-12">
        <hr />
    </div>
</div>