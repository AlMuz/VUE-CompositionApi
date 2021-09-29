<template>
  <div class="container">
    <form class="card" @submit.prevent="submit">
      <h1>Auth</h1>

      <pre>{{ form.email }}</pre>
      <pre>{{ form.password }}</pre>

      <div class="form-control">
        <label for="email">Email</label>
        <input id="email" v-model="form.email.value" type="email" />
      </div>

      <div class="form-control">
        <label for="password">Password</label>
        <input id="password" v-model="form.password.value" type="password" />
      </div>

      <button class="btn primary" type="submit">Submit</button>
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
        value: "test@example.com",
        validators: { required },
      },
      password: {
        value: "MyPsswrd",
        validators: { required, minLength: minLength(10) },
      },
    });

    function submit() {}

    return { form, submit };
  },
};
</script>
