<script>
  import { getContext } from "svelte";

  export let label;
  export let position;
  export let showIcon;
  export let variant;

  const { styleable } = getContext("sdk");
  const component = getContext("component");

  const iconMap = {
    info: "Info",
    positive: "CheckmarkCircle",
    negative: "Alert",
  };

  $: icon = iconMap[variant];
</script>

<div use:styleable={$component.styles}>
  <span class="u-tooltip-showOnHover">
    <slot />
    <div
      class="spectrum-Tooltip spectrum-Tooltip--{variant} spectrum-Tooltip--{position}"
    >
      {#if showIcon}
        <svg
          class="spectrum-Icon spectrum-Icon--sizeM spectrum-Tooltip-typeIcon"
          focusable="false"
          aria-hidden="true"
        >
          <use xlink:href="#spectrum-icon-18-{icon}" />
        </svg>
      {/if}
      <span class="spectrum-Tooltip-label">{label || ""}</span>
      <span class="spectrum-Tooltip-tip" />
    </div>
  </span>
</div>

<style>
  .spectrum-Tooltip {
    width: max-content;
    white-space: normal;
  }
</style>
