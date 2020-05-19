<script>
	import moment from 'moment';

	export let startDate = null;
	export let endDate = null;
	export let unit = 'days';
	export let numberOfDecimals = 1;

	let duration = null;

	$: if (startDate && endDate) {
		duration = moment.duration(moment(endDate).diff(moment(startDate))).as(unit).toFixed(numberOfDecimals)
	} else {
		duration = null
	}

</script>

{#if duration}
<div>
	{duration} {unit}
</div>
{/if}