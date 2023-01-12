<template>
    <div class="content">
        <div style="margin-bottom: 1rem">
            <span>local url: </span>
            <input
                    v-model.trim.lazy="localUrl"
                    placeholder="Project ID"
                    type="text"
            >

            <span>  -  </span>

            <span>project-id: </span>

            <input
                    v-model.trim.lazy.number="projectId"
                    placeholder="Project ID"
                    type="number"
            >

            <span>  -  </span>

            <span>Constructed Iframe url: </span>
            <span>
              <strong>{{ localUrl + '/extern/advies?project-id=' + projectId }}</strong>
          </span>
        </div>

        <iframe :src="localUrl+'/extern/advies?project-id='+projectId"
                frameborder="0"
                height="100%"
                style="overflow:hidden;height:87vh;width:100%"
                width="100%"
        >
        </iframe>

        <div
                class="sidebar"
        >
            <iframe :src="localUrl+'/extern/klant-documenten/verwerk?project-id='+projectId"
                    frameborder="0"
                    height="100%"
                    style="overflow:hidden;height:87vh;width:100%"
                    width="100%"
            >
            </iframe>
        </div>
    </div>
</template>

<script>

    export default {
        components: {},
        data() {
            return {
                localUrl: 'https://adpi.local.adpi.cloud',
                projectId: 7
            };
        },
    };
</script>

<style lang="scss" scoped>
    .sidebar {
      display: flex;
      flex: 0 0 33.33333333%;
      max-width: 33.33333333%;
    }
</style>
