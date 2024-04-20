<template>
  <div class="homepage">
    <div class="formulario">
      <h1>Ref</h1>
      <p>Full Name: {{ refPerson.fullname }} | (Computed) Initials - {{ getRefPersonInitials }}</p>
      <p>Country of origin: {{ refPerson.age }} | (Watch) {{ refMayorDeEdad }}</p>
      <p>Country of origin: {{ refPerson.country }}</p>

      <div>
        <label for="fullname">First Name: </label>
        <input id="fullname" type="text" v-model="refPerson.fullname">
      </div>

      <div>
        <label for="country">Last Name: </label>
        <input id="country" type="text" v-model="refPerson.country">
      </div>

      <div>
        <label for="age">Age: </label>
        <input id="age" type="number" v-model="refPerson.age">
      </div>

      <br>

      <h1>Reactive</h1>
      <p>Full Name: {{ reactiveState.fullname }} | (Computed) Initials - {{ getReactivePersonInitials }}</p>
      <p>Country of origin: {{ reactiveState.age }} | (Watch) {{ reactiveState.reactiveMayorDeEdad }}</p>
      <p>Country of origin: {{ reactiveState.country }}</p>

      <div>
        <label for="fullname">First Name: </label>
        <input id="fullname" type="text" v-model="reactiveState.fullname">
      </div>

      <div>
        <label for="country">Last Name: </label>
        <input id="country" type="text" v-model="reactiveState.country">
      </div>

      <div>
        <label for="age">Age: </label>
        <input id="age" type="number" v-model="reactiveState.age">
      </div>
    </div>
  </div>
</template>

<script>
import { ref, reactive, watch, computed } from 'vue';

export default {
  name: 'HomePage',
  props: {
    person: Object,
    count: Number
  },
  setup(props) {
    const refPerson = ref(props.person);
    const refMayorDeEdad = ref("No es Mayor de edad")
    
    const reactiveState = reactive({
      fullname:"Pepe Aguacate",
      country: "Colombia",
      age: 20,
      reactiveMayorDeEdad:"No es Mayor de edad"
    })

    //REFS WATCH
    watch(refPerson.value, (newPerson) => {
      if (newPerson.age >= 18) {
        refMayorDeEdad.value = "Mayor de edad"
      } else {
        refMayorDeEdad.value = "No es Mayor de edad"
      }
    }, { deep: true, immediate: true });


    //REACTIVE WATCH
    watch(reactiveState, (newPerson) => {
      if (newPerson.age > 18) {
         newPerson.reactiveMayorDeEdad = "Mayor de edad"
      } else {
         newPerson.reactiveMayorDeEdad = "No es Mayor de edad"
      }
    }, { deep: true, immediate: true });

    // REF COMPUTED
    const getRefPersonInitials = computed(() => {
      return refPerson.value.fullname
        ? refPerson.value.fullname.split(' ').map(substring => substring.charAt(0)).join('.')
        : '';
    });

    // REACTIVE COMPUTED
    const getReactivePersonInitials = computed(() => {
      return reactiveState.fullname
        ? reactiveState.fullname.split(' ').map(substring => substring.charAt(0)).join('.')
        : '';
    });

    return {
      refPerson,
      getRefPersonInitials,
      getReactivePersonInitials,
      refMayorDeEdad,
      reactiveState,
    }
  },
}
</script>