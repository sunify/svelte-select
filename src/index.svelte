<style>
  .root {
    position: relative;
  }

  .root select {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    opacity: 0;
  }
</style>

<script>
  export let options, value, emptyValue = '', placeholder = '';

  let currentOption;
  $: {
    currentOption = options.find(o => o[0] === value);
    if (!currentOption) {
      currentOption = [emptyValue, placeholder];
      if (value !== emptyValue) {
        value = options[0][0];
      }
    }
  }
</script>

<span class="root">
  <select bind:value={value}>
    {#if placeholder}
      <option value={emptyValue}>
        <slot name="option" option={placeholder}>
          {placeholder}
        </slot>
      </option>
    {/if}
    {#each options as [value, option]}
      <option {value}>
        <slot name="option" {option}>
          {option}
        </slot>
      </option>
    {/each}
  </select>
  <slot currentOption={currentOption[1]}>
    {currentOption[1]}
  </slot>
</span>