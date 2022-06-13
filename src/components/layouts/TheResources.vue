<template>
    <base-card>
        <base-button @click="setSelectedTab('stored-resources')" title="Stored Resources"
            :mode="selectedTab === 'stored-resources' && 'flat'" />
        <base-button @click="setSelectedTab('add-resource')" title="Add Resource"
            :mode="selectedTab === 'add-resource' && 'flat'" />
    </base-card>
    <keep-alive>
        <component :is="selectedTab"></component>
    </keep-alive>
</template>

<script>
import StoredResources from '../learning-resources/StoredResources.vue';
import AddResource from '../learning-resources/AddResource.vue';

export default {
    components: {
        StoredResources,
        AddResource
    },
    data() {
        return {
            selectedTab: 'stored-resources',
            storedResources: [
                {
                    id: 'official-guide',
                    title: 'Official Guide',
                    description: 'The official VueJS documentation',
                    link: 'https://vuejs.org'
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'Learn to Google',
                    link: 'https://google.com'
                }
            ]
        }
    },
    provide() {
        return {
            resources: this.storedResources,
            addMyResource: this.addMyResource,
            deleteResource: this.deleteResource
        }
    },
    methods: {
        setSelectedTab(tab) {
            this.selectedTab = tab;
        },
        addMyResource(resource) {
            this.storedResources.unshift(resource);
            this.selectedTab = 'stored-resources';
        },
        deleteResource(resID) {
            const resIndex = this.storedResources.findIndex(res => res.id === resID);
            this.storedResources.splice(resIndex, 1);
        }
    }
}
</script>