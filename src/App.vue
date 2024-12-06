<template>
  <div>
    <img alt="Vue logo" src="./assets/images/logo.png" />
    <h1>{{ title }}</h1>

    <!-- ref is use as selector like queryselector -->
    <input type="text" ref="name" />
    <button @click="handleClick">Click Me</button>

    <button @click="toggleModal('props')">Open Modal Using Props</button>
    <button @click="toggleModal('slot')">Open Modal Using Slot</button>
    <button @click="toggleModal('slot2')">
      Open Modal Using Slot Reusable
    </button>
    <button @click="toggleModal('teleport')">Open Modal Using Teleport</button>

    <!-- TELEPORT -->
    <teleport to=".teleportModal" v-if="showModalTeleport">
      <ModalSlots theme="sale" @close="toggleModal('teleport')">
        <div>
          <h1>I am Using Teleport</h1>
          <h1>{{ header }}</h1>
          <p>{{ text }}</p>
        </div>
        <template v-slot:links>
          <div>
            <a href="#">Sign Up</a>
            <a href="#">View More</a>
          </div>
        </template>
      </ModalSlots>
    </teleport>

    <!-- SLOTS V2 -->
    <div v-if="showModalSlot">
      <ModalSlots theme="sale" @close="toggleModal('slot')">
        <div>
          <h1>I am Using Slots</h1>
          <h1>{{ header }}</h1>
          <p>{{ text }}</p>
        </div>
        <template v-slot:links>
          <div>
            <a href="#">Sign Up</a>
            <a href="#">View More</a>
          </div>
        </template>
      </ModalSlots>
    </div>

    <!-- SLOTS -->
    <div v-if="showModalSlotTwo">
      <ModalSlots theme="sale" @close="toggleModal('slot2')">
        <div>
          <h1>I am Using Slots Part Two</h1>
          <h1>Signup for newsletter!</h1>
          <p>For the latest coupon and codes</p>
        </div>
        <template v-slot:links>
          <div>
            <a href="#">Sign Up</a>
            <a href="#">View More</a>
          </div>
        </template>
      </ModalSlots>
    </div>

    <!-- PROPS -->
    <div v-if="showModalProps">
      <ModalProps
        :header="header"
        :text="text"
        theme="sale"
        @close="toggleModal('props')"
      />
    </div>
  </div>
</template>

<script>
import ModalProps from "./components/ModalProps.vue";
import ModalSlots from "./components/ModalSlots.vue";

export default {
  name: "App",
  components: {
    ModalProps,
    ModalSlots,
  },
  data() {
    return {
      title: "Hello, Vue!",
      header: "Sign up for the Giveaway!",
      text: "Grab your ninja swag for half price!",
      showModalProps: false,
      showModalSlot: false,
      showModalSlotTwo: false,
      showModalTeleport: false,
    };
  },
  methods: {
    // Ref is used like for js dom like queryselector
    handleClick() {
      console.log(this.$refs.name);
      this.$refs.name.classList.add("active");
      this.$refs.name.focus();
    },
    toggleModal(type) {
      if (type === "slot") {
        this.showModalSlot = !this.showModalSlot;
      } else if (type === "props") {
        this.showModalProps = !this.showModalProps;
      } else if (type === "slot2") {
        this.showModalSlotTwo = !this.showModalSlotTwo;
      } else if (type === "teleport") {
        this.showModalTeleport = !this.showModalTeleport;
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
