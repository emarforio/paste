<script lang="ts">
  export let title: string;
  export let href: string | null = null;
  export let disabled = false;
</script>

{#if disabled}
  <span class="text-slate-500" title="Enter some text before saving"
    >[<button disabled>{title}</button>]</span
  >
{:else if href}
  <span class="text-slate-400 hover:text-yellow-400"
    >[<a class="underline underline-offset-1" {href}>{title}</a>]</span
  >
{:else}
  <span class="text-slate-400 hover:text-yellow-400"
    >[<button class="underline underline-offset-1" on:click>{title}</button
    >]</span
  >
{/if}
