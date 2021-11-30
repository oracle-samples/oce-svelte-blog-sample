<!--
/**
 * Copyright (c) 2021, Oracle and/or its affiliates.
 * Licensed under the Universal Permissive License v 1.0 as shown at https://oss.oracle.com/licenses/upl/
 */  
-->
<script context="module">
  import { fetchTopicArticles } from "../../scripts/services.js";
  export async function preload(page) {
    const topicId = page.params.slug;
    const topicName = page.query.topicName;
    const articlesData = await fetchTopicArticles(topicId);
    return { topicId, topicName, articlesData };
  }
</script>

<script>
  export let topicId;
  export let topicName;
  export let articlesData;
  import Breadcrumbs from "../../components/Breadcrumbs.svelte";
  import ArticlesListItem from "../../components/ArticlesListItem.svelte";
  let breadcrumbs = [
    {
      linkParams: ".",
      text: "Home",
    },
    {
      linkParams: null,
      text: topicName,
    },
  ];
</script>

<svelte:head>
  <title>Articles</title>
</svelte:head>
<Breadcrumbs {breadcrumbs} />
<div id="articles">
  {#each articlesData.articles as article}
    <ArticlesListItem {article} {topicName} {topicId} />
  {/each}
</div>

