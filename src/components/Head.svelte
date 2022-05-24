<script lang="ts">
  export let url = "";
  export let amount = 1;

  function onScroll(y: number) {
    hideHead = scrollY > prevScrollY && scrollY > 10 ? true : false;
    prevScrollY = scrollY;
  }

  let scrollY: number;
  let prevScrollY = 0;

  let hideHead = false;

  $: onScroll(scrollY);
</script>

<div class="head" class:head--hidden={hideHead}>
  <div class="controls container">
    <div class="controls-element controls-element-url">
      <input
        class="input input--url"
        type="text"
        bind:value={url}
        placeholder="url"
      />
    </div>
    <div class="controls-element">
      <input
        class="input input--amount"
        type="number"
        bind:value={amount}
        min="1"
        max="1000"
        placeholder="amount"
      />
    </div>
  </div>
</div>

<svelte:window bind:scrollY />

<style>
  .head {
    display: flex;
    position: fixed;
    box-sizing: border-box;
    align-items: center;
    top: 0;
    left: 0;
    width: 100%;
    height: 60px;
    background-color: rgb(255 255 255 / 80%);
    box-shadow: 0 0 10px rgb(0 0 0 /10%);
    transition: 0.2s;
    z-index: 1;
  }
  .head--hidden {
    transform: translateY(-100%);
    box-shadow: none;
  }
  .controls {
    display: flex;
    width: 100%;
    height: 35px;
  }
  .controls > *:not(:last-child) {
    margin-right: 15px;
  }
  .controls-element {
    display: flex;
  }
  .controls-element-url {
    width: 100%;
  }
  .input {
    border: none;
    padding: 5px 15px;
    background-color: rgb(240 240 240);
    border-radius: 5px;
    flex-grow: 0;
    box-sizing: border-box;
  }

  .input--url {
    width: 100%;
  }

  .input--amount {
    width: 100px;
  }
</style>
