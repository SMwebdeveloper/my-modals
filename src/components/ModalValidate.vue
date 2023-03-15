<template lang="">
  <modal title="Second modal" @close="$emit('close')">
    <template #body>
      <form @submit.prevent="onSubmit">
        <!-- name -->
        <div class="form-item" :class="{ errorInput: v$.name.$error }">
          <label>Name:</label>
          <p class="errorText" v-if="v$.name.$error">Field is required</p>
          <input
            v-model="name"
            :class="{ error: v$.name.$error }"
            @blur="v$.name.$touch()"
          />
        </div>
        <!-- email -->
        <div class="form-item" :class="{ errorInput: v$.email.$error }">
          <label>Email:</label>
          <p class="errorText" v-if="v$.email.$error">Field is required</p>
          <!-- <p class="errorText" v-if="!v$.email.email">Email is not correct</p> -->
          <input
            v-model="email"
            :class="{ error: v$.email.$error }"
            @blur="v$.email.$touch()"
          />
        </div>
        <button class="btn-primary">Submit</button>
      </form>
    </template>
  </modal>
</template>
<script>
import { useVuelidate } from "@vuelidate/core";
import { required, email } from "@vuelidate/validators";

import modal from "@/components/UI/Modals.vue";
export default {
    setup: () => ({ v$: useVuelidate() }),
  components: { modal },
  data() {
    return {
      name: "",
      email: "",
    };
  },
  validations() {
    return {
      name: { required },
      email: { required, email },
    };
  },
  methods: {
    onSubmit() {
        this.v$.$touch()
        if(!this.v$.$invalid){
            const user = {
                name: this.name,
                email:this.email
            }

            // Done
            this.name = ''
            this.email = ''
            this.v$.$reset()
            this.$emit('close')
        }
    }
  }
};
</script>
<style lang="css" scoped>
.form-item .errorText{
    margin-bottom: 8px;
    font-size: 13.4px;
    color: #de4040;
}

.form-item .errorInput .errorText{
    display: block;
}

input.error{
    border-color: #de4040;
}

form,
.form-item{
    display: flex;
    flex-direction: column;
    align-items: center;
}
input{
    height: 50px;
}
</style>
