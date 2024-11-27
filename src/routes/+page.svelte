<script>
	export let data;
	console.log(data);
  
	import { activeFilter } from "$lib/store";
	import Filters from "$lib/molecules/Filters.svelte";
  
	const techniques = ["Pottery", "Islamic art", "Tapestry", "Glass"];
  </script>
  
  <Filters />
  
  <ul class="masonry">
	{#each data.artObjects as art, index}
	  <li
		class="masonry-item"
		class:hidden={$activeFilter !== "*" &&
		  $activeFilter !== techniques[index % techniques.length]}
		data-category={techniques[index % techniques.length]}
	  >
		<figure>
		  <picture>
			<source
			  srcset={"https://fdnd-agency.directus.app/assets/" +
				art.image +
				".avif"}
			  type="image/avif"
			/>
			<source
			  srcset={"https://fdnd-agency.directus.app/assets/" +
				art.image +
				".webp"}
			  type="image/webp"
			/>
			<img
			  src={"https://fdnd-agency.directus.app/assets/" + art.image}
			  alt={art.title}
			  height={art.height}
			  width={art.width}
			  loading="lazy"
			/>
		  </picture>
		  <figcaption>
			<h2>{art.title}</h2>
		  </figcaption>
		</figure>
	  </li>
	{/each}
  </ul>
  
  <style>
	.masonry {
	  column-count: 1;
	  column-gap: 1rem;
	  list-style: none;
	  padding: 0;
	}
  
	.masonry-item {
	  break-inside: avoid;
	  display: block;
	  background-color: #fff;
	  border-radius: 8px;
	  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
	  margin-bottom: 1rem;
	  position: relative;
	  overflow: hidden;
	  transition: opacity 0.3s;
	}
  
	.masonry-item.hidden {
	  filter: opacity(0.3);
	  pointer-events: none;
	  transition: 1s;
	}
  
	figure {
	  margin: 0;
	  position: relative;
	}
  
	img {
	  width: 100%;
	  height: auto;
	  display: block;
	  border-radius: 8px;
	  transition: transform 0.3s ease-in-out;
	}
  
	figcaption {
	  position: absolute;
	  top: 0;
	  left: 0;
	  width: 100%;
	  height: 100%;
	  background-color: rgba(0, 0, 0, 0.6);
	  color: white;
	  display: flex;
	  flex-direction: column;
	  justify-content: center;
	  align-items: center;
	  opacity: 0;
	  transition: opacity 0.3s ease-in-out;
	}
  
	.masonry-item:hover img {
	  transform: scale(1.1);
	}
  
	.masonry-item:hover figcaption {
	  opacity: 1;
	}
  
	h2 {
	  font-size: 16px;
	  margin: 0.5rem 0;
	  text-align: center;
	  -webkit-text-stroke: 0.2px #ffff00;
	}
  
	/* Responsieve layout */
	@media (min-width: 600px) {
	  .masonry {
		column-count: 2;
	  }
	}
  
	@media (min-width: 900px) {
	  .masonry {
		column-count: 3;
	  }
  
	  h2 {
		font-size: 1.5rem;
	  }
	}
  
	@media (prefers-reduced-motion) {
	  img {
		width: 100%;
		height: auto;
		display: block;
		border-radius: 8px;
	  }
  
	  .masonry-item {
		break-inside: avoid;
		display: block;
		background-color: #fff;
		border-radius: 8px;
		box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
		margin-bottom: 1rem;
		position: relative;
		overflow: hidden;
	  }
  
	  .masonry-item.hidden {
		filter: opacity(0.1);
		pointer-events: none;
	  }
	}
  </style>
  