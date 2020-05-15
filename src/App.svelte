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
	<div class="form-group">
		<label>Date of birth</label>
		<input type="date" class="form-control" bind:value={dob}>
	</div>

	<div class="form-group">
		<label>Date of image</label>
		<input type="date" class="form-control" bind:value={doi}>
	</div>

	<div class="form-group">
		<label>Time between dates</label>
		<br/>
		{duration} 
	</div>
</div>