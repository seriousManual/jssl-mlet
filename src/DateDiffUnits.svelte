<script>
	import moment from 'moment';

	export let startDate = null;
	export let endDate = null;
	const units = ['years', 'months', 'weeks', 'days'];

	let duration = '';

	$: if (startDate && endDate) {
		const durationObject = moment.duration(moment(endDate).diff(moment(startDate)))

		const strings = units.map( unit => {
			const number = Math.floor(durationObject.as(unit))
			durationObject.subtract(number, unit)
			return number + unit.substring(0, 1)
		})

		duration = strings.join(' ')
	}
</script>

{#if duration}
<div>
	{duration}
</div>
{/if}