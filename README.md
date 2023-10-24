# Reproduction JsonForms Vuetify3 Select Issue

This repoository is a reproduction scenario for an issue when using JsonForms with the Vuetify3 adapter.

The following issue happens: Changes of a select field are not captured in the onchange event of the `<json-forms>` element.

## Running the example locally

1. Navigate to `app` folder
2. Run `npm ci`
3. Run `npm run dev`
4. Open browser and navigate to `http://localhost:3000`

## Observable behaviour

The value of the `data` object that is passed in the `onchange` event parameter is printed underneath the form. It contains all form data, except the one from the select field. 
