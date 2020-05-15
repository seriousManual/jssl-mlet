<script>
	import moment from 'moment';

	let doi = null;
	let dob = localStorage.getItem('dob');;
	let duration = '';

	$: localStorage.setItem('dob', dob);

	$: if (doi && dob) {
		duration = moment.duration(moment(doi).diff(moment(dob))).humanize();
	}
</script>

<div>
	<input type="date" bind:value={dob}>
	<input type="date" bind:value={doi}>

	<div>
		{duration} 
	</div>
</div>