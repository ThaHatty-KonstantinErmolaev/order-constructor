<template>
  <div :style="{position: 'relative', top:item.position.top+'px', left:item.position.left+'px', zIndex:1+item.id}" class="formItem"
       v-bind:class="{none: !item.visible}"
  >
    <h3>{{item.title}}</h3>
    <div class="inputs">
      <slot></slot>
    </div>
    <div>
      <a v-if="!item.order.last" v-on:click="$emit('move-left',item.id)" class="btn btn-outline-dark">Далее</a>
      <br>
      <a v-if="!item.order.first" v-on:click="$emit('move-right',item.id)" class="btn btn-outline-dark">Назад</a>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      type: Object
    }
  },
}
</script>

<style scoped>

</style>