<template>
  <div class="container-fluid">
    <div class="space"></div>
    <div class="row">
        <div class="col-md-8 offset-md-2 keypad"> 
          <Display :operation="operation" :display="toDisplay" v-if="toggleOnOff" /> 
          <Display class="offDisplay" v-else />
        </div>
    </div>
    <div class="row ">
      <div class="col-md-8 offset-md-2">
        <div class="row keypad">
          <div class="col-md-3 col-sm-3" v-for="keybtn in keysList" :key="keybtn"> 
              <Key :valor="keybtn"  @click="insertValue(keybtn)" />
          </div>
        </div>
      </div>
    </div>
</div>
</template>

<script>
import Display from '@/components/Display.vue'
import Key from '@/components/Key.vue'
import { ref } from 'vue'

export default {
  name: 'Home',
  components:{Display, Key},
  setup(){
    const operation = ref ('0')
    const toDisplay = ref ('0')
    const keysList = ['(',')','CE','ON/OFF','7','8','9','/','4','5','6','*','1','2','3','-','0','.','=','+']
    const toggleOnOff = ref(true)
    let stack = ""

    const insertValue = digit => {
       switch (digit) {
          case '=':
            toDisplay.value = equalFunction(stack)
            break;
          case 'CE':
            clearFunction();
            break;
          case 'ON/OFF':
            onOffFunction();
            clearFunction();
            break;
          default:
          
          stack = stack + digit
            if (digit == '*' || digit == '/' || digit == '-' || digit == '+'){
                operation.value = stack 
            } 
            else{
              toDisplay.value = digit
              operation.value = stack
            }
            break;
        }
     }

    const equalFunction = mathExpression => {
      try {
              return eval(mathExpression) 
          } catch (err) {
              console.log(err.message)  
              operation.value = err.message
          }   
    }

    const clearFunction = () => {
        toDisplay.value = '0'
        stack = ' '
        operation.value = '0'
    }

    const onOffFunction = () => {
      toggleOnOff.value = !toggleOnOff.value
    }

        return {
          toggleOnOff,
          operation,
          toDisplay, 
          insertValue, 
          keysList
          }
  }
}
</script>

<style scoped>
.keypad {
  background-color: grey;
}
.space{
    min-height: 50px;
}
.offDisplay{
  background-color: cadetblue;
}

</style>
