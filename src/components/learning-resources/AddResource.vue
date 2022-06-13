<template>
    <base-dialog v-if="!isValid" title="Invalid input" @closeModal="closeDialog">
        <template #default>
            <p>Please provide the required data!</p>
        </template>
        <template #actions>
            <base-button title="Okay" @click="closeDialog"></base-button>
        </template>
    </base-dialog>
    <base-card>
        <form @submit="addResource">
            <div class="form-control">
                <label for="title">Title</label>
                <input type="text" id="title" ref="title">
            </div>
            <div class="form-control">
                <label for="description">Description</label>
                <textarea name="description" id="description" rows="3" ref="description"></textarea>
            </div>
            <div class="form-control">
                <label for="link">Link</label>
                <input type="url" id="link" ref="link">
            </div>
            <div>
                <base-button type="submit" title="Add resource"></base-button>
            </div>
        </form>
    </base-card>
</template>
<script>
export default {
    inject: ['addMyResource'],
    data() {
        return {
            isValid: true
        }
    },
    methods: {
        addResource(e) {
            e.preventDefault();
            const resource = {
                id: this.$refs.title.value,
                title: this.$refs.title.value,
                description: this.$refs.description.value,
                link: this.$refs.link.value
            };

            if (resource.id === "" || resource.title === '' || resource.description === '' || resource.link === '') {
                this.isValid = false;
                return;
            } else {
                this.addMyResource(resource);
            }
        },
        closeDialog() {
            this.isValid = true;
        }
    }
}
</script>


<style>
label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
}

input,
textarea {
    display: block;
    width: 100%;
    font: inherit;
    padding: 0.15rem;
    border: 1px solid #ccc;
}

input:focus,
textarea:focus {
    outline: none;
    border-color: #3a0061;
    background-color: #f7ebff;
}

.form-control {
    margin: 1rem 0;
}
</style>