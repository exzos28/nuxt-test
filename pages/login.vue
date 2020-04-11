<template>
  <section class="section">
    <div class="container">
      <div class="columns">
        <div class="column is-4 is-offset-4">
          <h2 class="title has-text-centered">Welcome back!</h2>

          <Notification :message="error" v-if="error" />

          <form method="post" @submit.prevent="login">
            <div class="field">
              <label class="label">Phone</label>
              <div class="control">
                <input type="text" class="input" name="phone" v-model="phone" required />
              </div>
            </div>
            <div class="field">
              <label class="label">Password</label>
              <div class="control">
                <input type="password" class="input" name="password" v-model="password" required />
              </div>
            </div>
            <div class="control">
              <button type="submit" class="button is-dark is-fullwidth">Log In</button>
            </div>
          </form>
          <!-- <div class="has-text-centered" style="margin-top: 20px">
            <p>
              Don't have an account?
              <nuxt-link to="/register">Register</nuxt-link>
            </p>
          </div> -->
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Notification from "~/components/Notification";

export default {
  middleware: "guest",
  components: {
    Notification
  },

  data() {
    return {
      phone: "",
      password: "",
      error: null
    };
  },

  methods: {
    async login() {
      try {
        await this.$auth.loginWith("local", {
          data: {
            phone: this.phone,
            password: this.password
          }
        });
        this.$router.push("/posts");
      } catch (e) {
        this.error = e;
      }
    }
  }
};
</script>