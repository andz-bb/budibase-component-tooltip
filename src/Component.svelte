<script>
  import { getContext } from "svelte";

  export let label;
  export let position;
  export let showIcon;
  export let variant;

  const { styleable } = getContext("sdk");
  const component = getContext("component");

  const iconMap = {
    info: "info",
    positive: "check-circle",
    negative: "warning",
  };

  $: icon = iconMap[variant];
</script>

<div use:styleable={$component.styles}>
  <span class="u-tooltip-showOnHover">
    <slot />
    <div
      class="spectrum-Tooltip spectrum-Tooltip--{variant} spectrum-Tooltip--{position}"
    >
      {#if showIcon && icon}
        <i class="spectrum-Tooltip-typeIcon ph ph-{icon}" aria-hidden="true"
        ></i>
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
    z-index: 9999;
  }

  .spectrum-Tooltip-typeIcon.ph {
    align-items: center;
    align-self: center;
    color: currentColor;
    display: inline-flex;
    font-size: 1.33em;
    height: 1.33em;
    justify-content: center;
    line-height: 1;
    width: 1.33em;
  }
</style>
