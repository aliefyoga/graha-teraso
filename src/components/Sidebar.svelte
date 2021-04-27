<script>
  import { SlidersIcon, UserIcon, UsersIcon, BoxIcon, PackageIcon, ShoppingBagIcon } from 'svelte-feather-icons';
</script>

<nav id="sidebar" class="sidebar">
  <div class="sidebar-content js-simplebar">
    <a class="sidebar-brand" href="/">
      <span class="align-middle">Graha Teraso</span>
    </a>

    <ul class="sidebar-nav">
      <li class="sidebar-item">
        <a class="sidebar-link" href="/admin/dashboard">
          <SlidersIcon class="align-middle"/> <span class="align-middle">Dashboard</span>
        </a>
      </li>

      <li class="sidebar-item">
        <a class="sidebar-link" href="/admin/profile">
          <UserIcon class="align-middle"/> <span class="align-middle">Profile</span>
        </a>
      </li>

      <li class="sidebar-item">
        <a class="sidebar-link" href="/admin/item">
          <BoxIcon class="align-middle"/> <span class="align-middle">Item</span>
        </a>
      </li>

      <li class="sidebar-item">
        <a class="sidebar-link" href="/admin/category">
          <PackageIcon class="align-middle"/> <span class="align-middle">Category</span>
        </a>
      </li>

      <li class="sidebar-item">
        <a class="sidebar-link" href="/admin/transaction">
          <ShoppingBagIcon class="align-middle"/> <span class="align-middle">Transaction</span>
        </a>
      </li>

      <li class="sidebar-item">
        <a class="sidebar-link" href="/admin/customer">
          <UsersIcon class="align-middle"/> <span class="align-middle">Customer</span>
        </a>
      </li>

    </ul>

    <div class="sidebar-cta">
      <div class="sidebar-cta-content">
        <div class="d-grid">
          <a class="sidebar-link text-center" href="/admin/logout">
            <span class="align-middle">Logout</span>
          </a>
        </div>
      </div>
    </div>
  </div>
</nav>

<style>
  .sidebar-cta .sidebar-link {
    background: #2b3947;
    border-radius: 0.3rem;
  }
  .sidebar-cta .sidebar-cta-content {
    background: transparent;
    margin: 1rem 1.625rem;
    padding: 0;
  }
</style>