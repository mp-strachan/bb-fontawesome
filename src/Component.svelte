<script>
  import { getContext } from "svelte"

  import Icon from 'svelte-awesome';

  // UNCOMMENT FOR FONT AWESOME FREE
  import * as far from '@fortawesome/free-regular-svg-icons';
  import * as fas from '@fortawesome/free-solid-svg-icons';

  // UNCOMMENT FOR FONT AWESOME PRO
  // import * as far from '@fortawesome/pro-regular-svg-icons';
  // import * as fas from '@fortawesome/pro-solid-svg-icons';
  // import * as fal from '@fortawesome/pro-light-svg-icons';
  // import * as fat from '@fortawesome/pro-thin-svg-icons';

  const { styleable } = getContext("sdk")
  const component = getContext("component")

  export let iconStyle;
  export let iconName;
  export let iconScale;
  export let iconSubScale;
  export let iconColour;
  export let iconFlip;
  export let iconAnimate;

  let faStyle;

  $: switch (iconStyle) {
    case "Solid":
      faStyle = fas;
      break;
    case "Regular":
      faStyle = far;
      break;
    // UNCOMMENT FOR FONT AWESOME PRO
    // case "Light":
    //   faStyle = fal;
    //   break;
    // case "Thin":
    //   faStyle = fat;
    //   break;
    default:
      faStyle = far;
  }

  $: faName = "fa" + iconName.split("-").map((word) => {
    return word[0].toUpperCase() + word.substring(1);
  }).join("");

  $: fScale = iconScale + (iconSubScale / 100);
</script>

<div use:styleable={$component.styles}>
  {#if iconAnimate === "Spin"}
    <Icon class="faIcon" data={faStyle[faName]} scale="{fScale}" flip="{iconFlip.toLowerCase()}" spin style="color: {iconColour}"/>
  {:else if iconAnimate === "Pulse"}
    <Icon class="faIcon" data={faStyle[faName]} scale="{fScale}" flip="{iconFlip.toLowerCase()}" pulse style="color: {iconColour}"/>
  {:else}
    <Icon class="faIcon" data={faStyle[faName]} scale="{fScale}" flip="{iconFlip.toLowerCase()}" style="color: {iconColour}"/>
  {/if}
</div>

<style></style>
