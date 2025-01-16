<template>
  <div>
    <nav
      class="navbar navbar-expand-lg navbar-light bg-light fixed-top p-st"
      :class="{
        'bg-light': !nightMode,
        'navbar-blur': navbarConfig.blur,
        'bg-dark2': nightMode,
      }"
    >
      <div class="container">
        <a
          class="navbar-brand"
          href="/"
          @click.prevent="scrollTo('home')"
        >
          <Logo :nightMode="nightMode" />
        </a>
        <button
          class="navbar-toggler"
          type="button"
          data-toggle="collapse"
          data-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span style="color: gray; font-size: 23px;">
            <i class="fas fa-bars"></i>
          </span>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="nav nav-pills nav-fill gap-2 p-1 small bg-primary rounded-5 shadow-sm" id="pillNav2" role="tablist">
            <li class="nav-item" role="presentation">
              <button class="nav-link active rounded-5" id="home-tab2" data-bs-toggle="tab" type="button" role="tab" aria-selected="true">About</button>
              <a
                class="nav-link"
                href="/about"
                @click.prevent="scrollTo('about')"
                :class="{ 'text-light': nightMode }"
              >About</a>
            </li>
            <li class="nav-item mx-2">
              <a
                class="nav-link"
                href="/skills"
                @click.prevent="scrollTo('skills')"
                :class="{ 'text-light': nightMode }"
              >Skills</a>
            </li>
            <li class="nav-item mx-2">
              <a
                class="nav-link"
                href="/portfolio"
                @click.prevent="scrollTo('portfolio')"
                :class="{ 'text-light': nightMode }"
                v-tooltip.bottom="nightMode ? 'Portfolio' : 'Portfolio'"
              >Portfolio</a>
            </li>
            <li class="nav-item ml-2">
              <a
                class="nav-link"
                href="#"
                @click.prevent="switchMode"
                :class="{ 'text-light': nightMode }"
              ><i
                :class="{
                  'fas fa-moon': nightMode,
                  'far fa-moon': !nightMode,
                }"
                v-tooltip.bottom="nightMode ? 'Light Mode' : 'Night Mode'"
              ></i></a>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </div>
</template>