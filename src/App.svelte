<script lang="ts">

	export let title: string;
	
	let counters: {
    count: number;
    name: string;
	}[] = [
		{ count: 0, name: 'new' }
	];

	$: sum = counters.reduce((sum, i) => sum + i.count, 0);

	const newCounter = () => {
		let counter = { count: 0, name: 'new' };
		counters.push(counter);
		counters = counters;
	}

	const deleteCounter = (index: number) => {
		counters.splice(index, 1);
		counters = counters;
	}

	const incrementCount = (index: number) => {
		counters[index].count += 1
	}

	const decrementCount = (index: number) => {
    counters[index].count === 0 ? counters[index].count = 0 : counters[index].count -= 1;
  }

  const resetCount = (index: number) => {
    counters[index].count = 0
  }

</script>

<main>
	<h1>{title}</h1>
	<div class="counter-wrap">
		{#each counters as counter, index}
			<div class="counter-item">
				<input type="text" class="input" bind:value="{counter.name}">
				<div class="num">{counter.count}</div>
				<div class="buttons-wrap">
					<button class="plus" on:click={() => incrementCount(index)}>+</button>
					<button class="minus" on:click={() => decrementCount(index)}>-</button>
					<button class="reset" on:click={() => resetCount(index)}>0</button>
				</div>
				<div class="counter-reset" on:click={() => deleteCounter(index)}></div>
			</div>
		{/each}
	</div>
	<button class="newButton" on:click={newCounter}>New Counter!!</button>
	<div class="title-list mt10">
		Title List：
		{#each counters as counter, index}
			{#if index === 0}
				{counter.name}
			{:else}
				,&nbsp;{counter.name}
			{/if}
		{/each}
	</div>
	<div class="sum mt10">Sum Of Count：{sum}</div>
</main>

<style lang="scss">
	main {
		text-align: center;
		padding: 1em;
		margin: 0 auto;
	}

	h1 {
		color: #333;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	.newButton {
		background-color: #3e8ed0;
		border: none;
		color: #fff;
		cursor: pointer;
		margin: 0 auto;
		max-width: 366px;
		width: 100%;

		&:active {
			background-color: #3e8ed0;
		}
	}

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

		.counter-reset {
			height: 1.5rem;
			margin-left: .5rem;
			position: relative;
			width: 1.5rem;
			cursor: pointer;
			&:hover {
				background-color: rgba(60,64,67,0.08);
				border-radius: 50%;
			}

			&::before, &::after {
				content: '';
				position: absolute;
				top: 50%;
				left: 50%;
				background: #a0aec0;
				width: 2px;
				height: 1rem;
			}

			&::before {
				transform: translate(-50%, -50%) rotate(-45deg);
			}

			&::after {
				transform: translate(-50%, -50%) rotate(45deg);;
			}
		}
	}
</style>