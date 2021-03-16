<script context="module" lang="ts">
  import { client } from "../../components/SanityClient";

  export async function preload() {
    const query = "*[_type == 'post']{_id, slug, title}";
    const posts = await client.fetch(query);
    return { posts };
  }
</script>

<script lang="ts">
  type Slug = {
    _type: string;
    current: string;
  };

  export let posts: { slug: Slug; title: string }[] = [];
</script>

<h1>Recent posts</h1>
<ul>
  {#each posts as post}
    <li><a rel="prefetch" href="blog/{post.slug.current}">{post.title}</a></li>
  {/each}
</ul>
