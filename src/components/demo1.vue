<template>
  <div>
    <div class="item-name">
      <p style="display :inline;">{{ item.title }}</p>
    </div>
    <div class="btn-delete">
      <b-button
        variant="outline-danger"
        class="delete"
        @click.stop="del()"
        title="Xóa"
      >
        <b-icon-trash></b-icon-trash>
      </b-button>
    </div>
  </div>
</template>
<script>
export default {
  name: "demo1",
  /* data() {
    return {
      title: "Hello",
    };
  }, */
  props: {
    item:{
      type :Object,
      title : {
          type :  String,
          default : ""
        },
      id : Number,
      completed : Boolean,
      count : Number,
    },
  },
  methods :{
    del() {
      console.log('Trước');
      this.$emit('del');
      console.log('sau');
    }
  },
  watch: {},
  /* //life circle
  created(){

  },
  mounted(){

  },
  /// */
};
</script>
<style>
</style>