<script>
  import { page } from "$app/stores"
  import SEO from "@components/SEO.svelte"
  import { timeago, formattedDate } from "$lib/util"
  export let title, desc, date, author, tags, thumbnail, published
  const slug = $page.url.pathname.split("/").at(-2)
</script>

<SEO {title} {desc} img={thumbnail} />

<div class="prose prose-sm md:prose-base">
  {#if thumbnail}
    <figure class="w-full">
      <img
        loading="lazy"
        src={thumbnail}
        class="border-base-content bg-base-300 rounded-box border border-opacity-5"
        alt={title}
        style={`view-transition-name: ${slug.replaceAll("%20", "-")}-img`} />
    </figure>
  {/if}
  <div style={`view-transition-name: ${slug.replaceAll("%20", "-")}-text`}>
    <div class="mb-2 text-xs text-base-content/60">
      <span title={formattedDate(date)} class="italic">
        Published {timeago(date)}
      </span>
      {#if author}
        by
        <span>
          {author}
        </span>
      {/if}
    </div>
    {#if title}
      <h1>{title}</h1>
    {/if}
    {#if desc}
      <p>{desc}</p>
    {/if}
    <slot />
  </div>
  {#if published && tags}
    <div class="mb-2 text-xs opacity-60 flex flex-wrap gap-2">
      <span>Tags:</span>
      {#each tags as tag}
        <a class="link" href={`/blog/tag/${tag.replace(/ /g, "-").toLowerCase()}`}>
          {tag}
        </a>
      {/each}
    </div>
  {/if}
</div>
