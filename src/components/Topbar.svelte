<script>
  import { UserIcon, LogOutIcon } from 'svelte-feather-icons'; 
</script>

<nav class="navbar navbar-expand navbar-light navbar-bg">
  <a class="sidebar-toggle d-flex">
    <i class="hamburger align-self-center"></i>
  </a>

  <div class="navbar-collapse collapse">
    <ul class="navbar-nav navbar-align">
      <li class="nav-item dropdown">
        <a class="nav-link dropdown-toggle d-none d-sm-inline-block" href="#" data-bs-toggle="dropdown">
          <img src="img/avatars/avatar.jpg" class="avatar img-fluid rounded me-1" alt="Charles Hall" /> <span class="text-dark">Admin</span>
        </a>
        <div class="dropdown-menu dropdown-menu-end mt-3">
          <a class="dropdown-item" href="/admin/profile"><UserIcon class="align-middle me-1"/> Profile</a>
          <a class="dropdown-item" href="/admin/logout"><LogOutIcon class="align-middle me-1"/> Log out</a>
        </div>
      </li>
    </ul>
  </div>
</nav>