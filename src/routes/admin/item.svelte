<script context="module">
  export async function preload() {
    const res = await this.fetch("http://47.74.69.251/api/items", {
      headers: {
        Authorization:
          "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC80Ny43NC42OS4yNTFcL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2MTkwODAyNTcsImV4cCI6MTYxOTA4Mzg1NywibmJmIjoxNjE5MDgwMjU3LCJqdGkiOiJRTHRFNjcyTzBOR0FHSlpKIiwic3ViIjoxLCJwcnYiOiIyM2JkNWM4OTQ5ZjYwMGFkYjM5ZTcwMWM0MDA4NzJkYjdhNTk3NmY3In0.6SKpopSwEvImJ7GuPCTVYye37Rl3vqN5fcnoKM7UD0Y",
        "x-api-key":
          "$2y$10$hc0ovxu4eXjo0M/YL3hpU.riEH19GKKbZYh58Cf0.WkA26960vXFy",
      },
    });
    const data = await res.json();

    if (res.status === 200) {
      return {
        message: data.message,
        items: data.data,
      };
    } else {
      this.error(res.status, data.message);
    }
  }
</script>

<script>
  import ItemTable from "../../components/tables/item.svelte";
  import ItemForm from "../../components/forms/item.svelte";

  export let items = [];
  let data;
  let status;

  const handleAdd = (e) => {
    let item = e.detail;
    items = [...items, item];
  };

  const handleRemove = (e) => {
    items = items.filter((item) => item.id != e.detail);
  };

  const handleUpdate = (e) => {
    data = e.detail.item;
    status = e.detail.status;
  };

  const handleUpdated = (e) => {
    let currentItem = items.filter((item) => item.id == e.detail.id);

    items = items.map((item) => {
      if (JSON.stringify(item) === JSON.stringify(currentItem[0])) {
        return e.detail;
      } else {
        return item;
      }
    });

    status = "store";
  };

  const handleReset = () => {
    status = "store";
  };
</script>

<svelte:head>
  <title>Item</title>
</svelte:head>

<div class="container">
  <div class="row">
    <div class="col-md-8 col-sm-12">
      <div class="card shadow mb-4">
        <div class="card-body">
          <ItemTable
            on:remove={handleRemove}
            on:update={handleUpdate}
            {items}
          />
        </div>
      </div>
    </div>
    <div class="col-md-4 col-sm-12">
      <div class="card shadow mb-4">
        <div class="card-body">
          <ItemForm
            on:add={handleAdd}
            on:updated={handleUpdated}
            on:reset={handleReset}
            {status}
            {data}
          />
        </div>
      </div>
    </div>
  </div>
</div>

<style>
  .card {
    min-height: 70vh;
  }
</style>
