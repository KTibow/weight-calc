<script>
  import iconMercury from "$lib/mercury.svg";
  import iconVenus from "$lib/venus.svg";
  import iconMoon from "$lib/moon.svg";
  import iconMars from "$lib/mars.svg";
  import iconJupiter from "$lib/jupiter.svg";
  import iconSaturn from "$lib/saturn.svg";
  import iconUranus from "$lib/uranus.svg";
  import iconNeptune from "$lib/neptune.svg";
  let weight;
  let innerWidth;
  const planets = [
    { name: "Mercury", factor: 0.38, icon: iconMercury },
    { name: "Venus", factor: 0.91, icon: iconVenus },
    { name: "the Moon", factor: 0.165, icon: iconMoon },
    { name: "Mars", factor: 0.38, icon: iconMars },
    { name: "Jupiter", factor: 2.34, icon: iconJupiter },
    { name: "Saturn", factor: 1.06, icon: iconSaturn },
    { name: "Uranus", factor: 0.92, icon: iconUranus },
    { name: "Neptune", factor: 1.19, icon: iconNeptune },
  ];
</script>

<svelte:window bind:innerWidth />
<div class="flex flex-col items-center">
  <h1 class="text-4xl lg:text-6xl font-bold text-center my-8">Planet Weight</h1>
  <div class="flex bg-zinc-800 rounded-xl h-16 overflow-hidden my-8">
    <input
      class="bg-inherit px-4 border-r border-zinc-500 [appearance:textfield]"
      type="number"
      bind:value={weight}
    />
    <span class="self-center px-2">unit of your choice</span>
  </div>
  {#if weight}
    <ul class="lg:flex gap-4 lg:absolute lg:bottom-8">
      {#each planets as planet}
        {#if innerWidth < 1024}
          <li class="h-16 flex whitespace-nowrap items-center">
            <img src={planet.icon} alt="Icon for {planet.name}" class="h-16 w-16" />
            {(weight * planet.factor).toFixed(1)} on {planet.name}
          </li>
        {:else}
          {@const planetWeight = (weight * planet.factor).toFixed(1)}
          <li class="flex flex-col self-end items-center">
            <div class="bg-blue-500 w-20" style="height: {planetWeight}px;" />
            <span class="text-2xl">{planetWeight}</span>
            <img src={planet.icon} alt="Icon for {planet.name}" class="h-20 w-20" />
            {planet.name}
          </li>
        {/if}
      {/each}
    </ul>
  {/if}
</div>
