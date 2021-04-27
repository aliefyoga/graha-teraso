<script>
  export let name;
  export let label;
  export let type;
  export let value;
  export let rows = 3;
  export let valid = 'undefined';
  export let invalid = 'undefined';

  const handleInput = e => {
    value = e.target.value;
  };
</script>

<div class="mb-3">
  <label for={name} class="form-label">{label}</label>
  {#if type === "textarea"}
    <textarea class="form-control" id={name} {rows} on:input={handleInput} {value} autocomplete="off" required></textarea>
  {:else}
    <input {type} class="form-control" id={name} on:input={handleInput} {value} autocomplete="off" required>
  {/if}
  {#if valid !== 'undefined'}
    <div class="valid-feedback">
      {valid}
    </div>
  {/if}
  {#if invalid !== 'undefined'}
    <div class="invalid-feedback">
      {invalid}
    </div>
  {/if}
</div>
