<script>
	import moment from 'moment';
	import DateDiff from './DateDiff.svelte';
	import DateDiffUnits from './DateDiffUnits.svelte';

	let dateOfImage = null;
	let dateOfBirth = localStorage.getItem('dateOfBirth');;

	$: localStorage.setItem('dateOfBirth', dateOfBirth);
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

	<DateDiffUnits bind:startDate={dateOfBirth} bind:endDate={dateOfImage} />
	<DateDiff bind:startDate={dateOfBirth} bind:endDate={dateOfImage} unit="days" numberOfDecimals=0/>
	<DateDiff bind:startDate={dateOfBirth} bind:endDate={dateOfImage} unit="weeks"/>
	<DateDiff bind:startDate={dateOfBirth} bind:endDate={dateOfImage} unit="months"/>
	<DateDiff bind:startDate={dateOfBirth} bind:endDate={dateOfImage} unit="years"/>
</div>