<script>
    
    export let listData;
    export let displayMode;
    
    //date conversion
    let creationDate = new Date (Date.parse(listData.creation_date));
    console.log(creationDate);
    let creationDateFormatted = creationDate.toDateString();

</script>

<style>

.connection-list{
	position: relative;
	padding-top: 15px;
}
.name-container{
	width: 100%;
}
.aoe-span{
	color: orange;
    font-weight: 600;
}

.name{
	font-size: 22px;
    color: gray;
    font-weight: 600;
}

</style>

<div class="connection-list row">
    <div class="desc-container col-sm-10">
        {#if displayMode==="ViewReceivedRequestList"}
        <div class="name-container col-sm-10">
            <span class="name">{listData.mentee.name}</span>
        </div>
        {/if}
        <div class="aoe-container row col-sm-10">
            <div class="aoe-span">Skill to learn:</div>
            <div class="name-container">
                    {(listData.skillname)}
            </div>
        </div>
        <div class="aoe-container-row col-sm-10">
            <div class="aoe-span">Request date:</div>
            <div class="name-container">
                    {(creationDateFormatted)}
            </div>
        </div>
        <div class="aoe-container-row col-sm-10">
            <a href="/ReceiveReq/{listData.id}">
                <button type="button" class="btn btn-info btn-sm">View</button>
            </a>
        </div>
    </div>
    <div class="col-xs-10">
        <hr />
    </div>
</div>