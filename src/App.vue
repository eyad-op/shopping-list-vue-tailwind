<template>
  <div
    class="font-mono flex flex-col mt-32 max-w-3xl m-auto flex-wrap shadow-xl p-4 rounded-md"
  >
    <h1 class="text-3xl text-gray-700 font-extrabold">
      Welcome to your shopping list for
      <span class="text-orange-400">{{ date }}</span>
    </h1>
    <form
      @submit.prevent="setItem"
      class="w-full mt-8 flex justify-center flex-wrap gap-2"
    >
      <input
        class="py-2 px-3 bg-green-100 w-2/3 text-xl rounded-md grow border-none outline-none focus:bg-yellow-200"
        type="text"
        placeholder="Add an item"
        v-model="newItem"
      />
      <label
        class="px-2 flex items-center text-lg rounded-md font-bold"
        for="important"
        :class="[
          itemPriority
            ? 'bg-orange-500 text-white'
            : 'bg-orange-100 text-gray-600 ',
        ]"
      >
        <input
          class="hidden"
          type="checkbox"
          v-model="itemPriority"
          id="important"
        />
        Important!
      </label>
      <button
        class="px-2 text-white bg-green-500 hover:bg-green-400 rounded-md ease-in-out duration-300 font-bold"
      >
        ADD ITEM
      </button>
    </form>
    <p
      v-if="!itemsList.length"
      class="text-xl text-gray-500 font-bold mt-4 italic"
    >
      Start adding your items
      <span class="text-xs text-gray-400"
        >click on important button to mark as important</span
      >
    </p>
    <p v-if="emptyItem" class="text-2xl text-red-600 font-bold mt-3 italic">
      Item cannot be empty
    </p>
    <ListOfItems
      :listItems="itemsListReversed"
      @deleteItem="deleteFromList"
      @check="setPurchased"
    />
  </div>
</template>

<script>
import ListOfItems from "@/components/ListOfItems.vue";
export default {
  name: "App",
  components: {
    ListOfItems,
  },

  data() {
    return {
      itemsList: [
        // dummy data
        // { id: 1, label: "First item", purchased: true, highPriority: true },
        // { id: 2, label: "Second item", purchased: true, highPriority: false },
        // { id: 3, label: "Third item", purchased: false, highPriority: true },
        // { id: 4, label: "Fourth item", purchased: false, highPriority: false },
      ],
      newItem: "",
      itemPriority: false,
      emptyItem: false,
      date: new Date().toLocaleDateString(),
    };
  },
  methods: {
    setPurchased(item) {
      item.purchased = !item.purchased;
    },
    setItem() {
      if (this.newItem.length != 0) {
        this.itemsList.push({
          id: this.itemsList.length + 1,
          label: this.newItem,
          purchased: false,
          highPriority: this.itemPriority,
        });
        this.newItem = "";
        this.itemPriority = "";
      } else {
        this.emptyItem = true;
        setTimeout(() => (this.emptyItem = false), 1000);
      }
    },
    deleteFromList(item) {
      this.itemsList = this.itemsList.filter((listItem) => listItem != item);
    },
  },
  computed: {
    itemsListReversed() {
      return [...this.itemsList].reverse();
    },
  },
};
</script>
