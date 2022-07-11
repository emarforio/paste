<script lang="ts">
  export let title;
  export let href: string | null = null;
  export let disabled = false;
</script>

{#if disabled}
  <span class="text-slate-500" title="Enter some text before saving"
    >[<button disabled>{title}</button>]</span
  >
{:else if href}
  <span class="text-slate-400 hover:text-yellow-400"
    >[<a class="hover:underline" {href}>{title}</a>]</span
  >
{:else}
  <span class="text-slate-400 hover:text-yellow-400"
    >[<button class="hover:underline" on:click>{title}</button>]</span
  >
{/if}
