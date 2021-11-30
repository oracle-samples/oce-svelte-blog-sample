<!--
/**
 * Copyright (c) 2021, Oracle and/or its affiliates.
 * Licensed under the Universal Permissive License v 1.0 as shown at https://oss.oracle.com/licenses/upl/
 */  
-->
<script context="module">
  import { getTopicsListPageData } from "../scripts/services.js";
  export async function preload() {
    const data = await getTopicsListPageData();
    return { data };
  }
</script>

<script>
  export let data;
  import Header from "../components/Header.svelte";
  import TopicsListItem from "../components/TopicsListItem.svelte";
</script>

<svelte:head>
  <title>Topics</title>
</svelte:head>
{#if data}
  <Header
    companyTitle={data.companyTitle}
    companyThumbnailRenditionUrls={data.companyThumbnailRenditionUrls}
    aboutUrl={data.aboutUrl}
    contactUrl={data.contactUrl} />
  <div id="topics">
    {#each data.topics as topic}
      <TopicsListItem
        id={topic.id}
        name={topic.name}
        description={topic.description}
        renditionUrls={topic.renditionUrls} />
    {/each}
  </div>
{/if}
