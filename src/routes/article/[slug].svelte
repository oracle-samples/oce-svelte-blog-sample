<!--
/**
 * Copyright (c) 2021, Oracle and/or its affiliates.
 * Licensed under the Universal Permissive License v 1.0 as shown at https://oss.oracle.com/licenses/upl/
 */
-->
<script context="module">
  import { fetchArticleDetails } from "../../scripts/services.js";
  export async function preload(page) {
    const articleId = page.params.slug;
    const topicId = page.query.topicId;
    const topicName = page.query.topicName;
    const article = await fetchArticleDetails(articleId);
    return { topicId, topicName, article };
  }
</script>

<script>
  import filterXSS from "xss";
  import Breadcrumbs from "../../components/Breadcrumbs.svelte";
  import { dateToMDY } from "../../scripts/utils.js";

  export let topicId;
  export let topicName;
  export let article;

  let formattedDate =
    article.date && article.date.value
      ? `Posted on ${dateToMDY(article.date.value)}`
      : "";
  const options = {
    stripIgnoreTag: true, // filter out all HTML not in the whitelist
    stripIgnoreTagBody: ["script"], // the script tag is a special case, we need
    // to filter out its content
  };
  let cleancontent = filterXSS(article.content, options);
  let breadcrumbs = [
    {
      linkParams: ".",
      text: "Home",
    },
    {
      linkParams: `articles/${topicId}?topicName=${topicName}`,
      text: topicName,
    },
    {
      linkParams: null,
      text: article.name,
    },
  ];
</script>

<svelte:head>
  <title>Article</title>
</svelte:head>
<Breadcrumbs {breadcrumbs} />
<div id="article">
  <div class="author">
    <!-- {/* Avatar */} -->
    <picture>
      <source
        type="image/webp"
        srcset={article.authorRenditionUrls.srcset}
        sizes="80px" />
      <source srcset={article.authorRenditionUrls.jpgSrcset} sizes="80px" />
      <img src={article.authorRenditionUrls.small} alt="Author Avatar" />
    </picture>

    <!-- {/*  Author Name / Date */} -->
    <div class="name_date">
      <h4 class="title">{article.title}</h4>
      <div class="date">{formattedDate}</div>
    </div>
  </div>

  <!-- {/* Article Image and caption */} -->
  <figure>
    <picture>
      <source type="image/webp" srcset={article.renditionUrls.srcset} />
      <source srcset={article.renditionUrls.jpgSrcset} />
      <img src={article.renditionUrls.large} alt="Article"
        width={article.renditionUrls.width}
        height={article.renditionUrls.height}/>
    </picture>
    <figcaption>{article.imageCaption}</figcaption>
  </figure>

  <!-- {/* Article Content */} -->
  <div class="content">
    {@html cleancontent}
  </div>
</div>
