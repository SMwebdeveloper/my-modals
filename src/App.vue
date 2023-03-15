<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <!-- first modal -->
          <button class="btn-primary" @click="modalFirst = !modalFirst">
            Show first modal
          </button>
          <modals
            title="First modal"
            v-if="modalFirst"
            @close="modalFirst = false"
          >
            <template #body>
              <p>Text TEct gfsajdagfasdjgfa</p>
              <button class="btn-primary" @click="modalFirst = !modalFirst">
                Well Done
              </button>
            </template>
          </modals>

          <!-- second modal -->
          <button
            class="btn-primary"
            @click="modalSecond.show = !modalSecond.show"
          >
            Show modal with form
          </button>
          <modals
            title="Second modal"
            v-if="modalSecond.show"
            @close="modalSecond.show = false"
          >
            <template #body>
              <form @submit.prevent="submitSecondForm">
                <label>Name:</label>
                <input type="text" required v-model="modalSecond.name" />
                <label>Email:</label>
                <input type="email" required v-model="modalSecond.email" />
                <button class="btn-primary">Submit</button>
              </form>
            </template>
          </modals>

          <!-- modal with validate -->
          <button
            class="btn-primary"
            @click="modalValidate= !modalValidate"
          >
            Show modal with form + validate
          </button>
          <modalValidate v-if="modalValidate" @close="modalValidate = false"/>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import modals from "@/components/UI/Modals.vue";
import modalValidate from "@/components/ModalValidate.vue";
export default {
  components: { modals, modalValidate },
  data() {
    return {
      modalFirst: false,
      modalSecond: {
        show: false,
        name: "",
        email: "",
      },
      modalValidate:false,
    }
  },
  methods:{
    submitSecondForm() {
      const result =  {
        name:this.modalSecond.name,
        email:this.modalSecond.email
      }

      this.modalSecond.name = ''
      this.modalSecond.email = ''
      this.modalSecond.show = false
      console.log(result);
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Montserrat", sans-serif;
}

a {
  text-decoration: none;
}

input,
textarea,
select button {
  border: 1px solid #ccc;
}

ul li {
  list-style: none;
  margin: 0;
  padding: 0;
}

.wrapper {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  margin: 0;
}

.content-wrapper {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.container {
  width: 100%;
  flex: 0 0 auto;
  position: relative;
  max-width: 1200px;
  margin: 0 auto;
}

.btn-primary {
  margin-top: 20px;
  padding: 8px 25px;
  background: rgb(5, 91, 148);
  outline: none;
  border: 1px solid #ccc;
  border-radius: 50px;
  color: #f5f5f5;
  font-size: 24px;
  font-weight: 500;
  cursor: pointer;
}
form{
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: space-between;
}
form label{
  font-size: 20px;
  color: rgb(32, 18, 107);
  font-weight: 500;
  margin-bottom: 10px;
}

form input{
  width: 400px;
  border: 1px solid #c5c5c5;
  font-size: 18px;
  font-weight: 500;
  padding: 10px 20px;
  outline: none;
  background: #f5f5f5;
  border-radius:50px;
  height: 30px;
}
</style>
