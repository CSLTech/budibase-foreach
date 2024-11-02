<script lang='ts'>
  import { getContext } from "svelte";

  export let dataProvider;
  export let nextLineNumber: string;
  export let event;

  let currentLineNumber = 0;
  let currentLineData = {};

  $: dataContext = {
    currentLineNumber,
    currentLineData
  };

  const { styleable, Provider } = getContext("sdk");
  const component = getContext("component");

  $: nextLineChanged(nextLineNumber);

  function nextLineChanged(nextLineNumber: string) {
    currentLineNumber = parseInt(nextLineNumber, 10);

    if (isNaN(currentLineNumber) || currentLineNumber < 0 || currentLineNumber >= dataProvider?.rows.length) {
      currentLineNumber = null;
      currentLineData = null;
    }
    else {
      currentLineData = dataProvider?.rows[currentLineNumber];
    }

    dataContext = {
      currentLineNumber,
      currentLineData
    };

    if (event && currentLineNumber !== null) {
      event({lineData: currentLineData, lineNumber: currentLineNumber});
    }
  }
</script>

<div use:styleable={$component.styles}>
  <Provider data={dataContext}>
    {#if currentLineNumber !== null}
      Currently processing line {currentLineNumber}.
    {:else}
      Not currently processing
    {/if}
  </Provider>
</div>
