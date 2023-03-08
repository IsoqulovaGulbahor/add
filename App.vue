<template>
  <div>
    <nav>
      <div class="logo">
        <!-- <img src="./nextCode24.png" alt="nextCode24 logo" /> -->
        <h1>nextCode24</h1>
      </div>
      <ul class="nav-list">
        <li class="nav-item"><router-link to="/">Home</router-link></li>
        <li class="nav-item"><router-link to="/about">About</router-link></li>
        <li class="nav-item">
          <router-link to="/contact">Contact</router-link>
        </li>
      </ul>
      <div class="style-selector">
        <label for="style-select" class="style-selector-label"
          >Select Style:</label
        >
        <select
          id="style-select"
          v-model="selectedStyle"
          @change="changeStyle"
          class="style-selector-select">
          <option value="default">Default</option>
          <option value="dark">Dark</option>
          <option value="light">Light</option>
        </select>
      </div>
    </nav>
    <router-view></router-view>
  </div>
  <div class="d-flex">
    <div class="card container" :style="{ backgroundColor: selectedColor }">
      <img :src="imageUrl" :style="{ filter: `hue-rotate(${hueRotate}deg)` }" />
      <div class="color-picker">
        <!-- label1 -->
        <label for="color1">
          <input
            type="radio"
            name="color"
            id="color1"
            value="#ff0000"
            @change="selectColor" />
          <span class="color-swatch" style="background-color: #ff0000"></span>
        </label>

        <label for="color2">
          <input
            type="radio"
            name="color"
            id="color2"
            value="green"
            @change="selectColor" />
          <span class="color-swatch" style="background-color: green"></span>
        </label>
        <label for="color3">
          <input
            type="radio"
            name="color"
            id="color3"
            value="#0000ff"
            @change="selectColor" />
          <span class="color-swatch" style="background-color: #0000ff"></span>
        </label>
      </div>
      <div class="counter">
        <button @click="decrement">-</button>
        <span>{{ count }}</span>
        <button @click="increment">+</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  name: "Card",
  data() {
    return {
      selectedStyle: "default",
      count: 0,
      selectedColor: "#fff",
      imageUrl: "https://placekitten.com/300/200",
      hueRotate: 0,
    };
  },
  methods: {
    changeStyle() {
      const body = document.body;
      switch (this.selectedStyle) {
        case "default":
          body.classList.remove("dark");
          body.classList.remove("light");
          break;
        case "dark":
          body.classList.add("dark");
          body.classList.remove("light");
          break;
        case "light":
          body.classList.add("light");
          body.classList.remove("dark");
          break;
        default:
          body.classList.remove("dark");
          body.classList.remove("light");
          break;
      }
    },
    increment() {
      this.count++;
    },
    decrement() {
      if (this.count > 0) {
        this.count--;
      }
    },
    selectColor(event) {
      this.selectedColor = event.target.value;
      this.hueRotate = Math.floor(Math.random() * 360);
    },
  },
};
</script>

<style>
nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  background-color: #222;
  color: white;
}

.logo {
  display: flex;
  align-items: center;
}

.logo img {
  height: 50px;
  margin-right: 10px;
}

.logo h1 {
  margin: 0;
  font-size: 28px;
  font-weight: bold;
  letter-spacing: 1px;
}

.nav-list {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-item {
  margin-right: 20px;
}

.nav-item:last-child {
  margin-right: 0;
}

.nav-item a {
  color: white;
  text-decoration: none;
  font-size: 18px;
  font-weight: bold;
}

.nav-item a:hover {
  color: #ccc;
}

.style-selector {
  display: flex;
  align-items: center;
}

label {
  margin-right: 10px;
}

/* media query for screens with a maximum width of 1240px */
@media (max-width: 1240px) {
  nav {
    width: 100%;
    padding: 10px 20px;
  }
}

.dark {
  background-color: #222;
  color: white;
}

.light {
  background-color: white;
  color: black;
}
.d-flex {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 300px;
  height: 400px;
  padding: 20px;
  box-shadow: 10px 0px 10px 0px rgba(12, 0, 10, 0.2);
  border: solid #333;
  border-radius: 10px;
  margin-top: 50px;
}

.card img {
  width: 200px;
  height: 200px;
  object-fit: cover;
  border-radius: 50%;
  margin-bottom: 20px;
}

.color-picker {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.color-swatch {
  display: inline-block;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  margin-right: 10px;
  cursor: pointer;
}

.counter {
  display: flex;
  align-items: center;
}

.counter button {
  font-size: 24px;
  font-weight: bold;
  border: none;
  background-color: #fff;
  color: #333;
  width: 30px;
  height: 30px;
  margin: 10px;
}
</style>
