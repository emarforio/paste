<script>
    let textContent = "";
</script>

<main class="h-full">
    <textarea
        class="bg-slate-800 w-1 h-full text-slate-200 placeholder:text-slate-50"
        placeholder="123"
    ></textarea>
    <textarea
        class="bg-slate-800 w-9 h-full text-slate-50 placeholder:text-slate-50"
        placeholder="Start typing.."
        bind:value={textContent}
    ></textarea>
</main>
