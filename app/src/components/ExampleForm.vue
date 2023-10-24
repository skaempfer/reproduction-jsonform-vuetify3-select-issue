<template>
  <json-forms
    :data="{}"
    :schema="schema"
    :uischema="uischema"
    :renderers="renderers"
    @change="onChange"
    />
  <div>
    {{ form }}
  </div>
</template>

<script setup lang="ts">
  import { ref, Ref } from 'vue';
  import { JsonSchema, UISchemaElement } from '@jsonforms/core';
  import { JsonForms } from '@jsonforms/vue';
  import { vuetifyRenderers } from '@jsonforms/vue-vuetify';

  const renderers = Object.freeze([
    ...vuetifyRenderers,
    // here you can add custom renderers
  ]);

  const data: Ref<any> = ref(null);
  const schema: Ref<JsonSchema | undefined> = ref(undefined);
  const uischema: Ref<UISchemaElement | undefined> = ref(undefined);

  const form = ref({});

  function onChange(event: any) {
    form.value = event.data;
  }

  schema.value = {
    "type": "object",
    "properties": {
      "name": {
        "type": "string",
        "minLength": 3,
        "description": "Please enter your name"
      },
      "vegetarian": {
        "type": "boolean"
      },
      "birthDate": {
        "type": "string",
        "format": "date"
      },
      "nationality": {
        "type": "string",
        "enum": [
          "DE",
          "IT",
          "JP",
          "US",
          "RU",
          "Other"
        ]
      },
      "personalData": {
        "type": "object",
        "properties": {
          "age": {
            "type": "integer",
            "description": "Please enter your age."
          },
          "height": {
            "type": "number"
          },
          "drivingSkill": {
            "type": "number",
            "maximum": 10,
            "minimum": 1,
            "default": 7
          }
        },
        "required": [
          "age",
          "height"
        ]
      },
      "occupation": {
        "type": "string"
      },
      "postalCode": {
        "type": "string",
        "maxLength": 5
      }
    },
    "required": [
      "occupation",
      "nationality"
    ]
  };

  uischema.value = {
    "type": "VerticalLayout",
    "elements": [
      {
        "type": "HorizontalLayout",
        "elements": [
          {
            "type": "Control",
            "scope": "#/properties/name"
          },
          {
            "type": "Control",
            "scope": "#/properties/personalData/properties/age"
          },
          {
            "type": "Control",
            "scope": "#/properties/birthDate"
          }
        ]
      },
      {
        "type": "Label",
        "text": "Additional Information"
      },
      {
        "type": "HorizontalLayout",
        "elements": [
          {
            "type": "Control",
            "scope": "#/properties/personalData/properties/height"
          },
          {
            "type": "Control",
            "scope": "#/properties/nationality"
          },
          {
            "type": "Control",
            "scope": "#/properties/occupation",
            "suggestion": [
              "Accountant",
              "Engineer",
              "Freelancer",
              "Journalism",
              "Physician",
              "Student",
              "Teacher",
              "Other"
            ]
          }
        ]
      }
    ]
  } as any;

  data.value = {};
</script>
