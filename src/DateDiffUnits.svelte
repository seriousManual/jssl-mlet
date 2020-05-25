<script>
	import moment from 'moment';
	import { afterUpdate } from 'svelte';

	export let startDate = null;
	export let endDate = null;
	const units = ['years', 'months', 'weeks', 'days'];

	let duration = '';

	afterUpdate( () => {
		if (startDate && endDate) {
			const durationObject = moment.duration(moment(endDate).diff(moment(startDate)))
			const strings = []

			units.forEach(unit => {
				const number = Math.floor(durationObject.as(unit))
				durationObject.subtract(number, unit)
				strings.push(number + unit.substring(0,1))
			})

			duration = strings.join(' ')
		} else {
			duration = null
		}
	})
</script>

{#if duration}
<div>
	{duration}
</div>
{/if}