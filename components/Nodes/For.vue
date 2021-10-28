<template>
  <div>
    <h1 class="mb-2 font-bold">For Bucle</h1>
    <label class="flex items-center mt-2">
      <span class="mr-2">For ( i=0 ; i</span>
      <select class="form-select block text-black w-18">
        <option>==</option>
        <option>></option>
        <option>>=</option>
        <option><</option>
        <option><=</option>
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
          mx-2
          text-gray-700
          leading-tight
          bg-blue-100
          focus:outline-none focus:shadow-outline
        "
      />
      <span>;</span>
      <select class="form-select block text-black w-18 mx-2">
        <option>i++</option>
        <option>i--</option>
      </select>
      <span>)</span>
    </label>
  </div>
</template>

<script>
export default {
  methods: {},
};
</script>
