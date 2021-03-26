<template>
  <div>
    <button @click="currentPagePrev">Prev</button>

    {{ currentPage }} / {{ pageCount }}

    <button @click="currentPageNext">Next</button>
    <pdf
      :src="src"
      :page="currentPage"
      @num-pages="pageCount = $event"
      @page-loaded="currentPage = $event"
    ></pdf>
  </div>
</template>

<script>
import pdf from "vue-pdf";
var loadingTask = pdf.createLoadingTask("./sample.pdf");
export default {
  components: {
    pdf,
  },
  data() {
    return {
      src: loadingTask,
      numPages: undefined,
      currentPage: 1,
      pageCount: 0,
    };
  },
  mounted() {
    this.src.promise.then((pdf) => {
      this.numPages = pdf.numPages;
    });
  },
  methods: {
    currentPageNext() {
      if (this.pageCount > this.currentPage) {
        this.currentPage++;
      }
    },
    currentPagePrev() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
  },
};
</script>

<style></style>
