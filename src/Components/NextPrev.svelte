<script lang="ts">
  import { openOrSwitch, hoverPreview } from "obsidian-community-lib";
  import type { SquareItem } from "../interfaces";
  import type BCPlugin from "../main";
  import { linkClass } from "../Utils/ObsidianUtils";

  export let plugin: BCPlugin;
  export let next: SquareItem[];
  export let prev: SquareItem[];

  const activeLeafView = app.workspace.activeLeaf.view;
</script>

<div class="BC-NextPrev-Container">
  <div class="BC-prevs">
    <span>
      {#each prev as { field, real, to }}
        <div
          class="{linkClass(to, real)} BC-prev"
          on:click={async (e) => await openOrSwitch(to, e)}
          on:mouseover={(e) => hoverPreview(e, activeLeafView, to)}
        >
          <strong>{field}</strong>
          {to}
        </div>
      {/each}
    </span>
  </div>
  <div class="BC-nexts">
    <span>
      {#each next as { field, real, to }}
        <div
          class="{linkClass(to, real)} BC-next"
          on:click={async (e) => await openOrSwitch(to, e)}
          on:mouseover={(e) => hoverPreview(e, activeLeafView, to)}
        >
          {to} <strong>{field}</strong>
        </div>
      {/each}
    </span>
  </div>
</div>

<style>
  .BC-nexts div {
    text-align: right;
  }

  .BC-nexts {
    border-left: 1px solid var(--background-modifier-border);
  }
  .BC-prevs {
    border-right: 1px solid var(--background-modifier-border);
  }

  .BC-NextPrev-Container {
    display: grid;
    grid-template-columns: 1fr 1fr;
  }
</style>
