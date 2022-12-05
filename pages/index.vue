<template>
  <Form :initialValues="item" v-slot="{ values, setFieldValue }">
    {{ values }}
    <div style="display: flex">
      <div v-for="(c, i) in values.changed.added" :key="i" style="background: #eee; margin-right: 10px">
        <p>画像</p>
        <label>caption</label><br />
        <Field :name="`changed.added[${i}].caption`" v-slot="{ field }">
          <input v-bind="field" />
        </Field>
      </div>
    </div>
    <button type="button" @click="addItem(setFieldValue, values)">add</button>
    <button type="button" @click="deleteItem(setFieldValue)">delete</button>
  </Form>
</template>
<script setup>
import { Field, Form } from "vee-validate";

const item = ref(null);
item.value = {
  changed: { added: [], deleted: [] },
};

const addItem = (setFieldValue, values) => {
  const val = [
    ...values.changed.added,
    {
      image: "imageData",
      caption: "captionValue",
    },
  ];
  setFieldValue("changed", { added: val, deleted: [] });
};

const deleteItem = (setFieldValue) => {
  setFieldValue("changed", { added: [], deleted: [] });
};
</script>
