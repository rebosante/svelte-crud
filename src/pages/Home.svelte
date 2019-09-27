 <script>
 import { onMount } from 'svelte'
 import PostForm from '../components/PostForm.svelte'

 const apiBaseUrl = 'https://ndb99xkpdk.execute-api.eu-west-2.amazonaws.com/dev'
 let posts = []
 onMount(async () => {
   const res = await fetch(apiBaseUrl + '/posts')
   posts = await res.json()
 })
 function editPost(post) {
   console.log(post)
 }
 function deletePost(id) {
   console.log('Deleting post with id:', id)
 }
</script>

{#if posts.length === 0}
  <div class="box">
    <div class="loader-39"></div>
  </div>

{:else}
<div class="container flex flex-col justify-between min-h-screen min-w-full bg-white text-gray-800 leading-normal">
  <main class="w-full w-full container max-w-xl mx-auto p-6">
  <PostForm />
  {#each posts as post}
  <div class="max-w-sm max-w-full lg:flex shadow-inner bg-gray-300 border border-gray-400 rounded-b">
        <div class="p-4 flex flex-col justify-between leading-normal">
          <div class="mb-3">
            <div class="font-bold text-xl mb-2">{post.title}</div>
            <p class="text-gray-700 text-base">{post.body}</p>
          </div>
          <div>
            <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2">{post.createdAt}</span>
          </div>
          <div class="inline-flex mt-4">
            <button on:click="{() => editPost(post)}" class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded-l">
              Edit
            </button>
            <button on:click="{() => deletePost(post.id)}" class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded-r">
              Delete
            </button>
          </div>
        </div>
      </div>
      <br>
    {/each}
    <p class="text-center text-gray-500 text-xs">
        &copy;2019 Reboseitor Corp. All rights reserved.
      </p>
</main>
</div>
{/if}
