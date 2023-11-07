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

        <button 
            @click="navigateIframe"
            class="button"
        >
            naar Overlijden
        </button>

        <iframe 
            :src="localUrl"
            id="adviesIframe"
            height="100%"
            style="overflow:hidden;height:87vh;width:100%"
            width="100%"
            frameborder="0"
        >
        </iframe>

        <div
            class="side-bar"
        >
            <div
                style="margin-bottom: 1rem"
            >
                <span>local url: </span>
                <input
                        v-model.trim.lazy="sidebarUrl"
                        placeholder="Sidebar url"
                        type="text"
                        style="width: 100%"
                >
            </div>

            <iframe :src="sidebarUrl"
                    frameborder="0"
                    style="overflow:hidden;height:87vh;width:100%"
                    width="100%"
            >
            </iframe>
        </div>


<!--        <div-->
<!--                style="margin-top: 2rem"-->
<!--        >-->
<!--            <div-->
<!--                    style="margin-bottom: 1rem"-->
<!--            >-->
<!--                <span>local url: </span>-->
<!--                <input-->
<!--                        v-model.trim.lazy="customerProfileUrl"-->
<!--                        placeholder="Sidebar url"-->
<!--                        type="text"-->
<!--                        style="width: 100%"-->
<!--                >-->
<!--            </div>-->

<!--            <iframe :src="customerProfileUrl"-->
<!--                    frameborder="0"-->
<!--                    style="overflow:hidden;height:87vh;width:100%"-->
<!--                    width="100%"-->
<!--            >-->
<!--            </iframe>-->
<!--        </div>-->
    </div>
</template>

<script>
    export default {
        components: {},

        mounted() {
            window.addEventListener('message', (event) => {
                if(event.data === 'toHome') {
                    window.alert('triggert from parent')
                    console.log(event.data);
                   // Handle event
                }
            });

            return{

            }
        },

        data() {
            return {
                localUrl: 'https://adpi.local.adpi.cloud/extern/advies?project-id=7',
                sidebarUrl: 'https://adpi.local.adpi.cloud/extern/klant-documenten/verwerk?project-id=7',
                customerProfileUrl: 'https://adpi.local.adpi.cloud/extern/klantomgeving/profiel'
            };
        },

        methods: {
            navigateIframe() {
                const iframe = document.querySelector('#adviesIframe');
                const iframeWindow = iframe.contentWindow;

                const message = {
                    type: 'navigate',
                    url: '/kantooromgeving/projecten/7/advies/risicos/overlijden'
                };
            
                iframeWindow.postMessage(message, '*');
            }
        }
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

    .button {
        padding: 0.5rem;
        background-color: rgb(12, 12, 81);
        color: white;
        margin-bottom: 1rem;

        &:hover {
            cursor: pointer;
        }
    }
</style>
