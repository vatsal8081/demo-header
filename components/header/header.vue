<template>
  <div>
    <header>
      <nav class="navbar navbar-expand-lg navbar-light dark_ligh_bg">
        <div class="container">
          <!-- <button
            class="navbar-toggler"
            type="button"
            data-toggle="collapse"
            data-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent"
            aria-expanded="false"
            aria-label="Toggle navigation"
          >
            <span class="navbar-toggler-icon"></span>
          </button> -->

          <appMenu></appMenu>

          <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav ml-auto">
              <li class="nav-item active">
                <a
                class="nav-link"
                href="#"
                  ><fa icon="phone-alt"></fa> +31(0)123456789</a
                >
              </li>
              <li class="nav-item active">
                <a
                class="nav-link"
                href="#"
                  ><fa icon="user"></fa> John</a
                >
              </li>
              <li class="nav-item active">
                <a
                class="nav-link"
                href="#"
                  ><fa icon="shopping-bag"></fa> {{ $t('cart') }}</a
                >
              </li>
            </ul>
          </div>
          <div class="mobile-menu d-lg-none">
            <ul class="d-flex">
              <li>
                <a href="#"><fa icon="search"></fa></a>
              </li>
              <li>
                <a href="#"><fa icon="user"></fa></a>
              </li>
              <li>
                <a href="#"><fa icon="shopping-bag"></fa></a>
              </li>
            </ul>
          </div>
        </div>
      </nav>
    </header>
  </div>
</template>

<script>
import appMenu from '@/components/menu/menu.vue'

export default {
  components: { appMenu }
}
</script>

<style scoped >
@import url("./style.css");
</style>
