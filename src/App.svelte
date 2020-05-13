<script>
	import moment from 'moment';

	let date1 = localStorage.getItem('date1');
	let date2 = null;
	let duration = '';

	$: localStorage.setItem('date1', date1);

	$: if (date1 && date2) {
		duration = moment.duration(moment(date1).diff(moment(date2))).humanize();
	}
</script>

<div>
	<input type="date" bind:value={date2}>
	<input type="date" bind:value={date1}>

	<div>
		{duration} 
	</div>
</div>