<template>
  <div>
    <h1 class="mb-2 font-bold">If - Else</h1>
    <label class="flex items-center mt-2">
      <span>If</span>
      <input
        type="text"
        class="
          shadow
          appearance-none
          border
          rounded
          w-full
          py-2
          px-3
          text-gray-700
          leading-tight
          bg-blue-100
          focus:outline-none focus:shadow-outline
        "
      />
      <select class="form-select block">
        <option>==</option>
        <option>></option>
        <option>>=</option>
        <option>{<}</option>
        <option>{<=}</option>
      </select>
      <input
        type="text"
        class="
          shadow
          appearance-none
          border
          rounded
          w-full
          py-2
          px-3
          text-gray-700
          leading-tight
          bg-blue-100
          focus:outline-none focus:shadow-outline
        "
      />
    </label>
  </div>
</template>

<script>
export default {
  methods: {},
};
</script>
