<script lang="ts">
  export let value: string;
  export let readonly = false;

  function getLineNumbers(length: number) {
    return Array.from({ length })
      .map((_, i) => i + 1)
      .join("\n");
  }

  $: lineCount = value.split("\n").length;
  $: lineNumbers = getLineNumbers(lineCount);
</script>

<main class="flex overflow-scroll-y grow">
  <div
    id="lines"
    class="w-min px-3 py-3 bg-slate-800 text-slate-600 text-right font-mono"
  >
    {lineNumbers}
  </div>
  <textarea
    class="resize-none outline-none bg-slate-800 w-full px-1 py-3 text-slate-100 placeholder:text-slate-500 font-mono"
    placeholder="Start typing.."
    wrap="off"
    bind:value
    {readonly}
  />
</main>
