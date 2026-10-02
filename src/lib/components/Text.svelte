<script lang="ts">
    import { supabase } from '#lib/supabaseClient.js';
    import { invalidateAll } from '$app/navigation';

    let content = $state("");
    let user = $state("");

    async function post() {
        // TASK 2: Post Messages
           const { error } = await supabase
          .from('posts')
          .insert({
            username: user,
            content: content
          });

        if (error) {
          console.log(error.message);
          return;
        }

          content = "";
         await invalidateAll();
        }


</script>

<div class="container">
    <input bind:value={user} type="text" placeholder="Name">
    <div class="post-container">
            <input bind:value={content} type="text" placeholder="Post">
    <button onclick={post}>Post</button>
    </div>

</div>
