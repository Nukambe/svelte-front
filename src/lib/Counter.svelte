<script>
  export let initialCount;
  export let maxCount = -1;

  let count = initialCount;
  let countee = initialCount;
  function increment() {
    count += maxCount;
    countee += maxCount;
  }
  function reset() {
    count = 0;
  }
  function total() {
    return count + countee;
  }

  let string;
  $: if (count > 0) {
    string = `You have clicked ${total()} times`;
  } else {
    string = `womp womp...`;
  }
</script>

<button on:click={increment}>Clicks {count}</button>
<button on:click={reset}>Reset</button>
<h2>{string}</h2>
<h3>countee {countee}</h3>
