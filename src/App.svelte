<script>
	import moment from 'moment';
	import DateDiff from './DateDiff.svelte';

	let dateOfImage = null;
	let dateOfBirth = localStorage.getItem('dateOfBirth');;
	let durationDiff = null;

	$: localStorage.setItem('dateOfBirth', dateOfBirth);

	$: if (dateOfImage && dateOfBirth) {
		const durationObject = moment.duration(moment(dateOfImage).diff(moment(dateOfBirth)))

		const month = Math.floor(durationObject.as('months'))
		durationObject.subtract(month, 'months')
		const weeks = Math.floor(durationObject.as('weeks'))
		durationObject.subtract(weeks, 'weeks')
		const days = durationObject.as('days').toFixed(0)
		durationDiff = month + "m " + weeks + "w " + days + "d"
	}
</script>

<div style="width:85%;margin:auto;margin-top:20px">
	<div class="form-group">
		<label>Date of birth</label>
		<input type="date" class="form-control" bind:value={dateOfBirth}>
	</div>

	<div class="form-group">
		<label>Date of image</label>
		<input type="date" class="form-control" bind:value={dateOfImage}>
	</div>

{#if durationDiff}
	<div class="form-group">
		<label>Time between dates</label>
		<div>
			<h3>{durationDiff}</h3>
		</div>
	</div>
{/if}

	<DateDiff bind:startDate={dateOfBirth} bind:endDate={dateOfImage} unit="days" numberOfDecimals=0/>
	<DateDiff bind:startDate={dateOfBirth} bind:endDate={dateOfImage} unit="weeks"/>
	<DateDiff bind:startDate={dateOfBirth} bind:endDate={dateOfImage} unit="months"/>
	<DateDiff bind:startDate={dateOfBirth} bind:endDate={dateOfImage} unit="years"/>
</div>