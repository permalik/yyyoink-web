<script setup>
import Button from "primevue/button";
import {Field, Form, ErrorMessage} from "vee-validate";
import {toTypedSchema} from "@vee-validate/zod";
import * as zod from "zod";

const textareaSchema = toTypedSchema(
    zod.object({
      prompt: zod.string().min(5, {message: "Prompt is required."}),
    })
);

function onSubmit(values) {
  alert(JSON.stringify(values, null, 2));
}
</script>

<template>
  <main>
    <div>
      yyyoink
    </div>
    <Form :validation-schema="textareaSchema" @submit="onSubmit" class="flex-col">
      <div>
        <Field as="textarea" name="prompt" id="prompt" col="50" rows="10" class="w-92 bg-stone-700"/>
        <ErrorMessage name="prompt"/>
      </div>
      <Button>Submit</Button>
    </Form>
  </main>
</template>

<style scoped>
main {
  display: flex;
  flex-flow: column nowrap;
  place-items: center;
}
</style>