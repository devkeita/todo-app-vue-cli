<template>
  <div class="home">
    <add-form />
    <todo />
  </div>
</template>

<script>
  import AddForm from "../components/AddForm";
  import Todo from "../components/Todo";

  export default {
    components: {
      AddForm,
      Todo
    }
  }
</script>
