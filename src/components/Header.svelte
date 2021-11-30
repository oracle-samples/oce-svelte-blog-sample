<!--
/**
 * Copyright (c) 2021, Oracle and/or its affiliates.
 * Licensed under the Universal Permissive License v 1.0 as shown at https://oss.oracle.com/licenses/upl/
 */
-->
<script>
  export let companyTitle;
  export let companyThumbnailRenditionUrls;
  export let aboutUrl;
  export let contactUrl;
</script>

<div class="logo" data-testid="Header">
  <picture id="company-thumbnail">
    <source
      type="image/webp"
      srcset={companyThumbnailRenditionUrls.srcset}
      sizes="(max-width: 480px) 60vw, 25vw" />
    <img src={companyThumbnailRenditionUrls.native} alt="Company icon" width="{companyThumbnailRenditionUrls.width*.85}" height="{companyThumbnailRenditionUrls.height*.85}"/>
  </picture>
  <h1 id="company-title">{companyTitle}</h1>
  <ul>
    <li><a id="about" href={aboutUrl}>About Us</a></li>
    <li><a id="contact" href={contactUrl}>Contact Us</a></li>
  </ul>
</div>
