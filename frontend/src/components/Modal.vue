<template>
  <div class="background">
    <div class="modal">
      <header v-if="title"><h3>{{title}}</h3></header>
      <p>{{text}}</p>
      <footer>
        <button class="inverted" @click="action()">{{actionName}}</button>
        <button class="cancel" @click="onCancel()">Cancel</button>
      </footer>
    </div>
  </div>
</template>
<script>
  export default {
    props: ['title', 'text', 'action', 'actionName', 
    'onCancel']
  }
</script>
<style lang="scss" scoped>
  .background {
    background: rgba(0,0,0,.25);
    display: flex;
    align-items: center;
    justify-content: center;
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    z-index: 200;
    padding: 1.5em;
    box-sizing: border-box;
  }
  
  .modal {
    background: white;
    padding: 0;
    border-radius: 1em;
    overflow: hidden;
    max-width: 400px;
    margin-left: auto;
    margin-right: auto;
  }
  
  header {
    background: #4a4a4a;
  }
  
  p {
    padding-left: 1em;
    padding-right: 1em;
  }
  
  h3 {
    color: white;
    text-align: center;
    margin: 0;
    padding: .5em;
  }
  
  footer {
    display: flex;
    
    button {
      flex-grow: 1;
      
      &.cancel {
        background-image: linear-gradient(120deg, #84fab0 0%, #8fd3f4 100%);
      }
    }
  }
</style>