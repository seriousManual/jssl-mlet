<style>
	.root {
		width:85%;
		margin:auto;
		margin-top:20px;
		max-width: 600px;
	}
</style>

<script>
	import moment from 'moment';
	import DateDiff from './DateDiff.svelte';
	import DateDiffUnits from './DateDiffUnits.svelte';

	let dateOfImage = null;
	let dateOfBirth = localStorage.getItem('dateOfBirth');;

	$: localStorage.setItem('dateOfBirth', dateOfBirth);
</script>

<div class="root">
	<div class="form-group">
		<label>Date of birth</label>
		<input type="date" class="form-control" bind:value={dateOfBirth}>
	</div>

	<div class="form-group">
		<label>Date of image</label>
		<input type="date" class="form-control" bind:value={dateOfImage}>
	</div>

	<DateDiffUnits startDate={dateOfBirth} endDate={dateOfImage} />
	<DateDiff startDate={dateOfBirth} endDate={dateOfImage} unit="days" numberOfDecimals=0/>
	<DateDiff startDate={dateOfBirth} endDate={dateOfImage} unit="weeks"/>
	<DateDiff startDate={dateOfBirth} endDate={dateOfImage} unit="months"/>
	<DateDiff startDate={dateOfBirth} endDate={dateOfImage} unit="years"/>
</div>