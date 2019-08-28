<script>
  import Dropdown from '../src/index.svelte';

  const emptyValue = '';

  let value1 = emptyValue;
  let options1 = [
    ['0xa1', {name: 'Alice'}],
    ['0xb1', {name: 'Bob'}],
    ['0xc1', {name: 'Charlie'}],
  ];

  let value2 = emptyValue;
  let options2 = [
    ['0', 'Moscow'],
    ['1', 'New York'],
    ['2', 'London'],
  ];

  let value3 = emptyValue;
  let options3 = [
    ['0', 'Shimano'],
    ['1', 'Campangnolo'],
    ['2', 'Sram'],
  ];

  function handleReset() {
    value1 = emptyValue;
    value2 = emptyValue;
    value3 = emptyValue;
  }
</script>

<style>
  :global(body) {
    font-family: Helvetica, Arial, sans-serif;
    margin: 0;
    padding: 1rem;
  }

  h3 {
    margin-bottom: 0.5rem;
    margin-top: 2rem;
  }

  h3:first-of-type {
    margin-top: 0;
  }

  .button {
    display: inline-block;
    padding: 5px 10px;
    border: 1px solid #ccc;
    border-radius: 3px;
  }

  select:focus + .button {
    border-color: #00f;
  }

  hr {
    margin: 2rem 0;
  }
</style>

<h3>Object values</h3>
<Dropdown
  options={options1}
  {emptyValue}
  placeholder="Select address"
  bind:value={value1}
  let:currentOption
>
  <slot>
    <span class="button">
      {currentOption.name || currentOption}
    </span>
  </slot>
  <span slot="option" let:option>
    {option.name || option}
  </span>
</Dropdown>

<h3>String values</h3>
<Dropdown
  options={options2}
  {emptyValue}
  placeholder="Select city"
  bind:value={value2}
  let:currentOption
>
  <slot>
    <span class="button">
      {currentOption} ▾
    </span>
  </slot>
</Dropdown>

<h3>Default button</h3>
<Dropdown
  options={options3}
  {emptyValue}
  placeholder="Freehub body"
  bind:value={value3}
  let:currentOption
/>

<hr />

<button on:click={handleReset}>Reset</button>