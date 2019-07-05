<template>
  <div id="app">
    <nav>
      <h1>Navbar</h1>
      <div>
        <ul>
          <li>
            <router-link :to="{ name: 'posts' }">Posts</router-link>
          </li>
        </ul>
      </div>
    </nav>
    <router-view />
  </div>
</template>

<script>

export default {
  name: 'app',
}
</script>