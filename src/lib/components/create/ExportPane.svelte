<script type="ts">
  import type { ITheme } from "$lib/data/Themes";
  import type { ViewParameter } from "$lib/data/types/ViewParameter";
  import { adjustLightness } from "$lib/utils/ColorUtils";
  import { quadOut } from "svelte/easing";
  import { fly } from "svelte/transition";
  import { requestExport, stringifyViewParameters } from "$lib/utils/ExportUtils";
  import ActionBtn from "../common/ActionBtn.svelte";

  export let currentTheme: ITheme;
  export let designerPaneWidth: number = 367;
  export let viewParameters: ViewParameter[] = [];

  const onExport = (): void => {
    const payload: string = stringifyViewParameters("simpleborder", viewParameters);
    requestExport(payload);
  };
</script>

<article
  style="
  background: {currentTheme.primary};
  left: {designerPaneWidth}px;"
  transition:fly={{ duration: 180, easing: quadOut, x: -20 }}
>
  This is where options shall be!<br />
  <ActionBtn
    backgroundColor={adjustLightness(currentTheme.tertiary, -25)}
    clickFunc={() => onExport()}
    {currentTheme}
    text="Export"
  />
</article>

<style>
  article {
    position: absolute;
    top: 80px;
    min-width: 8rem;
    padding: 1rem;
    border-radius: 0 0.3rem 0.3rem 0;
  }
</style>
