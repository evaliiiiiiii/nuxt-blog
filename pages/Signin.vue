<template>
  <v-card
    class="mx-auto"
    max-width="500"
  >
    <v-card-title class="title font-weight-regular justify-space-between">
      <span>{{ currentTitle }}</span>
    </v-card-title>

    <v-window v-model="step">
      <v-window-item>
        <v-card-text>
          <v-text-field
            label="Password"
            type="password"
          ></v-text-field>
          <span class="caption grey--text text--darken-1">
            Please enter a password for your account
          </span>
        </v-card-text>
      </v-window-item>
    </v-window>

    <v-divider></v-divider>

    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn
        color="orange"
        depressed
      >
        Sign in
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
  export default {
    computed: {
      currentTitle () {
        switch (this.step) {
          default: return 'User login'
        }
      },
    },
  }
</script>
