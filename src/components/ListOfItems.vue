<template>
  <ul class="w-full text-left mt-4">
    <li
      v-for="item in listItems"
      :key="item.id"
      class="text-xl font-medium mt-2 px-2 py-1 hover:font-semibold hover:bg-lime-100 ease-in-out duration-300 flex justify-between items-center rounded-md"
    >
      <span
        class="cursor-pointer"
        @click="check(item)"
        :class="[
          [
            item.purchased && item.highPriority
              ? 'line-through opacity-50'
              : item.purchased
              ? 'line-through opacity-50'
              : '',
          ],
          [item.highPriority ? 'text-red-500' : ''],
        ]"
      >
        {{ item.label }}</span
      >

      <button
        @click="deleteItem(item)"
        class="px-2 font-bold text-orange-200 border-2 hover:border-orange-500 hover:text-orange-500 rounded-md"
      >
        X
      </button>
    </li>
  </ul>
</template>

<script>
export default {
  props: ["listItems"],
  methods: {
    deleteItem(item) {
      this.$emit("deleteItem", item);
    },
    check(item) {
      this.$emit("check", item);
    },
  },
};
</script>

<style></style>
