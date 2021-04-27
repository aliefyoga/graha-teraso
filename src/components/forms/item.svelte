<script>
  import Field from '../partials/Field.svelte';
  import { onMount, createEventDispatcher } from "svelte";
  let dispatch = createEventDispatcher();
  
  export let status = 'store';
  export let data = {
    'name'        : '',
    'description' : '',
    'price'       : '',
    'stock'       : ''
  };

  let submit;

  const storeItem = async () => {
    let method = status === 'store' ? 'post' : 'put';
    let url = status === 'store' ? 'http://127.0.0.1:8000/api/items' : `http://127.0.0.1:8000/api/items/${data.id}`;

    const res = await fetch(url, {
      method: method,
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(data)
    });
    const json = await res.json();
    data = json.data;

    if (status === 'store') {
      dispatch('add', data);
    } else {
      dispatch('updated', data);
    }

    resetForm();
  }

  const resetForm = () => {
    data = {
      'name'        : '',
      'description' : '',
      'price'       : '',
      'stock'       : ''
    }

    dispatch('reset');
  }

  onMount(async () => {
    submit = () => {
      var forms = document.querySelectorAll('.needs-validation')

      Array.prototype.slice.call(forms)
        .forEach(function (form) {
          if (!form.checkValidity()) {
            event.preventDefault()
            event.stopPropagation()
            form.classList.add('was-validated')
          } else {
            storeItem()
            form.classList.remove('was-validated')
          }
        })
    }
  });

</script>

<form class="needs-validation" on:submit|preventDefault={submit} novalidate>
  <Field
    name="name"
    label="Name"
    type="text"
    bind:value={data.name} />
  <Field
    name="desc"
    label="Description"
    type="textarea"
    rows=3
    bind:value={data.description} />
  <Field
    name="price"
    label="Price"
    type="number"
    bind:value={data.price} />
  <Field
    name="stock"
    label="Stock"
    type="number"
    bind:value={data.stock} />
  <div class="mt-4 d-flex justify-content-between">
    <button
      type="submit"
      class="btn btn-primary">
      {#if status === 'store'}
        Add Item
      {:else}
        Update Item
      {/if}
    </button>
    <a class="btn btn-danger" on:click={resetForm}>Reset</a>
  </div>
</form>