<template lang="pug">
  .container.pt-5
    h1.app-name QuickNote
    .form-control.pt-5
      .card.center
        h1 {{ notesTitle }}
        input(

          type="text"
          :placeholder="placeholderText"
          v-model="inputValue"
          @keypress.enter="addNewNote"

          )
        h3 Текст заметки: {{ inputValue }}
        button.btn(@click="addNewNote") Добавить
        button.btn(@click="removeAll") Очистить
        ul.list(v-if="notes.length !== 0")
          li.list-item(v-for="(note, index) in notes") {{ index + 1 + "."}} {{ note }}
            button.btn.danger.notes(@click="removeNote(index, $event)") X
        p(v-else) Заметок пока нет.
        strong.counter Количество заметок {{ notes.length }}
</template>

<script>
  export default {
    name: "MainComponent",
    data() {
      return {
        counterTitle: "Счетчик",
        counter: 0,
        notesTitle: "Заметки",
        placeholderText: "Введите название заметки",
        inputValue: "",
        notes: [],
      }
    },
    methods: {
      addNewNote() {
        if (this.inputValue !== '') {
          this.notes.push(this.inputValue)
          this.inputValue = ""
        }
      },
      removeNote(index) {
        this.notes.splice(index, 1)
      },
      removeAll() {
        this.notes.splice(0)
      },
    },
    watch: {
      inputValue(value) {
        if (value.length > 25) {
          this.inputValue = ''
        }
      }
    },
  }

</script>

<!--//scoped - стили действуют в области видимости-->
<style lang="css">

@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500&display=swap');

* {
  box-sizing: border-box;
}

body {
  font-family: Inter, Roboto, Oxygen, Fira Sans, Helvetica Neue, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size: 16px;
  color: #fff;
  background: #372963;
}

hr {
  margin: 1rem 0;
}

strong,
.bold {
  font-weight: 500;
}

ol,
p,
ul {
  line-height: 1.7;
}

a {
  color: #3eaf7c;
  font-weight: 500;
  text-decoration: none;
}

h1,
h2,
h3,
h4,
h5,
h6 {
  font-weight: 500;
  line-height: 1.45;
}

h1 {
  font-size: 2.2rem;
  font-weight: 600;
}

h2 {
  font-size: 1.65rem;
  padding-bottom: 0.3rem;
  border-bottom: 1px solid #eaecef;
}

h3 {
  font-size: 1.35rem;
}

.app-name {
  font-size: 50px;
  font-family: "Chalkboard SE";
  margin: 0;
}

.danger {
  color: #e53935;
}

.btn {
  color: #42b983;
  position: relative;
  place-content: center;
  place-items: center;
  width: fit-content;
  border-radius: 99px;
  letter-spacing: 0.05em;
  border: 1px solid #42b983;
  text-decoration: none;
  text-transform: uppercase;
  margin-right: 10px;
  padding: 0.5rem 1.5rem;
  margin-top: 10px;
  white-space: nowrap;
  font-weight: 700;
  outline: none;
  background: #fff;
  transition: all 0.22s;
}

.btn:hover {
  cursor: pointer;
  opacity: 0.8;
}

.btn:active {
  box-shadow: inset 1px 1px 1px rgba(0, 0, 0, 0.3);
}

.btn.danger {
  background: #e53935;
  color: #fff;
  border-color: #e53935;
}

.btn.danger.notes {
  margin-left: 15px;
  margin-bottom: 10px;
}

.container {
  margin: 0 auto;
  max-width: 1000px;
}

.pt-5 {
  padding-top: 5rem;
}

.form-control {
  position: relative;
  margin-bottom: 0.5rem;
}

.form-control input {
  margin: 0;
  outline: none;
  border: 1px solid rgba(255, 255, 255, 0.25);
  display: block;
  width: 100%;
  color: #2c3e50;
  padding: 0.5rem 1.5rem;
  border-radius: 5px;
  font-size: 1rem;
}

.form-control label {
  display: block;
  margin: 0 0 0.3rem 0.3rem;
  font-weight: 500;
}

.form-control input:active,
.form-control input:focus {
  transition: border 0.22s;
  border: 2px solid #42b983;
}

.card {
  padding: 1rem;
  border-radius: 10px;
  box-shadow: 2px 3px 10px rgba(0, 0, 0, 0.2);
  background: #493B71;
}

.card.center {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.list {
  margin: 0;
  padding: 0;
  list-style: none;
}

.list-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.5rem 0;
}

.counter {
  padding-top: 20px;
}

</style>