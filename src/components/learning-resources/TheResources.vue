<template>
    <base-card>
        <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Stored Resources </base-button>
        <base-button @click="setSelectedTab('add-resources')" :mode="addResButtonMode">Add Resources </base-button>
    </base-card>
    <keep-alive>
        <component :is="selectedTab"></component>
    </keep-alive>
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
                resources: this.storedResources,
                addResources: this.addResources,
                deleteResource: this.removeResources
            }
        },
        methods: {
            setSelectedTab(tab) {
                this.selectedTab = tab;
            },
            addResources(title, description, url) {
                const newResource = {
                    id: new Date().toISOString(),
                    title: title,
                    description: description,
                    link: url
                }
                this.storedResources.push(newResource);
                this.selectedTab = 'stored-resources'
            },
            removeResources(resId) {
                const resourseIdx = this.storedResources.findIndex(res => res.id === resId);
                this.storedResources.splice(resourseIdx, 1);
            }
        }
    }
</script>
