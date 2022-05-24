<script lang="ts">
  import Head from "./Head.svelte";
  import Frame from "./Frame.svelte";

  import MdAdd from "svelte-icons/md/MdAdd.svelte";

  let url = localStorage.getItem("url") || "";
  let amount = 3;

  function genFxhash() {
    const alphabet =
      "123456789abcdefghijkmnopqrstuvwxyzABCDEFGHJKLMNPQRSTUVWXYZ";
    return (
      "oo" +
      Array(49)
        .fill(0)
        .map((_) => alphabet[(Math.random() * alphabet.length) | 0])
        .join("")
    );
  }

  $: localStorage.setItem("url", url);
</script>

<main>
  <Head bind:url bind:amount />
  <div class="container">
    {#if url}
      <ul class="preview-list">
        {#each [...Array(amount).keys()] as i (i)}
          <li class="preview-list-item">
            <Frame src={url + `?fxhash=${genFxhash()}`} />
          </li>
        {/each}
        <li class="preview-list-item">
          <button class="button-add" on:click={() => amount++}>
            <div class="button-add-inner">
              <div class="button-add-icon">
                <MdAdd />
              </div>
            </div>
          </button>
        </li>
      </ul>
    {/if}
  </div>
</main>

<style>
  main {
    margin-top: 80px;
  }
  .preview-list {
    display: grid;
    list-style-type: none;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    grid-gap: 20px;
    margin: 0;
    margin-bottom: 20px;
    padding: 0;
  }
  .button-add {
    display: block;
    position: relative;
    box-sizing: border-box;
    width: 100%;
    border: none;
    outline: none;
    margin: 0;
    padding: 0;
    border-radius: 5px;
    overflow: hidden;
  }
  .button-add::before {
    content: "";
    display: block;
    padding-top: 100%;
  }
  .button-add-inner {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 20px;
  }
  .button-add-icon {
    width: 60px;
    height: 60px;
    color: gray;
  }
</style>
