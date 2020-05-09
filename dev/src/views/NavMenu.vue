<template>
  <div class="nav-menu">
    <div class="dev-flex-c-b">
      <div class="nav-logo dev-flex-c">
        <!-- <img :src="logoImg" class="nav-logo-img" /> -->
        <span class="nav-logo-text">{{ logoText }}</span>
      </div>
      <div class="nav-content dev-flex-c">
        <div class="nav-content-item">
          <a
            href="https://github.com/one-data-model/prototype-registry/blob/verification/README.md"
            target="_blank"
            rel="noopener noreferrer"
            class="p-right-1"
          >README</a>
          <a
            href="https://github.com/one-data-model/prototype-registry"
            target="_blank"
            rel="noopener noreferrer"
            class="p-right-1"
          >GITHUB</a>
          <a
            href="https://one-data-model.github.io/prototype-registry/"
            target="_blank"
            rel="noopener noreferrer"
          >CONTACT</a>
        </div>
      </div>
    </div>
    <div>
      <p>
        To submit new models please follow the instructions provided in the
        <a
          href="https://github.com/one-data-model/prototype-registry/blob/verification/README.md"
          class="p-link"
        >README</a> file.
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "NavMenu",
  data() {
    return {
      logoText: "ONE DATA MODEL REGISTRY"
    };
  }
};
</script>

<style lang="scss" scoped>
.nav-menu {
  margin: 1em 0.5em;
  box-sizing: border-box;
  padding: 20px;
  color: #ffffff;
  transition: all 0.4s ease;
  user-select: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  -webkit-user-drag: none;
  background-color: rgba(125, 125, 125, 0.5);
}

.nav-logo-img {
  width: 24px;
  height: 24px;
}
.nav-logo-text {
  margin-left: 0.4em;
  font-size: 1.5em;
  color: #ffffff;
  font-weight: 600;
  padding-bottom: 0.7em;
}

.nav-menu p {
  padding: 0 0 0 0.7em;
  margin-bottom: 5em;
  font-weight: normal;
  font-size: 0.8em;
}

.p-link,
.nav-content-item a,
.nav-content-item a:visited,
.nav-content-item a:focus {
  color: rgb(248, 99, 121);
  font-size: 1em;
  font-weight: bold;
  text-decoration: none;
}

.p-right-1 {
  padding-right: 1em;
}

.nav-content-item {
  margin: 0 12px;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  color: rgb(248, 99, 121);
  cursor: pointer;
}
.nav-content-item:hover,
.nav-menu a:hover {
  color: #ffffff;
}
</style>