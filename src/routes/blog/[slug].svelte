<script context="module" lang="ts">
  import { client } from "../../components/SanityClient";

  export async function preload({ params: { slug } }) {
    console.log("preloading...", slug);
    const query = `*[slug.current == "${slug}"]`;
    const res = await client.fetch(query);
    const post = await res.shift(); // research shift()
    return { post };
  }
</script>

<script lang="ts">
  import snarkdown from "snarkdown";
  export let post: { slug: string; title: string; body: string };

  console.log("post.body", post.body);
</script>

<h1>{post.title}</h1>

<div class="content">
  {#if typeof post.body === "string" || post.body !== undefined}
    {@html snarkdown(post.body)}
  {/if}
</div>
