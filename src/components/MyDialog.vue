<template>
  <div class="dialogWrapper" v-show="visible">
    <div class="dialog">
      <header>
        {{title}}
        <span class="close" @click="close">X</span>
      </header>
      <main>
        <slot></slot>
      </main>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'MyDialog',
    props: ['title', 'visible'],
    methods: {
      close(){
      console.log('close')
        this.$emit('close')
      }
    }
  }

</script>


<style scoped lang="scss">
   .dialogWrapper{
     position: fixed;
     background: hsla(0, 0%,0%,0.25);
     top: 0;
     left: 0;
     bottom: 0;
     right: 0;
     margin: 0;
     display: flex;
     justify-content: center;
     align-items: center;

   }
   .dialog{
     background: white;
     min-height: 12em;
     min-width: 18em;
     border-radius: 3px;
     background: #f6f6f6;
     > header{
       padding: 16px;
       display: flex;
       justify-content: space-between;
       > .close{
               cursor: pointer;
            }
     }

     > main{
       padding: 16px;
     }
   }
</style>
