<script>
	import { onMount } from 'svelte';
	import * as d3 from 'd3';
	import cloud from 'd3-cloud';

	let container;

	onMount(() => {
		function wordCloud(selector) {
			// Color scale
			const fill = d3.scaleOrdinal(d3.schemeCategory10);

			// Create the SVG container
			const svg = d3
				.select(selector)
				.append('svg')
				.attr('width', 600)
				.attr('height', 600)
				.append('g')
				.attr('transform', 'translate(400,400)'); // Center the group

			// Draw function to display words
			function draw(words) {
				const text = svg.selectAll('text').data(words);

				// Enter new words
				text
					.enter()
					.append('text')
					.attr('text-anchor', 'middle')
					.style('font-family', 'Impact')
					.style('fill', (d) => d.color || fill(d.text)) // Use custom color or fallback
					.attr('font-size', 1)
					.text((d) => d.text)
					.transition()
					.duration(1000)
					.style('font-size', (d) => `${d.size}px`)
					.attr('transform', (d) => `translate(${d.x}, ${d.y})rotate(${d.rotate})`);

				// Remove old words
				text.exit().remove();
			}

			return {
				update: function (words) {
					cloud()
						.size([600, 600])
						.words(words)
						.padding(5) // Increased padding for better spacing
						.rotate(() => 0) // All words horizontal
						.font('Impact')
						.fontSize((d) => d.size) // Font size based on word size
						.on('end', draw)
						.start();
				}
			};
		}

		// Fixed word list
		const words = [
			{ text: 'DirtyCop', size: 20, color: '#c48bf0' },
			{ text: 'ByronicHero', size: 19, color: '#c48bf0' },
			{ text: 'PsychoForHire', size: 14, color: '#c48bf0' },
			{ text: 'HenpeckedHusband', size: 12, color: '#c48bf0' },
			{ text: 'MasterSwordman', size: 10, color: '#c48bf0' },
			{ text: 'CorruptCorporateExecutive', size: 9, color: '#c48bf0' }
		];

		// Create and render the word cloud
		const myWordCloud = wordCloud(container);
		myWordCloud.update(words);
	});
</script>

<div bind:this={container}></div>

<style>
	svg {
		width: 100%;
		height: 100%;
	}
</style>
