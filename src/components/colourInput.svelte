<script>
  import { colour as userColour } from "../scripts/colourStore";
  import { isValidColour } from "../scripts/isValidColour";
  let clipAccess = true;
  const onFocus = () => {
    navigator.clipboard
      .readText()
      .then(async (text) => {
        const validClipboard = isValidColour(text);

        const hexMatchNohash = new RegExp(
          "^((?:[0-9a-f]{3}){1,2})$",
          "i"
        );

        if (validClipboard) {
          const hexMatchNohash = new RegExp(
            "^((?:[0-9a-f]{3}){1,2})$",
            "i"
          );
          if (hexMatchNohash.test(text)) {
            $userColour = `#${text}`;
          } else {
            $userColour = text;
          }
          // reset to empty
          try {
            await navigator.clipboard.writeText("");
          } catch (err) {
            console.error("Cannot reset clipboard", err);
          }
        }
        console.log("Pasted content: ", text);
      })
      .catch((err) => {
        clipAccess = false;
        console.error("Failed to read clipboard contents: ", err);
      });
  };
</script>

<section class="mt-2">
  <p class="font-semibold">
    Enter a colour, get a Tailwind colour name
  </p>

  <div class="block mt-0 text-gray-700">
    Type a hex colour code like
    <code>#FFFFFF</code>
    or
    <code>#ed3939</code>

    {#if !clipAccess}
      <div class="text-yellow-600 my-3">
        Enable Clipboard Access for easy pasting next time
      </div>
    {/if}
  </div>
  <input
    placeholder="#FFFFFF"
    class="block w-48 mt-4 uppercase rounded shadow focus:ring-cyan-800"
    id="colour"
    type="text"
    title="Type a hex colour code"
    on:focus={onFocus}
    bind:value={$userColour}
  />

  <label class="block mt-4 text-gray-700">
    Or select a colour from this colour picker
    <input
      type="color"
      class="block w-20 h-10 mt-2 border-2 rounded shadow appearance-none border-cyan-800"
      bind:value={$userColour}
    />
  </label>
</section>
