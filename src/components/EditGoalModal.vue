<template>
  <div class="addGoalModalCont">
    <div class="flexModalCont">
      <div class="addGoalModal">

        <form v-on:submit.prevent="editGoal">
          <header>
            <input v-model.trim="name" required minlength="5" maxlength="100"/>
            <button class="btnClose" @click="close">
              <svg width="26" height="26" viewBox="0 0 26 26" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path
                    d="M14.4361 13.0008L25.7023 1.73457C26.0989 1.33792 26.0989 0.694822 25.7023 0.298221C25.3056 -0.0983798 24.6625 -0.0984305 24.2659 0.298221L12.9997 11.5644L1.73359 0.298221C1.33694 -0.0984305 0.693845 -0.0984305 0.297244 0.298221C-0.0993563 0.694873 -0.099407 1.33797 0.297244 1.73457L11.5634 13.0007L0.297244 24.2669C-0.099407 24.6636 -0.099407 25.3067 0.297244 25.7033C0.495545 25.9016 0.755494 26.0007 1.01544 26.0007C1.27539 26.0007 1.53529 25.9016 1.73364 25.7033L12.9997 14.4371L24.2659 25.7033C24.4642 25.9016 24.7241 26.0007 24.9841 26.0007C25.244 26.0007 25.5039 25.9016 25.7023 25.7033C26.0989 25.3066 26.0989 24.6635 25.7023 24.2669L14.4361 13.0008Z"
                    fill="black"/>
              </svg>
            </button>
          </header>
          <hr>
          <section class="addGoalModalBody">
            <div class="addGoalNameInput">
              <label for="addGoalAuthor">Автор</label>
              <label for="addGoalCommand">Отдел</label>
              <label for="addGoalDateStart">Период</label>
              <label for="addGoalExecutor">Ответственный</label>
              <label for="addGoalDescr">Описание цели</label>
            </div>
            <div class="addGoalInput">
              <div class="modal_user_name">
                <img class="icon_user" src="../style/img/User.png" alt="">
                <p>{{author}}</p>
              </div>
              <select v-model="command" id="addGoalExecutor" class="input_user">
                <option selected hidden>{{command}}</option>
                <option v-for="(com, index) in this.$store.state.commands" v-bind:key="index">
                  {{com}}
                </option>
              </select>
              <div class="addGoalDate">
                <input v-model="dateStart" id="addGoalDateStart" class="input_user" placeholder="Дата начала" type="text"
                      onfocus="(this.type='date')" onblur="(this.type='text')" required>
                <input v-model="dateEnd" id="addGoalDateEnd" class="input_user" placeholder="Дата окончания" type="text"
                      onfocus="(this.type='date')" onblur="(this.type='text')" required>
              </div>
              <select v-model="executor" id="addGoalExecutor" class="input_user">
                <option selected hidden>{{executor}}</option>
                <option v-for="(men, index) in this.$store.state.people" v-bind:key="index">
                  {{men}}
                </option>
              </select>
              <textarea v-model="descr" id="addGoalDescr" class="input_user" type="text"
                        placeholder="Описание цели" minlength="5" maxlength="500"></textarea>
            </div>
          </section>
          <footer>
            <button type="submit" class="button_pass">
              Сохранить
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
  name: 'EditGoalModal',

  props: ['idGoal'],

  data: () => ({
    name: '',
    author: '',
    dateStart: '',
    dateEnd: '',
    executor: '',
    command: '',
    descr: ''
  }),

  mounted: function () {
    this.$store.state.goals.forEach(goal => {
      if (goal.id === this.idGoal) {
          this.name = goal.name;
          this.author = goal.author;
          this.dateStart = goal.dateStart;
          this.dateEnd = goal.dateEnd;
          this.executor = goal.executor;
          this.command = goal.command;
          this.descr = goal.descr;
        }
    });
  },

  methods: {
    close() {
      this.$emit('close');
    },

    editGoal() {
      let modifiedGoal = {
        name: this.name,
        command: this.command,
        dateStart: this.dateStart,
        dateEnd: this.dateEnd,
        id: this.idGoal,
        descr: this.descr,
        executor: this.executor
      }
      this.$store.commit('editGoal', modifiedGoal);
      this.$emit('close');
    }
  },
}
</script>

<style scoped>
.addGoalModal {
  padding: 0 0 30px;
}

.modal_user_name {
  margin-bottom: 23px;
}
</style>