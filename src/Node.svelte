<!-- Node.svelte -->
<script>
    import { slide } from 'svelte/transition';
	import ClosedIcon from './ClosedIcon.svelte';
	import OpenedIcon from './OpenedIcon.svelte';
	export let node;
	export let level = 0;
    export let slot;
	
	function toggle() {
		node.expanded = !node.expanded;
        return false;
	}
</script>

<li on:click|stopPropagation={toggle} transition:slide class="{ node.expanded ? 'expanded' : 'collapsed'}">
    {#if node.children || node.slots }
        {#if !node.expanded }
            <ClosedIcon/>
        {:else }
            <OpenedIcon/>
        {/if}
    {/if}
    {#if slot }
        <strong>{slot}:</strong>
    {/if}
	<span>{ node.type }</span>

    {#if node.children || node.slots }
        <ul class="tree">
        {#if node.expanded && node.slots}
            {#each Object.entries(node.slots) as [slot, child]}
                <svelte:self node={child} level={level+1} slot={slot}/>
            {/each}
        {/if}

        {#if node.expanded && node.children}
            {#each node.children as child}
                <svelte:self node={child} level={level+1} slot={null}/>
            {/each}
        {/if}
        </ul>
    {/if}

</li>



<style>
li {
    font-size: 0.9rem;
}
li > span {
    padding: 0.1rem 0.5rem;
    margin-left: 0.5em;
}
li > strong {
    padding: 0.2rem 0 0 0.4rem;
}
li > span {
    background-color: rgba(0,0,0,0.1);
    border-radius: 0.3rem;
}
li.expanded > span {
    background-color: #999;
    color: white;
    border-radius: 0.3rem;
}
</style>