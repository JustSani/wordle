<template>
  <div class="mt-4">
    <v-text-field filled hint="Inserisci una parola di 5 lettere" :error-messages="error ? [error] : []" persistent-hint autofocus v-model="guess"></v-text-field>
    <v-btn class="mt-2" color="primary" large block @click="sendGuess">Invia</v-btn>
  </div>
</template>
<script>

import { words } from '~/utils/words'

export default {
  data: () => ({
    guess: '',
    error: null,
  }),
  methods: {
    validateGuess() {
      // TODO validare la parola inserita (variabile this.guess)
      // - controllare che la lunghezza sia di esattamente 5 lettere
      // - controllare che la parola faccia parte del dizionario (words)
      // - restituire true se entrambe le condizioni sono verificate, false altrimenti

      // TIP: valorizzando this.error con un messaggio di errore questo verrà mostrato nella text field

      if(this.guess.length != 5){
        this.error = "Lunghezza della parola non corretta"
        return false
      }
      else if(!words.includes(this.guess)){
        this.error ="Parola non nel dizionario"
        return false;
      }
      else{
        this.error =""
        return true;
      }
      
    },
    sendGuess() {
      if(!this.validateGuess()) { return }

      this.$emit('guess', this.guess)
      this.guess = ''
    }
  }
}
</script>