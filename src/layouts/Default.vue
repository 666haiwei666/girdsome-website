<template>
  <div class="layout">
    <header class="header">
      <g-link to="/">
        <img src='/images/logo.svg' style="width: 66px;" />
      </g-link>
      <nav class="nav">
        <g-link class="nav__link" to="/journals"><span>Journal</span></g-link>
        <g-link class="nav__link" to="/contact"><span>Say Hi!</span></g-link>
      </nav>
    </header>
    <div class="content">
      <slot />
    </div>
    <footer>
      <div class="container">
        <span>Copyright © 2021</span>
      </div>
    </footer>
  </div>
</template>

<static-query>
  query {
  metadata {
  siteName
  }
  }
</static-query>

<style>
  .content {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  body {
    font-family: -apple-system, system-ui, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
    margin: 0;
    padding: 0;
    line-height: 1.5;
  }

  .layout {
    max-width: 1100px;
    margin: 0 auto;
    padding-left: 20px;
    padding-right: 20px;
  }

  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
    height: 80px;
  }

  .nav__link {
    margin-left: 20px;
    font-size: .9rem;
    font-weight: 600;
    text-decoration: none;
    margin-top: 4px;
    margin-right: 3rem;
    padding-bottom: 4px;
    transition: border .15s;
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 6rem 0;
  }
</style>