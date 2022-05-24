<script lang="ts">
  import MdSync from "svelte-icons/md/MdSync.svelte";
  import MdLink from "svelte-icons/md/MdLink.svelte";

  export let src: string;

  function onClickReload() {
    const buf = src;
    src = "";
    setTimeout(() => (src = buf), 100);
  }
</script>

<div class="wrapper">
  <iframe {src} title={src} frameborder="0" />
  <div class="controls">
    <button class="controls-item btn-icon" on:click={onClickReload}>
      <div class="controls-item-icon">
        <MdSync />
      </div>
    </button>
    <a class="controls__item a-icon" href={src} target="_blank">
      <div class="controls-item-icon">
        <MdLink />
      </div>
    </a>
  </div>
</div>

<style>
  .wrapper {
    position: relative;
    width: 100%;
    border-radius: 5px;
    overflow: hidden;
    box-shadow: 0 0 0 1px rgb(0 0 0 / 5%), 0 0 10px rgb(0 0 0 / 10%);
  }
  .wrapper::before {
    content: "";
    display: block;
    padding-top: 100%;
    z-index: -1;
    user-select: none;
  }
  .wrapper:hover > .controls {
    opacity: 1;
  }
  iframe {
    position: absolute;
    top: 0;
    left: 0;
    box-sizing: border-box;
    display: block;
    /* border: 1px solid red; */
    border-radius: 5px;
    overflow: auto;
    width: 100%;
    height: 100%;
  }
  .controls {
    display: flex;
    align-items: center;
    position: absolute;
    opacity: 0;
    bottom: 10px;
    right: 10px;
    /* background-color: white;
    box-shadow: 0 0 10px rgb(0 0 0 / 10%), 0 0 0 1px rgb(0 0 0 / 10%); */
    /* padding: 5px; */
    border-radius: 4px;
    font-family: monospace;
    text-decoration: none;
    transition-duration: 0.2s;
  }

  .controls-item {
    display: block;
  }

  .controls-item:not(:last-child) {
    margin-right: 5px;
  }

  .controls-item-icon {
    height: 20px;
  }

  .btn-icon,
  .a-icon {
    border: none;
    outline: none;
    padding: 5px;
    color: black;
    background-color: rgb(240 240 240);
    border-radius: 50px;
    cursor: pointer;
  }
</style>
