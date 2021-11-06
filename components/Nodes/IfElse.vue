<template>
  <div>
    <h1 class="mb-2 font-bold">If - Else</h1>
    <label class="flex items-center mt-2">
      <span class="mr-2">If</span>
      <input
        type="text"
        class="
          shadow
          appearance-none
          border
          rounded
          w-16
          py-2
          px-3
          mr-2
          text-gray-700
          leading-tight
          bg-blue-100
          focus:outline-none focus:shadow-outline
        "
      />
      <select class="form-select block text-black">
        <option>==</option>
        <option>></option>
        <option>>=</option>
        <option>'&lt;'</option>
        <option>'&lt;'=</option>
      </select>
      <input
        type="text"
        class="
          shadow
          appearance-none
          border
          rounded
          w-16
          py-2
          px-3
          ml-2
          text-gray-700
          leading-tight
          bg-blue-100
          focus:outline-none focus:shadow-outline
        "
      />
    </label>
    <p class="text-right mt-2">Else</p>
  </div>
</template>

<script>
export default {
  methods: {},
};
</script>
