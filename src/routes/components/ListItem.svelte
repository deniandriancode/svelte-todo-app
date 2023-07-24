<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();
  
  export let id;
  export let content;
  export let isChecked;

  function del() {
	dispatch("deleteCurrentTask", {
	  targetId: id
	});
  }
</script>

<li>
  <label class:finished={isChecked}>
	<input type="checkbox" bind:checked={isChecked} />
	{content}
  </label>
  <button on:click={del}>x</button>
</li>


<style>
  .finished {
	text-decoration: line-through;
  }
</style>
