<script setup>

defineProps(['question'])

const selected = ref('')


</script>

<template>
    <div class="transition ease-in-out delay-0 border border-solid border-gray-300 rounded-md p-4" :id="question.name">
        <p class="text-base">{{ question.ask }}</p>
        <UFormGroup :name="question.name">
            <URadioGroup :name="question.name" color="blue"
            v-model="selected" 
            :options="question.choices" 
            @input="$emit('update:modelValue', $event.target.value)" 
            :uiRadio="{ label: 'text-base hover:cursor-pointer text-black font-normal', container : 'ml-2', wrapper : 'mt-1' }" :ui="{}">
                <template #label="{ option }">
                    <p>
                        {{ option.label }}
                    </p>
                </template>
            </URadioGroup>
        </UFormGroup>
        <!-- Answer picked : {{ selected }} -->
    </div>

</template>