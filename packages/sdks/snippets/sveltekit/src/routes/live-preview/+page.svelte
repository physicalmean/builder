<script lang="ts">
  import type { BuilderContent } from '@builder.io/sdk-svelte';
  import { onMount } from 'svelte';
  import { subscribeToEditor } from '@builder.io/sdk-svelte';

  let content: BuilderContent | null = null;

  onMount(() => {
    let unsubscribe = subscribeToEditor({
      model: 'blog-data',
      apiKey: 'ee9f13b4981e489a9a1209887695ef2b',
      callback(updatedContent) {
        content = updatedContent;
      },
    });

    return () => unsubscribe();
  });
</script>

{#if content}
  <div class="blog-data-preview">
    <div>Blog Title: {content.data?.title}</div>
    <div>Authored by: {content.data?.author}</div>
    <div>Handle: {content.data?.handle}</div>
  </div>
{/if}
