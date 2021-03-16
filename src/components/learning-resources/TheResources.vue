<template>
    <base-card>
        <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Stored Resources </base-button>
        <base-button @click="setSelectedTab('add-resources')" :mode="addResButtonMode">Add Resources </base-button>
    </base-card>
    <component :is="selectedTab">

    </component>
</template>

<script>
    import StoredResources from '../stored-resources/StoredResources';
    import AddResources from './AddResources';

    export default {
        components: {
            StoredResources,
            AddResources
        },
        computed: {
            storedResButtonMode() {
                return this.selectedTab === 'stored-resources' ? null : 'flat';
            },
            addResButtonMode() {
                return this.selectedTab === 'add-resources' ? null : 'flat'
            }
        },
        data() {
            return {
                selectedTab: 'stored-resources',
                storedResources: [
                {
                    id: 'official-guide',
                    title: 'Official Guide',
                    description: 'Official Vue.js documentation',
                    link: 'vue-js.org'
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'You need to know how to google ',
                    link: 'google.com'
                }
            ]
        }
        },
        provide() {
            return {
                resources: this.storedResources
            }
        },
        methods: {
            setSelectedTab(tab) {
                this.selectedTab = tab;
            }
        }
    }
</script>
