<template>
  <div class="addGoalModalCont">
    <div class="flexModalCont">
    <div class="addGoalModal">
      <form v-on:submit.prevent="deleteGoal">
        <div>
          Вы уверены, что хотите удалить выбранную цель?
        </div>
        <footer>
          <button type="submit" class="button_pass">
            Удалить
          </button>
          <button type="button" class="button_pass" @click="close">
            Отмена
          </button>
        </footer>
      </form>
    </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'DeleteGoalModal',
  methods: {
    close() {
      this.$emit('close');
    },

    deleteGoal() {
      this.$emit('delete');
      this.$emit('close');
    }
  },
}
</script>

<style scoped>
.addGoalModal footer {
  margin-top: 40px;
}
</style>
