<script lang="ts">
  import { page } from "$app/stores";
  import type { LayoutData } from "./$types";
  import "virtual:windi.css";

  import PreviewBanner from "$lib/components/PreviewBanner.svelte";
  interface Props {
    data: LayoutData;
    children?: import('svelte').Snippet;
  }

  let { data, children }: Props = $props();

  /**
   * Only show the preview banner on the following route id's.
   */
  const previewRouteIds = ["/(app)/posts/[slug]"];

  let { previewMode, previewModeEmbed: embedded } = $derived(data);
  let showPreviewBanner = $derived(previewMode && previewRouteIds.includes($page.route.id || ""));
</script>

{#if showPreviewBanner}
  <PreviewBanner {embedded} />
{/if}

{@render children?.()}
