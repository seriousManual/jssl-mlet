<script>
	import moment from 'moment';

	export let startDate;
	export let endDate;
	export let unit = 'days';

	let duration = 0;
	const numberOfDecimals = 1;

	$: if (startDate && endDate) {
		duration = moment.duration(moment(endDate).diff(moment(startDate))).as(unit).toFixed(numberOfDecimals)
	}

</script>

{duration} {unit}