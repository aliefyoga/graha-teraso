<script>
  import { Datatable, rows } from "svelte-simple-datatables";
  import { EditIcon, Trash2Icon } from "svelte-feather-icons";
  import { createEventDispatcher } from "svelte";
  let dispatch = createEventDispatcher();

  let id;
  export let items = [];

  const settings = {
    sortable: true,
    pagination: true,
    rowPerPage: 10,
    columnFilter: false,
  };

  const handleUpdate = async (id) => {
    let item = items.find((item) => item.id == id);
    let data = {
      item: item,
      status: "update",
    };

    dispatch("update", data);
  };

  const handleRemove = async () => {
    dispatch("remove", id);

    const res = await fetch(`http://127.0.0.1:8000/api/items/${id}`, {
      method: "delete",
      headers: {
        "Content-Type": "application/json",
      },
    });
  };

  const formatDate = (v) => {
    let date = new Date(v).toLocaleString("id-ID", {
      dateStyle: "medium",
    });
    let result = date;

    return result;
  };
</script>

<Datatable {settings} data={items}>
  <thead>
    <th data-key="name">Name</th>
    <th data-key="description">Description</th>
    <th data-key="price">Price</th>
    <th data-key="stock">Stock</th>
    <th data-key="created_at">Created at</th>
    <th data-key="updated_at">Updated at</th>
    <th>Action</th>
  </thead>
  <tbody>
    {#each $rows as row}
      <tr>
        <td>{row.title}</td>
        <td>{row.description}</td>
        <td>{row.price}</td>
        <td>{row.stock}</td>
        <td>{formatDate(row.created_at)}</td>
        <td>{formatDate(row.updated_at)}</td>
        <td>
          <div class="d-flex justify-content-center">
            <a
              class="me-3"
              on:click={() => {
                handleUpdate(row.id);
              }}><EditIcon class="align-middle text-success" /></a
            >
            <a
              data-bs-toggle="modal"
              data-bs-target="#deleteModal"
              on:click={() => {
                id = row.id;
              }}><Trash2Icon class="align-middle text-danger" /></a
            >
          </div>
        </td>
      </tr>
    {/each}
  </tbody>
</Datatable>

<div
  class="modal fade"
  id="deleteModal"
  tabindex="-1"
  aria-labelledby="exampleModalLabel"
  aria-hidden="true"
>
  <div class="modal-dialog modal-dialog-centered modal-sm">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
        <button
          type="button"
          class="btn-close"
          data-bs-dismiss="modal"
          aria-label="Close"
        />
      </div>
      <div class="modal-body">are u sure delete this item?</div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal"
          >no</button
        >
        <button
          type="button"
          class="btn btn-danger"
          on:click={handleRemove}
          data-bs-dismiss="modal">yes</button
        >
      </div>
    </div>
  </div>
</div>
