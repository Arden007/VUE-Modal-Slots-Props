<template>
  <p>Welcome</p>
  <!-- to create a custom event that will show or Modal and hide it by wrapping it in a div with a v-if-->
  <!-- for the teleport go to index.html , the reason we use .modals is because its a class that was given to the div-->
  <teleport to=".modals" v-if="showModal">
    <!-- lets work with props so that we can access data in the child components(prop: header in the modal) 
to pass in arrays or bolean we need to data bind otherwise it will just be displayed as a string....
-->
    <Modal
      :header="header"
      text="Grab your free Getaway"
      v-for="arrays in array"
      :key="arrays"
      :array="array"
      theme="sale"
      @closeModal="toggleModal"
    />
    <!-- to listen to event we emit we set the click event to the name of the method we listening to and set it equal to method we ref (@closeModal="toggleModal") -->
  </teleport>
  <!-- now that we have the custom event lets create a button that will change the value of the showModal -->
  <button @click="toggleModal">Open Modal</button>

  <div v-if="showSlot">
    <SlotModal theme="gdj" @closeModal="toggle">
      <h1>hello</h1>
      <p>Slots are where you place full ass templates</p>

      <!-- now that we can display our slots lets create a name slot which uses a template, to name this slot we use v-slot as we would with class and id -->
      <template v-slot:links>
        <h2>Template Slot Eg.</h2>
        <a href="#">sign up</a>
        <br />
        <a href="#">more info</a>
      </template>
    </SlotModal>
  </div>
  <button @click="toggle">Open Modal</button>
</template>

<script>
import Modal from "./components/Modal.vue";
import SlotModal from "./components/SlotModal.vue";

export default {
  name: "App",
  components: {
    Modal,
    SlotModal,
  },
  data() {
    return {
      header: "Sign up for the Getaway",
      array: ["ocean", "city", "mountains", "back"],
      showModal: false,
      showSlot: false,
    };
  },
  methods: {
    toggleModal() {
      this.showModal = !this.showModal;
    },
    toggle() {
      this.showSlot = !this.showSlot;
    },
  },
};
</script>

<style>
#app .modals {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
