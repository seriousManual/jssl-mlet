<style>
	.root {
		width:85%;
		margin:auto;
		margin-top:20px;
		max-width: 600px;
	}

	textarea {
		width: 100%;
		height: 20rem;
	}

	button {
		border: 1px solid black;
		width: 100%;
		height: 3rem;
	}

	h2 {
		margin-top: 3rem;
	}
</style>

<script>
	import moment from 'moment';
	import DateDiff from './DateDiff.svelte';
	import DateDiffUnits from './DateDiffUnits.svelte';

	let dateOfImage = null;
	let dateOfBirth = localStorage.getItem('dateOfBirth');
	let datesText = '';
	let lines = [];
	let dates = [];

	$: localStorage.setItem('dateOfBirth', dateOfBirth);
	$: dates = lines

	function processMultipleDates() {
		lines = datesText.split("\n").map( date => {
			return {
				name: date.split(": ")[0],
				date: date.split(": ")[1]
		}})
	}
</script>

<div class="root">
	<div class="form-group">
		<h2>Date of birth</h2>
		<input type="date" class="form-control" bind:value={dateOfBirth}>
	</div>

	<h2>Single date</h2>
	<div class="form-group">

		<input type="date" class="form-control" bind:value={dateOfImage}>
	</div>

	<DateDiffUnits startDate={dateOfBirth} endDate={dateOfImage} />
	<DateDiff startDate={dateOfBirth} endDate={dateOfImage} unit="days" numberOfDecimals=0/>
	<DateDiff startDate={dateOfBirth} endDate={dateOfImage} unit="weeks"/>
	<DateDiff startDate={dateOfBirth} endDate={dateOfImage} unit="months"/>
	<DateDiff startDate={dateOfBirth} endDate={dateOfImage} unit="years"/>

	<h2>Multiple dates</h2>	
	<div class="form-group">
		<textarea bind:value="{datesText}" placeholder="title: date"/>
		<button on:click={processMultipleDates}>Calculate</button>
	</div>

	{#each dates as date}
		<h3>{date.name}</h3>
		<DateDiff startDate={dateOfBirth} endDate={date.date} unit="weeks"/>
		<DateDiff startDate={dateOfBirth} endDate={date.date} unit="months"/>
		<DateDiff startDate={dateOfBirth} endDate={date.date} unit="years"/>
	{/each}
</div>