<script lang="ts">
  export let count: number;
  export let name: string;

  const incrementCount = () => {
		count += 1;
	}

  const decrementCount = () => {
    (count === 0) ? count = 0 : count -= 1;
  }

  const resetCount = () => {
    count = 0
  }
</script>

<div class="counter-item">
  <input type="text" class="input" bind:value="{name}">
  <div class="num">{count}</div>
  <div class="buttons-wrap">
    <button class="plus" on:click={incrementCount}>+</button>
    <button class="minus" on:click={decrementCount}>-</button>
    <button class="reset" on:click={resetCount}>0</button>
  </div>
  <div class="counter-reset"></div>
</div>

<style lang="scss">
	.counter-item {
		align-items: center;
    background: #f7fafc;
		border-radius: .25rem;
		box-shadow: 0 10px 15px -3px rgb(0 0 0 / 10%), 0 4px 6px -2px rgb(0 0 0 / 5%);
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
		padding: 1rem .5rem;
    margin: 0 auto 1rem;
    max-width: 350px;

    .num {
      padding: .5rem 1rem;
    }

    .buttons-wrap {
      button {
        border: none;
        color: #fff;
        cursor: pointer;
      }

      .plus {
        background: #f14668;
      }

      .minus {
        background: #00d1b2;
      }

      .reset {
        background: #ffe08a;
      }
    }
	}
</style>