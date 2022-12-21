<template>
  <div class="content">
      <div style="margin-bottom: 1rem">
          <span>local url: </span>
          <input
              type="text"
              v-model.trim.lazy="localUrl"
              placeholder="Project ID"
          >

          <span>  -  </span>

          <span>project-id: </span>

          <input
              type="number"
              v-model.trim.lazy.number="projectId"
              placeholder="Project ID"
          >

          <span>  -  </span>

          <span>Constructed Iframe url: </span>
          <span>
              <strong>{{localUrl+'/extern/advies?project-id='+projectId}}</strong>
          </span>
      </div>

    <iframe :src="localUrl+'/extern/advies?project-id='+projectId"
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
        localUrl: 'https://adpi.local.adpi.cloud',
        projectId: 7
    };
  },
};
</script>
