
<style scoped>
:global(body) {
  background-color: #e3e3e3;
  margin-top: 20px;
  margin-bottom: 20px;
}
</style>

<script setup lang="ts">
import type { FormError, FormErrorEvent, FormSubmitEvent } from '#ui/types'
import type { RefSymbol } from '@vue/reactivity';

const pageTitle = ref('Math Sheet');

const sheetHeader = ref('Rounding Off to Nearest 10');

let score = ref(0)
let formStatus = ref(0)

const questions = [
  {
    id: 1,
    ask: '17 rounded off to the nearest 10 is..',
    answer: '20',
    name: 'q1',
    choices: [
      {
        label: '10',
        value: '10'
      },
      {
        label: '20',
        value: '20'
      },
      {
        label: '17',
        value: '17'
      }
    ],

  },
  {
    id: 2,
    ask: '45 rounded off to the nearest 10 is..',
    answer: '50',
    name: 'q2',
    choices: [
      {
        label: '50',
        value: '50'
      },
      {
        label: '45',
        value: '45'
      },
      {
        label: '40',
        value: '40'
      }
    ],

  },
  {
    id: 3,
    ask: '75 rounded off to the nearest 10 is..',
    answer: '80',
    name: 'q3',
    choices: [
      {
        label: '70',
        value: '70'
      },
      {
        label: '80',
        value: '80'
      },
      {
        label: '175',
        value: '175'
      }
    ],
  },
  {
    id: 4,
    ask: '19 rounded off to the nearest 10 is..',
    answer: '20',
    name: 'q4',
    choices: [
      {
        label: '20',
        value: '20'
      },
      {
        label: '10',
        value: '10'
      },
      {
        label: '19',
        value: '19'
      }
    ],
  },
  {
    id: 5,
    ask: '64 rounded off to the nearest 10 is..',
    answer: '60',
    name: 'q5',
    choices: [
      {
        label: '64',
        value: '64'
      },
      {
        label: '70',
        value: '70'
      },
      {
        label: '60',
        value: '60'
      }
    ],
  },
  {
    id: 6,
    ask: '0 rounded off to the nearest 10 is..',
    answer: '0',
    name: 'q6',
    choices: [
      {
        label: '10',
        value: '10'
      },
      {
        label: '1',
        value: '1'
      },
      {
        label: '0',
        value: '0'
      }
    ],
  },
  {
    id: 7,
    ask: '98 rounded off to the nearest 10 is..',
    answer: '100',
    name: 'q7',
    choices: [
      {
        label: '80',
        value: '80'
      },
      {
        label: '100',
        value: '100'
      },
      {
        label: '89',
        value: '89'
      }
    ],
  },
  {
    id: 8,
    ask: '199 rounded off to the nearest 10 is..',
    answer: '200',
    name: 'q8',
    choices: [
      {
        label: '190',
        value: '190'
      },
      {
        label: '100',
        value: '100'
      },
      {
        label: '200',
        value: '200'
      }
    ],
  },
  {
    id: 9,
    ask: '94 rounded off to the nearest 10 is..',
    answer: '90',
    name: 'q9',
    choices: [
      {
        label: '100',
        value: '100'
      },
      {
        label: '94',
        value: '94'
      },
      {
        label: '90',
        value: '90'
      }
    ],
  },
  {
    id: 10,
    ask: '165 rounded off to the nearest 10 is..',
    answer: '170',
    name: 'q10',
    choices: [
      {
        label: '160',
        value: '160'
      },
      {
        label: '170',
        value: '170'
      },
      {
        label: '150',
        value: '150'
      }
    ],
  },
  {
    id: 11,
    ask: '445 rounded off to the nearest 10 is..',
    answer: '450',
    name: 'q11',
    choices: [
      {
        label: '450',
        value: '450'
      },
      {
        label: '440',
        value: '440'
      },
      {
        label: '500',
        value: '500'
      }
    ],
  },
  {
    id: 12,
    ask: '999 rounded off to the nearest 10 is..',
    answer: '1,000',
    name: 'q12',
    choices: [
      {
        label: '990',
        value: '990'
      },
      {
        label: '1,000',
        value: '1,000'
      },
      {
        label: '909',
        value: '909'
      }
    ],
  }
]

