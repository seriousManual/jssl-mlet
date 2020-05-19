<script>
	import moment from 'moment';
	import DateDiff from './DateDiff.svelte';

	let dateOfImage = null;
	let dateOfBirth = localStorage.getItem('dateOfBirth');;
	let duration = '';
	let durationDays = 0;
	let durationMonth = 0;
	let durationWeeks = 0;
	let durationYear = 0;
	let durationDiff = ''

	$: localStorage.setItem('dateOfBirth', dateOfBirth);

	$: if (dateOfImage && dateOfBirth) {
		const durationObject = moment.duration(moment(dateOfImage).diff(moment(dateOfBirth)))
		duration = durationObject.locale('de').humanize()
		durationDays = durationObject.as('days').toFixed(0)
		durationWeeks = durationObject.as('weeks').toFixed(1)
		durationMonth = durationObject.as('months').toFixed(1)
		durationYear = durationObject.as('years').toFixed(1)



		const month = Math.floor(durationObject.as('months'))
		durationObject.subtract(month, 'months')
		const weeks = Math.floor(durationObject.as('weeks'))
		durationObject.subtract(weeks, 'weeks')
		const days = Math.floor(durationObject.as('days').toFixed(0))
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

	<div class="form-group">
		<label>Time between dates</label>
		<div>
			<h3>~{duration}</h3>
			<h3>{durationDays} days</h3>
			<h3>{durationWeeks} weeks</h3>
			<h3>{durationMonth} months</h3>
			<h3>{durationYear} years</h3>
			<h3>{durationDiff}</h3>
		</div>
	</div>
	<DateDiff bind:startDate={dateOfBirth} bind:endDate={dateOfImage}/>
</div>