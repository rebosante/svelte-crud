<script>
  let title = ''
  let body = ''
  const apiBaseUrl = 'https://ndb99xkpdk.execute-api.eu-west-2.amazonaws.com/dev'

  async function onSubmit(event){
    event.preventDefault()
    if(title.trim() === '' || body.trim() === '') {
      return
    }
    const newPost = {title, body}
    const res = await fetch(`${apiBaseUrl}/post`,{
      method: 'POST',
      body: JSON.stringify(newPost)
    })
    const post = await res.json()
  }
</script>
<div class="w-full">
  <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4" on:submit={onSubmit}>
    <div class="mb-4">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="title">
        Title
      </label>
      <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" name="title" type="text" bind:value={title} placeholder="Title">
    </div>
    <div class="mb-6">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="body">
        Body
      </label>
      <textarea class="shadow appearance-none border border-red-500 rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline" name="body" type="text" bind:value={body} placeholder="Body"></textarea>
      <!--<p class="text-red-500 text-xs italic">Please choose a password.</p>-->
    </div>
    <div class="flex items-center justify-between">
      <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="submit">
        Post
      </button>
    </div>
  </form>
</div>