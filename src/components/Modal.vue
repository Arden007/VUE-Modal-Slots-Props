<template>
<!-- we will be using a click event modifier so that the event will only fire on a certain condition, in this case when we click on the background-->
  <div class="backdrop" @click.self="closeModal">
      <!-- below is how we customise certain elements classes , by checking if the theme prop match the condition set which in this case is the theme props value being sale-->
      <div class="modal" :class="{ sale:theme === sale }">
          <h1>{{ header }}</h1>
          <p>{{ text }}</p>
          <li>{{array}}</li>
      </div>
  </div>
</template>

<script>
export default {
    // to use the props of the parent component we need a props object which will be an array , note that when we define a prop we wrap it in ""    
    props: ["header", "text", "array", "sale"],
    methods:{
        // we will create a custom event so that the parent comp can listen to the child , to allow the parent to listen we need to emit our custom event
        closeModal(){
        //we first ref the current comp with (this.) then we emit the event($emit) and the arguement will be the name of the event we want to emit
        this.$emit("closeModal")
        }
    }
}
</script>

<style scoped>
.modal {
    width: 400px;
    padding: 20px;
    margin: 100px auto;
    background: white;
    border-radius: 10px;
}
.backdrop {
    top: 0;
    position: fixed;
    background: rgba(0, 0, 0, 0.5);
    width: 100%;
    height: 100%;
}
/* the below is how we target a element within a class  */
.modal h1{
    color: #03cfb4;
    border: none;
    padding: 0;
}
.modal.sale {
    background: crimson;
    color: white;
}
.modal.sale h1 {
    color: white;
}
</style>