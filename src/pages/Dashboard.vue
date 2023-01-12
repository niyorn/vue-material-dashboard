<template>
    <div class="content">
        <div style="margin-bottom: 1rem">
            <span>local url: </span>
            <input
                    v-model.trim.lazy="localUrl"
                    placeholder="Advise url"
                    type="text"
            >
        </div>

        <iframe :src="localUrl"
                frameborder="0"
                height="100%"
                style="overflow:hidden;height:87vh;width:100%"
                width="100%"
        >
        </iframe>

        <div
                class="side-bar"
        >
            <span>local url: </span>
            <input
                    v-model.trim.lazy="sidebarUrl"
                    placeholder="Sidebar url"
                    type="text"
                    style="width: 100%"
            >

            <iframe :src="sidebarUrl"
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
                localUrl: 'https://adpi.local.adpi.cloud/extern/advies?project-id=7',
                sidebarUrl: 'https://adpi.local.adpi.cloud/extern/klant-documenten/verwerk?project-id=7'
            };
        },
    };
</script>

<style lang="scss" scoped>
    .side-bar {
      margin-top: 4rem;

      flex: 0 0 33.33333333%;
      max-width: 33.33333333%;
      margin-left: auto;
    }

    .content {
      input {
        width: 100%;
      }
    }
</style>
