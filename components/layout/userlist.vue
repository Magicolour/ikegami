<template>
  <div :class="[ 'c-parts-userlist', {
    collapsed: collapse
  } ]">
    <ul>
      <cell
        v-for="c in combatants"
        :combatant="c"
        :topdps="topdps"
        :key="c.name">
        <detailed-view :c="c" :e="e" />
      </cell>
    </ul>
  </div>
</template>

<script>

import { mapState, mapGetters } from 'vuex'

import cell from '../user/cell.vue'
import detailedView from '../user/detailed-view.vue'

export default {
  components: {
    cell,
    detailedView
  },
  computed: {
    ...mapState('encounter', {
      // assuming worst case of combatant count: 124px * 75% * 32 = 2976px
      combatants: state => state.combatants?.slice(0, 32),
      topdps: 'topdps',
      e: 'encounter'
    })
  }
}

</script>

<style lang="sass">

.c-parts-userlist
  display: flex
  width: 100%

  align-items: flex-start
  justify-content: center

  // this container exists for alignment.
  // |      *------*      |
  // -> this may implemented by only one container
  // |*-------------------|---*
  // -> but this is why <ul> exists
  > ul
    display: flex
    max-width: 100%

    align-items: flex-start
    justify-content: flex-start

    .c-user-cell
      flex-shrink: 0

</style>
