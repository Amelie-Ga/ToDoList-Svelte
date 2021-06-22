<script>
  import { fade, fly } from 'svelte/transition';

  let todos = [];
  let task = "";
  let active = false;

  let addTask = () => {
    if(task.length >= 1){
    todos = [...todos, task];
    task = "";
    }
  }

  let taskCompleted = () => {
    active = !active; 
  }

  let taskDeleted = (index) => {
    todos.splice(index, 1);
    todos = [...todos]
  }

</script>

<main class="w-screen h-screen px-16 py-8 font-sans bg-gray-100">
  <div class="p-8 mx-8 bg-white rounded-lg shadow-md">
    <h1 class="fontConeria flex justify-center text-3xl text-pink-400">To Do List</h1>

    <form class="flex justify-center mt-1" on:submit|preventDefault={addTask}>

      <input type="text" id="task" class="rounded-md bg-pink-200 m-1 p-2 focus:outline-none fontJosefin" bind:value={task}/>

      <button type="submit" class="bg-pink-400 text-white rounded-md m-1 p-2 fontJosefin focus:outline-none hover:bg-pink-300">Add</button>

    </form>



    {#each todos as todo, index}

      <div class=" text-pink-400 bg-pink-50 mr-40 ml-40 rounded-md">
        <div class="flex flex-row justify-between items-center m-2 p-2" in:fly="{{x: index % 2 ? 200 : -200, duration: 2000}}" out:fade>
              <p class="mr-10 flex flex-start fontJosefin">{todo}<p>

              <button class="focus:outline-none" on:click={()=>taskCompleted(index)}>
                {#if active}
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" viewBox="0 0 20 20" fill="currentColor">
                    <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
                  </svg>
                  
                {:else}

                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 hover:text-green-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                {/if}
              </button>

      
              <button class="focus:outline-none hover:text-red-600" on:click={()=>taskDeleted(index)}>
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
              </button>

        </div>
      </div>
    {:else}
      <p class="mt-3 text-2xl text-center fontJosefin text-gray-300">Nothing to do</p>
    {/each}
  </div>
</main>

<style global lang="postcss">
  @tailwind base;
  @tailwind components;
  @tailwind utilities;

  @font-face {
    font-family: 'Coneria';
    font-style: normal;
    font-weight: 600;
    src: url('/font/Demo_ConeriaScript.ttf')
  }

  .fontConeria {
    font-family: 'Coneria';
  }

  @font-face {
    font-family: 'Josefin';
    font-style: normal;
    font-weight: 600;
    src: url('/font/JosefinSans-Regular.ttf')
  }

  .fontJosefin {
    font-family: 'Josefin';
  }

</style>