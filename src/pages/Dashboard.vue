<template>
    <div class="content">
        <div style="margin-bottom: 1rem">
            <span>local url: </span>
            <input
                v-model.trim.lazy="localUrl"
                placeholder="Advise url"
                type="text"
            />
            <input
                v-model.trim.lazy="apiToken"
                placeholder="token"
                type="text"
            />
        </div>
        
        <div style="display: flex; gap: 1rem; margin-bottom: 1rem;">
            <button
                v-for="route in routes"
                class="button"
                @click="navigateIframe(route.name)"
            >
                {{ route.text }}
            </button>
        </div>
        
        <button @click="getApiToken()">
            Refresh token
        </button>
        
        <iframe
            :src="adviceUrl"
            id="adviesIframe"
            :height="height"
            :style="`overflow:hidden;width:100%; height:${height}`"
            width="100%"
            frameborder="0"
        >
        </iframe>
        
        <div class="side-bar">
            <div style="margin-bottom: 1rem">
                <span>local url: </span>
                <input
                    v-model.trim.lazy="sidebarUrl"
                    placeholder="Sidebar url"
                    type="text"
                    style="width: 100%"
                >
            </div>
            
            <iframe
                :src="sidebarUrl"
                frameborder="0"
                style="overflow:hidden;width:100%"
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
    import axios from 'axios';
    
    export default {
        components: {},
        
        mounted() {
            this.getApiToken();
            
            window.addEventListener('message', (event) => {
                if (event.data === 'toHome') {
                    window.alert('triggert from parent');
                    console.log(event.data);
                    // Handle event
                }
            });
            
            window.addEventListener('message', (event) => {
                if (event.data.type === 'action') {
                    console.log(event.data.state);
                    console.log(event.data);
                    // Handle event
                }
            });
            
            window.addEventListener('message', (event) => {
                if (event.data.type === 'resizeEvent') {
                    console.log(event.data.state);
                    this.height = event.data?.state?.height ?? '87vh';
                }
            });
            
            return {};
        },
        
        data() {
            return {
                localUrl: 'https://adpi.local.adpi.cloud/extern/advies?project-id=85',
                sidebarUrl: 'https://adpi.local.adpi.cloud/extern/klant-documenten/verwerk?project-id=41',
                customerProfileUrl: 'https://adpi.local.adpi.cloud/extern/klantomgeving/profiel',
                apiToken: '',
                height: '87vh',
                routes: [
                    {
                        "name": "employee.project.advice.show",
                        "text": "Inventarisatie"
                    },
                    {
                        "name": "employee.projects.advice.customerprofile",
                        "text": "Klantprofiel"
                    },
                    {
                        "name": "employee.projects.advice.compare_mortgage_rate",
                        "text": "Rentevergelijker"
                    },
                    {
                        "name": "employee.projects.advice.maxmortgage",
                        "text": "Max"
                    },
                    {
                        "name": "employee.projects.advice.financeplan",
                        "text": "Financieringsopzet"
                    },
                    {
                        "name": "employee.projects.advice.comparisons",
                        "text": "Vergelijken"
                    },
                    {
                        "name": "employee.projects.advice.proposals",
                        "text": "Voorstellen"
                    },
                    {
                        "name": "employee.project.advice.risks.death",
                        "text": "Risico's"
                    },
                    {
                        "name": "employee.projects.advice.reports",
                        "text": "Rapportage"
                    },
                    {
                        "name": "employee.projects.advice.applications",
                        "text": "Aanvragen"
                    }
                ]
            };
        },
        
        methods: {
            async getApiToken() {
                const options = {
                    method: 'GET',
                    url: 'https://adpi.local.adpi.cloud/api/v1/offices/1b96778d-6c20-11ee-928a-0242ac160004/token',
                    headers: { Authorization: 'Bearer 2|2hrrejT75goH9IhYlz9mKVuj6eqk7UYvXGR91sG4' },
                };
                
                try {
                    const { data } = await axios.request(options);
                    console.log('data', data);
                    this.apiToken = data.token;
                    console.log(data);
                } catch (error) {
                    console.error(error);
                }
            },
            
            navigateIframe(routeName) {
                const iframe = document.querySelector('#adviesIframe');
                const iframeWindow = iframe.contentWindow;
                
                const message = {
                    type: 'navigate',
                    name: routeName,
                    projectId: 7,
                };
                
                iframeWindow.postMessage(message, '*');
            },
        },
        computed: {
            adviceUrl() {
                if (!this.apiToken) {
                    return `${this.localUrl}`;
                }
                
                return `${this.localUrl}&token=${this.apiToken}`;
            },
        },
    };
</script>

<style
    lang="scss"
    scoped
>
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
