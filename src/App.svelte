<script>
	import moment from 'moment';

	let dateOfImage = null;
	let dateOfBirth = localStorage.getItem('dateOfBirth');;
	let duration = '';

	$: localStorage.setItem('dateOfBirth', dateOfBirth);

	$: if (dateOfImage && dateOfBirth) {
		duration = moment.duration(moment(dateOfImage).diff(moment(dateOfBirth))).humanize();
	}
</script>

<div>
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
		<br/>
		{duration} 
	</div>
</div>