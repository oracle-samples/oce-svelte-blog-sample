<!--
/**
 * Copyright (c) 2021, Oracle and/or its affiliates.
 * Licensed under the Universal Permissive License v 1.0 as shown at https://oss.oracle.com/licenses/upl/
 *
 * Component representing an Article List Item displayed in the list of articles.
 *
 * @param {string} topicId The Topic to which the Article belongs, used when creating
 *                         the link to the article details
 * @param {string} topicName The Topic name, used to render breadcrumbs
 * @param {object} article The Article to display
 */ -->
<script>
  import { dateToMDY } from "../scripts/utils.js";
  export let article;
  export let topicName;
  export let topicId;
  const formattedDate = `Posted on ${dateToMDY(
    article.fields.published_date.value
  )}`;
</script>

<!-- whole view is wrapped in a link component with the URL of the format
       articles/articleId?topicName=name&topicId=id -->
<a
  sapper:prefetch
  href="article/{article.id}?topicId={topicId}&topicName={topicName}"
  style={{ textDecoration: 'none' }}>
  <div class="article">
    <div class="title-date">
      <h4 class="title">{article.name}</h4>
      <div class="date">{formattedDate}</div>
    </div>
    <picture>
      <source
        type="image/webp"
        srcset={article.renditionUrls.srcset}
        sizes="80px" />
      <source srcset={article.renditionUrls.jpgSrcset} sizes="80px" />
      <img src={article.renditionUrls.small} alt="Article thumbnail"
        width={article.renditionUrls.width}
        height={article.renditionUrls.height}/>
    </picture>

    <div class="description">{article.description}</div>
  </div>
</a>
