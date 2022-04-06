<template>
  <nav class="navbar">
    <div class="navbar-container">
      <!-- Hamburger menu -->
      <button id="menu-btn" class="hamburger" type="button">
        <span class="hamburger-top"></span>
        <span class="hamburger-middle"></span>
        <span class="hamburger-bottom"></span>
      </button>

      <div class="navbar-brand">
        <a href="#">
          <span class="title">torre</span><span class="co">.co</span>
        </a>
      </div>

      <ul class="navbar-nav-right">
        <li class="search-icon">
          <img
            src="../static/search-white.svg"
            alt="search"
            @click="$emit('showInput')"
          />
        </li>
        <li class="sign-in">
          <a href="#">
            <span>SIGN IN</span>
          </a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {}
</script>

<style scoped>
.navbar {
  width: 100%;
  height: auto;
  background-color: #27292d;
  padding: 20px;
  /* box-shadow: 0 1px 3px rgb(0 0 0 / 10%), 0 2px 2px rgb(0 0 0 / 6%),
    0 0 2px rgb(0 0 0 / 7%); */
  -webkit-box-shadow: 0px 5px 8px 0px #000000;
  box-shadow: 0px 5px 8px 0px #000000;
}

.navbar-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1440px;
  margin: 0 auto;
}

.navbar-container li a {
  text-decoration: none;
}

.navbar ul {
  display: flex;
  align-items: center;
}

.navbar ul li {
  /* margin: 0 15px; */
  font-weight: bold;
  display: flex;
  justify-content: center;
  align-items: center;
}

.navbar-container li a:hover {
  color: var(--color-primary);
}

.navbar-nav-left {
  text-transform: uppercase;
  /* Push to the side */
  flex: 1;
  margin-left: 20px;
}

.navbar-nav-right li:first-child a {
  display: flex;
  align-items: center;
}

.navbar-nav-right li:nth-child(2) {
  margin-right: 0 5px;
}

.navbar-nav-right li:nth-child(3) button {
  font-weight: bold;
}

.navbar-brand {
  flex: 1;
  margin-left: 1.5rem;
  font-size: 23px;
}

.navbar-brand img {
  width: 50px;
  height: 50px;
}

.navbar-nav-right img {
  height: 20px;
  width: 20px;
  margin-right: 10px;
}

/* .search-icon img {
  width: 50px;
} */

.title {
  font-weight: bold;
}

.co {
  color: #cddc39;
}

.sign-in a span {
  color: #cddc39;
  font-weight: normal;
}

.hamburger {
  cursor: pointer;
  width: 24px;
  height: 20px;
  position: relative;
  background: none;
  border: none;
  z-index: 10;
  transition: all 0.25s;
  display: none;
  margin-top: 5px;
}

.hamburger-top,
.hamburger-middle,
.hamburger-bottom {
  position: absolute;
  top: 0;
  left: 0;
  width: 24px;
  height: 2px;
  background: white;
  transform: rotate(0);
  transition: all 0.5s;
}

.hamburger-middle {
  transform: translateY(7px);
}

.hamburger-bottom {
  transform: translateY(14px);
}

.open .hamburger-top {
  transform: rotate(45deg) translateY(6px) translateX(6px);
}
.open .hamburger-middle {
  display: none;
}
.open .hamburger-bottom {
  transform: rotate(-45deg) translateY(6px) translateX(-6px);
}

@media (max-width: 768px) {
  .hamburger {
    display: block;
  }
}
</style>