const state = ref({
  name: ''
})

const validate = (state: any): FormError[] => {
  const errors = []
  if (!state.name) errors.push({ path: 'name', message: 'Required' })
  return errors
}

async function onSubmit(event: FormSubmitEvent<any>) {

  if (formStatus.value == 0){
    calculateScore(event.data)
  }

  formStatus.value = 1
}

async function onError(event: FormErrorEvent) {
  const element = document.getElementById(event.errors[0].id)
  element?.focus()
  element?.scrollIntoView({ behavior: 'smooth', block: 'center' })
}

function calculateScore(data) {
  console.log('here')
  Object.keys(data).forEach(function (key) {

    if (key === 'name') { return }

    let qKey = key.substring(1, 3).trim();

    var qDiv = document.getElementById(key)

    qDiv.classList.add("border-2");

    if (questions[qKey - 1].answer === data[key]) {
      qDiv.classList.add("border-green-500");
      score.value++
    }
    else {
      qDiv.classList.add("border-red-500");
    }

  });


}

function resetForm() {
  score.value = 0
  formStatus.value = 0

  for (let i = 1; i <= 12; i++) {
    document.querySelector('[id="q'+i+'"]').classList.remove("border-green-500");
    document.querySelector('[id="q'+i+'"]').classList.remove("border-red-500");
    document.querySelector('[id="q'+i+'"]').classList.remove("border-2");
  }
  
}
</script>

<template>
  <UContainer>
    <div>
      <NuxtRouteAnnouncer />
      <!--<NuxtWelcome />-->
    </div>
    <div class="grid grid-cols-5 justify-center mt-5 p-4 py-8 border border-solid border-gray-300 rounded-md bg-white ">
      <div class="col-span-5 lg:col-start-2 lg:col-span-3 bg-gray-200 py-3 px-6 rounded-full mb-6">
        <h1 class="font-sans text-lg md:text-2xl font-normal text-center ">{{ sheetHeader }}</h1>
      </div>

      <div class="col-span-5 lg:col-start-2 lg:col-span-3">
        <UForm :validate="validate" :state="state" @submit="onSubmit" @error="onError">
          <UFormGroup name="name" :ui="{ error: 'text-right mt-0' }" eager-validation class="w-full lg:w-1/2 items-center justify-center">
            <div class="flex flex-wrap items-center justify-center">
              <label class="tracking-wide font-medium items-center mr-3" for="name">
                Name
              </label>
              <input name="name" v-model="state.name"
                class="grow bg-transparent placeholder:text-slate-400 text-slate-700 border border-slate-200 rounded-lg px-3 py-2 transition duration-300 ease focus:outline-none focus:border-blue-400 hover:border-slate-300 shadow-sm focus:shadow"
                placeholder="Your name here.." autocomplete="off">
            </div>
          </UFormGroup>
          <h2 class="font-sans text-xl font-normal text-center my-5">Click the correct answers.</h2>
          <div class="w-full grid grid-cols-2 gap-1">
            <Question v-for="(question, key) in questions" :key="key" :question="question"
              v-model="state[question.name]" class="col-span-5 md:col-span-1 lg:col-span-1" /> <!--:question="question"-->
            <div class="w-full place-content-end col-span-2 text-right mt-5">
              <span class="text-2xl font-semibold">Your score is : {{ score }}</span>
            </div>
          </div>
          <div class="flex justify-end mt-5">
            <UButton type="submit" class="mr-2 text-base">
              Submit
            </UButton>
            <UButton type="reset" color="gray" variant="solid" @click="resetForm" class="text-base">Reset</UButton>
          </div>
        </UForm>
      </div>
    </div>
  </UContainer>
</template>