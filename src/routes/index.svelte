<script>
  import { isValidColour } from "../scripts/isValidColour";

  import ColourInput from "../components/colourInput.svelte";
  import ColourResult from "../components/tailwindResult.svelte";

  import { colour as userColour } from "../scripts/colourStore";
</script>

<svelte:head>
  <title>Find the nearest Tailwind Colour</title>
</svelte:head>

<header
  class="p-4 mt-3 pb-5  text-indigo-800 sm:rounded text-center border-b border-gray-200"
>
  <h1 class="leading-none text-indigo-800 font-bold tracking-tight">
    Tailwind colour
  </h1>
  <p class="mt-2 text-gray-500">
    A tool to find the nearest colour from
    <a href="https://tailwindcss.com/docs/customizing-colors">
      the Tailwind colour palette</a
    >
  </p>
  <p class="mt-2 text-sm text-indigo-800" style="">
    For Tailwind CSS v3.0
  </p>
</header>

<main>
  <section class="mt-8">
    <ColourInput />
  </section>

  {#if $userColour != null && isValidColour($userColour)}
    <section class="mt-10">
      <ColourResult />
    </section>
  {/if}
</main>

<footer
  class="p-4 mt-8 -ml-4 -mr-4 sm:rounded text-gray-400  border-top-4 text-center text-xs"
>
  <p class="mt-0">
    Powered by <a href="https://web3templates.com/">Web3Templates</a>
  </p>

  <p>
    <a href="https://edjohnsonwilliams.co.uk/">Author</a> |
    <a href="https://github.com/web3templates/tailwind-color"
      >Github</a
    >
  </p>
</footer>
