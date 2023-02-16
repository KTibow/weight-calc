<script>
  import iconApple from "$lib/icons/apple.svg";
  import iconBasketball from "$lib/icons/basketball.svg";
  import iconBicycle from "$lib/icons/bicycle.svg";
  import iconGiraffe from "$lib/icons/giraffe.svg";
  import iconPerson from "$lib/icons/person.svg";

  import iconMercury from "$lib/planets/mercury.svg";
  import iconVenus from "$lib/planets/venus.svg";
  import iconMoon from "$lib/planets/moon.svg";
  import iconMars from "$lib/planets/mars.svg";
  import iconJupiter from "$lib/planets/jupiter.svg";
  import iconSaturn from "$lib/planets/saturn.svg";
  import iconUranus from "$lib/planets/uranus.svg";
  import iconNeptune from "$lib/planets/neptune.svg";
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
  const exampleObjects = [
    { icon: iconApple, name: "Apple", kg: 0.15 },
    { icon: iconBasketball, name: "Basketball", kg: 0.6237 },
    { icon: iconBicycle, name: "Bicycle", kg: 10 },
    { icon: iconGiraffe, name: "Giraffe (male)", kg: 1192 },
    { icon: iconPerson, name: "Person", kg: 70 },
  ];
  let kgOut = false;
</script>

<svelte:window bind:innerWidth />
<div class="flex flex-col items-center">
  <h1 class="text-4xl lg:text-6xl font-bold text-center my-8">Planet Weight</h1>
  <div class="flex flex-wrap mt-8 gap-8 justify-center">
    <button
      class="bg-zinc-800 h-16 w-16 rounded-2xl inline-flex items-center justify-center hover:bg-zinc-700 transition-all"
      on:click={() => (kgOut = !kgOut)}
    >
      out<br />{kgOut ? "kg" : "lb"}
    </button>
    <div class="flex bg-zinc-800 rounded-xl h-16 overflow-hidden">
      <input
        class="bg-inherit px-4 border-r border-zinc-500 [appearance:textfield]"
        type="number"
        bind:value={weight}
      />
      <span class="self-center px-2">kg</span>
    </div>
    <div class="flex h-16 border-zinc-500 border-2 rounded-xl overflow-hidden">
      {#each exampleObjects as { icon, name, kg }}
        <button
          class="p-2 hover:bg-zinc-800 transition-all inline-flex flex-col items-center"
          on:click={() => (weight = kg.toFixed(2))}
        >
          <img src={icon} alt="Icon for apple" class="h-6 w-6" />
          {name}
        </button>
      {/each}
    </div>
  </div>
  {#if weight}
    <p class="mb-8">or {(weight * 2.20462).toFixed(2)} lb</p>
    <ul class="lg:flex gap-4 lg:absolute lg:bottom-8">
      {#each planets as planet}
        {@const planetWeight = (weight * (kgOut ? 1 : planet.factor)).toFixed(1)}
        {#if innerWidth < 1024}
          <li class="h-16 flex whitespace-nowrap items-center">
            <img src={planet.icon} alt="Icon for {planet.name}" class="h-16 w-16" />
            {planetWeight}
            {kgOut ? "kg" : "lb"} on {planet.name}
          </li>
        {:else}
          <li class="flex flex-col self-end items-center">
            <div class="bg-blue-500 w-20" style="height: {planet.factor * 10}vh;" />
            <span class="text-2xl">{planetWeight} {kgOut ? "kg" : "lb"}</span>
            <img src={planet.icon} alt="Icon for {planet.name}" class="h-20 w-20" />
            {planet.name}
          </li>
        {/if}
      {/each}
    </ul>
  {/if}
</div>
