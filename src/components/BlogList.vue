<template>
  <div class="list-wrap">
    <TransitionGroup name="list" tag="ul">
    <!-- <ul> -->
      <!-- v-for in  :key  -->
      <li v-for="(item,index) in memodata" v-bind:key="index" class="shadow">
        <i class="fas fa-check check-bt" @click="updateMemo(item,index)"
          v-bind:class="{memoComplete:item.complete}"></i>
        <span :class="{memoCompleteTxt:item.complete}">{{item.memotitle}}</span>
        <div class="info">
          <span class="icon"
            :style="{backgroundImage:'url(' + require(`@/assets/images/${item.memoicon}`) + ')'}"></span>
          <span class="date">{{item.memodate}}</span>
          <span class="remove-bt" @click="removeMemo(item.id,index)">
            <i class="fas fa-trash-alt"></i>
          </span>
        </div>
      </li>
      <!-- </ul> -->
    </TransitionGroup>
  </div>
</template>

<script>
  export default {
    props: ['memodata'],

    setup(props, context) {


      const removeMemo = (item, index) => {
        console.log(index);

        // console.log('지워');
        context.emit('removeitem', item, index);
      }
      const updateMemo = (item, index) => {


        context.emit('updateitem', item, index);
      }
      return {

        removeMemo,
        updateMemo
      }
    }
  }
</script>

<style scoped>
  li {
    display: flex;
    min-height: 50px;
    line-height: 50px;
    margin: 10px 0;
    background-color: #fff;
    border-radius: 5px;
    padding: 0 20px;

  }

  .remove-bt {
    margin-left: 10px;

    cursor: pointer;
    color: hotpink;
  }

  .check-bt {
    color: #62acde;
    line-height: 50px;
    margin-right: 10px;
    cursor: pointer;
  }

  .memoComplete {
    color: #b3adad;

  }

  .memoCompleteTxt {
    color: #b3adad;
    text-decoration: line-through;
  }

  .info {
    margin-left: auto;

  }

  .icon {
    display: inline-block;
    width: 40px;
    height: 40px;
    margin-right: 10px;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;


  }

  .date {}


  /* 애니메이션 */

  .list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

</style>