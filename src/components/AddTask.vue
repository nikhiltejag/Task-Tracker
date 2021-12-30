<template>
    <form @submit="onSubmit" class="add-form">
        <div class="form-control">
            <label>Task</label>
            <input type="text" v-model="text" name="text" placeholder="Add Task"/>
        </div>
        <div class="form-control">
            <label>Day & Time</label>
            <input type="text" name='day' v-model="day" placeholder="Add Day & Time"/>
        </div>
        <div class="form-control form-control-check">
            <label >Set Remainder</label>
            <input type="checkbox" v-model="remainder" name='remainder' />
        </div>
        <input type="submit" value="Save Task" class="btn btn-black"/>
    </form>
</template>

<script>
export default {
    name: 'AddTask',
    data() {
        return {
            text: '',
            day: '',
            remainder: false,
        }
    },
    methods: {
        onSubmit(event){
            event.preventDefault()
            if (!this.text){
                alert('Please add a task !!')
                return
            }
            let newTask = {
                id: Math.floor(Math.random() * 10000),
                text: this.text,
                day: this.day,
                remainder: this.remainder
            }
            this.$emit('add-new-task', newTask)
            this.text = ''
            this.day = ''
            this.remainder = ''
        }
    }
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 95%;
  /* height: 40px; */
  margin: 5px;
  margin-left: 0px;
  padding: 5px 7px;
  font-size: 16px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}

.btn {
    padding: 6px 12px;
    background-color: rgb(34, 179, 236);
    color: white;
    border: none;
    border-radius: 4px;
}
</style>