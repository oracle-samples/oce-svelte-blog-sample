<!--
/**
 * Copyright (c) 2021, Oracle and/or its affiliates.
 * Licensed under the Universal Permissive License v 1.0 as shown at https://oss.oracle.com/licenses/upl/
 */  
 * Component representing a Topic displayed in the list of topics.
-->
<script>
  export let id;
  export let name;
  export let description;
  export let renditionUrls;
</script>

<a sapper:prefetch href="articles/{id}?topicName={name}">
  <div class="topic">
    <div class="button-wrapper">
      <div class="button">{name}</div>
    </div>
    <picture>
      <source type="image/webp" srcset={renditionUrls.srcset} sizes="300px" />
      <source srcset={renditionUrls.jpgSrcset} sizes="300px" />
      <img src={renditionUrls.thumbnail} alt="Topic Thumbnail" />
    </picture>
    <div class="desc-wrapper">
      <div class="description">{description}</div>
    </div>
  </div>
</a>
