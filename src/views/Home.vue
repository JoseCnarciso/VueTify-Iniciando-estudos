<template>
  <h1>Conteúdo principal</h1>
  <p>Este é o conteúdo principal da página.</p>
  <p id="bem_vindo_usuario"></p>
  <p>Nome: <span id="nome"></span> </p>
  <p>Username: <span id="username"></span> </p>
  <p>Qtd de seguidores: <span id="qtd_seguidores"></span> </p>
  <p>Qtd de publicações: <span id="qtd_publicacoes"></span> </p>

  <v-form ref="form" @submit.prevent="handleSubmit">
    <v-text-field label="Nome" variant="outlined" :rules="[v => !!v || 'Nome é obrigatório!']"
      v-model="nome"></v-text-field>

    <v-text-field label="Email" variant="outlined" :rules="[v => !!v || 'Email é obrigatório!']"
      v-model="email"></v-text-field>

    <v-btn variant="tonal" color="green" type="submit">Cadastrar</v-btn>

    <v-snackbar v-model="snackbar" :timeout="timeout">
      {{ text }}

      <template v-slot:actions>
        <v-btn color="red" variant="text" @click="snackbar = false">
          Fechar
        </v-btn>
      </template>
    </v-snackbar>

    <v-select clearable label="Escolher" :items="['Batata', 'Ovo', 'Farinha', 'Oleo', 'Beringela', 'Wyoming']"
      variant="solo-inverted"></v-select>
  </v-form>



  <v-container class="bg-surface-variant">
    <v-row no-gutters>
      <v-col v-for="n in 3" :key="n" cols="12" sm="4">
        <v-sheet class="ma-2 pa-2">
          <v-card variant="tonal" class="ma-5 pt-10 rounded-circle" v-for="(nome, index) in nomes" :key="index">
            <v-card-text>
              <img :width="200" :src="nome" alt="usuario">
            </v-card-text>
          </v-card>
        </v-sheet>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      snackbar: () => ({
        snackbar: false,
        timeout: 2000,
        text: `Hello, I'm a snackbar`,
      }),
      email: '',
      nome: '',
      nomes: [
        'https://http.cat/images/202.jpg',
        'https://http.cat/images/301.jpg',
        'https://http.cat/images/404.jpg',
        'https://http.cat/images/408.jpg',
        'https://http.cat/images/417.jpg',
        'https://http.cat/images/498.jpg',
        'https://http.cat/images/500.jpg'
      ],
      estadosList: ['']
    }
  },
  methods: {
    async handleSubmit() {
      const { valid } = await this.$refs.form.validate()

      if (valid) {
        this.text = 'Usuário cadastrado com sucesso!'

        this.snackbar = true
        //Limpar os campos
        this.$refs.form.reset()
      }
    }
  }
}
</script>
