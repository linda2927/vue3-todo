<script>
export default {
  name: 'TodoListNew',
};
</script>

<script setup>
import { reactive, toRefs, inject, ref } from 'vue';

const today = inject('today');
const addTodo = inject('addTodo');
const val_obj = reactive({
  job: '',
  date: today,
  today: today,
});

const onAddTodo = () => {
  if (val_obj.job.length > 0) {
    addTodo(val_obj.job, val_obj.date);
    val_obj.job = '';
    val_obj.date = today;
  }
};
const { job, date } = toRefs(val_obj); // script setup 에서 스프레드 연산자 사용 금지

</script>

<template>
  <section class="mb-5">
    <div class="container">
      <div class="row justify-content-center m-2">
        <div class="col border border-primary rounded">
          <input id="todo_input" v-model="job" type="text" class="form-control my-2" placeholder="여기에 할일을 적으세요"/>
          <div class="row my-2">
            <div class="col-6">
              <input v-model="date" type="date" :min="today"/>
            </div>
            <div class="col-6">
              <button type="button" class="btn btn-primary btn-sm float-end" @click="onAddTodo">작업 추가</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
