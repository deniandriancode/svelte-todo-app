<script>

  import ListItem from "./ListItem.svelte";

  let task = "";
  let taskId = 0;
  let taskList = [];

  function addTask() {
	if (task.trim().length == 0) {
	  return;
	}
	
	let newTaskObj = {
	  id: taskId,
	  content: task,
	  isChecked: false
	};

	taskId += 1;
	task = "";

	taskList = [...taskList, newTaskObj];
  }

  function deleteTask(event) {
	taskList = taskList.filter((i) => {
	  return i.id != event.detail.targetId;
	});
  }
  
</script>

<h1>Svelte todo-list app</h1>

<form on:submit|preventDefault={addTask}>
  <input type="text" bind:value={task}/>
  <button type="submit">Add</button>
</form>

<div>
  {#if taskList.length == 0}
	<p>No task currently</p>
  {:else}
	<p>Current task:</p>
	<ul>
	  {#each taskList as t (t.id)}
		<ListItem {...t} on:deleteCurrentTask={deleteTask} />
	  {/each}
	</ul>
  {/if}
</div>
