# svelte-select

Simple select that allows you to customize button appearance

```svelte
<script>
  import Select from '../src/index.svelte';

  const emptyValue = '';

  let value = emptyValue;
  let options = [
    ['0', { brand: 'Shimano', material: 'Steel' }],
    ['1', { brand: 'Campangnolo', material: 'Alluminium' }],
    ['2', { brand: 'Sram', material: 'Alluminium' }],
  ];
</script>

<style>
  .button {
    display: inline-block;
    padding: 5px 10px;
    border: 1px solid #ccc;
    border-radius: 3px;
  }

  select:focus + .button {
    border-color: #00f;
  }
</style>

<Select
  options={options}
  {emptyValue}
  placeholder="Freehub body"
  bind:value={value}
  let:currentOption
>
  <slot>
    <span class="button">
      {currentOption.brand || currentOption} ▾
    </span>
  </slot>
  <span slot="option" let:option>
    {#if typeof option === 'object'}
      {option.brand} ({option.material})
    {:else}
      {option}
    {/if}
  </span>
</Select>
```

## Install

`npm install @sunify/svelte-select` or `yarn add @sunify/svelte-select`

## Props

- `options: [string, any][]` — an array of key-value pairs
- `emptyValue: string = ''` — default value when no selected option
- `placeholder: string = ''`
- `value: string` — current option key

## Slots

- `default` — to customize select button appearance or add anything you want to select
- `option` — to customize select options (see example above)