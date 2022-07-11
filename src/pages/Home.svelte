<script>
    let textContent = "";

    function getLineNumbers(length) {
        return Array.from({ length })
            .map((_, i) => i + 1)
            .join("\n");
    }

    function save() {
        alert("It works");
    }

    $: lineCount = textContent.split("\n").length;
    $: lineNumbers = getLineNumbers(lineCount);
    $: console.log(lineCount);
</script>

<div class="flex flex-col h-full">
    <nav class="sticky top-0 px-3 py-1 bg-slate-900 text-slate-500 font-mono">
        <span class="hover:text-yellow-400"
            >[<button on:click={save} class="hover:underline">Save</button
            >]</span
        >
    </nav>

    <main class="flex overflow-scroll-y grow">
        <div
            id="lines"
            class="w-min px-3 py-3 bg-slate-800 text-slate-600 text-right font-mono"
        >
            {lineNumbers}
        </div>
        <textarea
            class="bg-slate-800 w-full px-1 py-3 text-slate-100 placeholder:text-slate-500 font-mono"
            placeholder="Start typing.."
            wrap="off"
            bind:value={textContent}
        />
    </main>
</div>

<style>
    textarea {
        resize: none;
        outline: none;
    }
</style>
