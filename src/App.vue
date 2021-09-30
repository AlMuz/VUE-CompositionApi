<template>
  <div class="container">
    <form class="card" @submit.prevent="submit">
      <h1>Auth</h1>

      <div
        class="form-control"
        :class="{ invalid: !form.email.valid && form.email.touched }"
      >
        <label for="email">Email</label>
        <input
          id="email"
          v-model="form.email.value"
          type="email"
          @blur="form.email.blur"
        />
        <small v-if="form.email.errors.required && form.email.touched">
          This field is required
        </small>
      </div>

      <div
        class="form-control"
        :class="{ invalid: !form.password.valid && form.password.touched }"
      >
        <label for="password">Password</label>
        <input
          id="password"
          v-model="form.password.value"
          type="password"
          @blur="form.password.blur"
        />
        <small v-if="form.password.errors.required && form.password.touched">
          This field is required
        </small>
        <small
          v-else-if="form.password.errors.minLength && form.password.touched"
        >
          This field min length is 10.
        </small>
      </div>

      <button class="btn primary" type="submit" :disabled="!form.valid">
        Submit
      </button>
    </form>

  </div>
</template>

<script>
import { useForm } from "./hooks/form";
import { required, minLength } from "./utils/validation";

export default {
  setup() {
    const form = useForm({
      email: {
        value: "",
        validators: { required },
      },
      password: {
        value: "",
        validators: { required, minLength: minLength(10) },
      },
    });

    function submit() {
      console.log("Email", form.email.value);
      console.log("Password", form.password.value);
    }

    return { form, submit };
  },
};
</script>
