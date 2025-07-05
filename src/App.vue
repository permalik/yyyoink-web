<script setup>
import Button from "primevue/button";
import {Field, Form, ErrorMessage} from "vee-validate";
import {toTypedSchema} from "@vee-validate/zod";
import * as zod from "zod";

const textareaSchema = toTypedSchema(
    zod.object({
      body : zod.string().min(5, {message: "Prompt is required."}),
    })
);

async function createPrompt(payload) {
  const res = await fetch("http://localhost:5166/turn", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(payload),
  });

  const data = await res.json();
  console.log(data);
};

async function onSubmit(values) {
  alert(JSON.stringify(values, null, 2));
  await createPrompt(values);
}
</script>

<template>
  <main>
    <div>
      yyyoink
    </div>
    <Form :validation-schema="textareaSchema" @submit="onSubmit" class="flex-col">
      <div class="flex-col">
        <Field as="textarea" name="body" id="body" col="50" rows="10" class="w-92 bg-stone-700"/>
        <ErrorMessage name="body"/>
      </div>
      <Button type="submit" label="Submit"/>
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