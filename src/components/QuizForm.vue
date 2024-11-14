<script setup lang="ts">
import { computed, ref } from 'vue'

const cheval = ref<string | null>(null)
const chat = ref<string | null>(null)
const capitale = ref<string | null>(null)
const filled = computed<boolean>(
  () => cheval.value !== null && chat.value !== null && capitale.value !== null,
)

function submit(event: Event): void {
  event.preventDefault()

  let point = 0
  if (cheval.value == 'blanc') {
    point = point + 1
  }
  if (chat.value == '4 pattes') {
    point = point + 1
  }
  if (capitale.value == 'Berne') {
    point = point + 1
  }

  let message: string = ''
  if (point == 3) {
    message = "Bravo ! C'est parfait !"
  }

  if (filled.value) {
    alert(`
    Vous avez choisi la couleur ${cheval.value}
    Vous avez choisi ${chat.value}
    Vous avez choisi la ville de ${capitale.value}


    Vous avez fait ${point} sur 3 !
    ${message}
    `)
  }
}

function refresh(): void {
  location.reload()
}
</script>

<template>
  <form @submit="submit">
    De quelle couleur est le cheval blanc de Napoléon ?
    <div class="form-check">
      <input
        id="chevalBlanc"
        v-model="cheval"
        class="form-check-input"
        type="radio"
        name="cheval"
        value="blanc"
      />
      <label class="form-check-label" for="chevalBlanc">Blanc</label>
    </div>
    <div class="form-check">
      <input
        id="chevalBrun"
        v-model="cheval"
        class="form-check-input"
        type="radio"
        name="cheval"
        value="brun"
      />
      <label class="form-check-label" for="chevalBrun">Brun</label>
    </div>
    <div class="form-check">
      <input
        id="chevalNoir"
        v-model="cheval"
        class="form-check-input"
        type="radio"
        name="cheval"
        value="noir"
      />
      <label class="form-check-label" for="chevalNoir">Noir</label>
    </div>
    <div class="form-check">
      <input
        id="chevalRouge"
        v-model="cheval"
        class="form-check-input"
        type="radio"
        name="cheval"
        value="rouge"
      />
      <label class="form-check-label" for="chevalRouge">Rouge</label>
    </div>
  </form>
  <br />

  <form @submit="submit">
    Combien de pattes a un chat ?
    <div class="form-check">
      <input
        id="2pattes"
        v-model="chat"
        class="form-check-input"
        type="radio"
        name="chat"
        value="2 pattes"
      />
      <label class="form-check-label" for="2pattes">2 pattes</label>
    </div>
    <div class="form-check">
      <input
        id="4pattes"
        v-model="chat"
        class="form-check-input"
        type="radio"
        name="chat"
        value="4 pattes"
      />
      <label class="form-check-label" for="4pattes">4 pattes</label>
    </div>
    <div class="form-check">
      <input
        id="8pattes"
        v-model="chat"
        class="form-check-input"
        type="radio"
        name="chat"
        value="8 pattes"
      />
      <label class="form-check-label" for="8pattes">8 pattes</label>
    </div>
    <div class="form-check">
      <input
        id="10pattes"
        v-model="chat"
        class="form-check-input"
        type="radio"
        name="chat"
        value="10 pattes"
      />
      <label class="form-check-label" for="10pattes">10 pattes</label>
    </div>
  </form>
  <br />

  <form @submit="submit">
    Quelle est la capitale de la Suisse ?
    <div class="form-check">
      <input
        id="Geneve"
        v-model="capitale"
        class="form-check-input"
        type="radio"
        name="capitale"
        value="Genève"
      />
      <label class="form-check-label" for="geneve">Genève</label>
    </div>
    <div class="form-check">
      <input
        id="Lausanne"
        v-model="capitale"
        class="form-check-input"
        type="radio"
        name="capitale"
        value="Lausanne"
      />
      <label class="form-check-label" for="lausanne">Lausanne</label>
    </div>
    <div class="form-check">
      <input
        id="Berne"
        v-model="capitale"
        class="form-check-input"
        type="radio"
        name="capitale"
        value="Berne"
      />
      <label class="form-check-label" for="berne">Berne</label>
    </div>
    <div class="form-check">
      <input
        id="Zurich"
        v-model="capitale"
        class="form-check-input"
        type="radio"
        name="capitale"
        value="Zurich"
      />
      <label class="form-check-label" for="zurich">Zurich</label>
    </div>
  </form>
  <br />

  <form @submit="submit">
    <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    <button class="btn btn-primary" button @:click="refresh">Réinitialiser</button>
  </form>
</template>
