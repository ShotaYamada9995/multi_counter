<script lang="ts">
    import Counter from "./Counter.svelte";
    let counterList: { id: number; count: number; title: string }[] = [
        { id: Date.now(), count: 0, title: "new" },
    ];

    function addCounter() {
        let newCounter = {
            id: Date.now(),
            count: 0,
            title: "new",
        };
        counterList = [...counterList, newCounter];
    }

    function removeCounter(id: number) {
        counterList = counterList.filter((counter) => counter.id !== id);
    }
    let sum: number = 0;
    $: {
        sum = counterList.reduce((sum, counter) => sum + counter.count, 0);
    }
    function handleCountChange() {
        sum = counterList.reduce((sum, counter) => sum + counter.count, 0);
    }
    function handleTitleChange() {
        counterList = [...counterList];
    }
</script>

<section>
    {#each counterList as counter (counter.id)}
        <Counter
            {counter}
            {removeCounter}
            on:countChange={handleCountChange}
            on:titleChange={handleTitleChange}
        />
    {/each}
    <button
        on:click={addCounter}
        class="max-w-sm w-full m-auto text-center bg-green-400 rounded text-white cursor-pointer"
    >
        new counter
    </button>
    <p>
        title list:
        {#each counterList as title, index}
            {#if index > 0}, {/if}
            {title.title}
        {/each}
    </p>
    <p>total sum: {sum}</p>
</section>

<style>
</style>
