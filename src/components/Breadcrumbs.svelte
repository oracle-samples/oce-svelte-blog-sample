<!--
/**
 * Copyright (c) 2021, Oracle and/or its affiliates.
 * Licensed under the Universal Permissive License v 1.0 as shown at https://oss.oracle.com/licenses/upl/
 */
 * Component representing a set of breadcrumbs.
 * @param {array} breadcrumbsData the list of objects for each breadcrumb
-->
<script>
  export let breadcrumbs;
</script>

<div id="breadcrumb">
  <ul>
    {#each breadcrumbs as breadcrumb}
      <li>
        {#if breadcrumb.linkParams}
          <a sapper:prefetch href={breadcrumb.linkParams}>{breadcrumb.text}</a>
        {:else}{breadcrumb.text}{/if}
      </li>
    {/each}
  </ul>
</div>
