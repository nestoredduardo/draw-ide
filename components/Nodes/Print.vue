<template>
  <div class="w-52">
    <h1 class="mb-2 font-bold">Print</h1>
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
    <label class="flex items-center mt-2">
      <input
        type="checkbox"
        class="form-checkbox text-pink-600 border-pink-300 border-2"
      />
      <span class="ml-2 mr-4">Insert line break</span>
      <input
        type="checkbox"
        class="form-checkbox text-pink-600 border-pink-300 border-2"
      />
      <span class="ml-2">Is variable</span>
    </label>
  </div>
</template>

<script>
export default {
  methods: {},
};
</script>
