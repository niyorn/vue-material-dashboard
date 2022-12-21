<template>
  <div class="content">
      <div>
          <span>project-id: </span>

          <input
                  type="number"
                  v-model.trim.lazy.number="projectId"
                  placeholder="Project ID"
          >
      </div>

    <iframe :src="'https://adpi.local.adpi.cloud/extern/advies?project-id='+projectId"
      frameborder="0"
      width="100%"
      height="100%"
      style="overflow:hidden;height:87vh;width:100%"
      >
    </iframe>
  </div>
</template>

<script>
import {
  StatsCard,
  ChartCard,
  NavTabsCard,
  NavTabsTable,
  OrderedTable,
} from "@/components";

export default {
  components: {
  },
  data() {
    return {
        projectId: 7
    };
  },
};
</script>
