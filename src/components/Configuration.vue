<script setup>
import { ref } from 'vue'
import draggable from 'vuedraggable'
import AddonItem from './AddonItem.vue'
import Authentication from './Authentication.vue'

const stremioAPIBase = "https://api.strem.io/api/"
const dragging = false
let stremioAuthKey = ref('');
let addons = ref([])
let addonsLoaded = ref(false)
let loadAddonsButtonText = ref('Load Addons')

function loadUserAddons() {
    const key = stremioAuthKey.value
    if (!key) {
        console.error('No auth key provided')
        return
    }

    loadAddonsButtonText.value = 'Loading...'
    console.log('Loading addons...')

    const url = `${stremioAPIBase}addonCollectionGet`
    fetch(url, {
        method: 'POST',
        body: JSON.stringify({
            type: 'AddonCollectionGet',
            authKey: key,
            update: true,
        })
    }).then((resp) => {
        resp.json().then((data) => {
            console.log(data)
            if (!("result" in data) || data.result == null) {
                console.error("Failed to fetch user addons: ", data)
                alert('Failed to fetch user addons - are you sure you pasted the correct Stremio AuthKey?')
                return
            }
            addons.value = Array.isArray(data.result.addons) ? data.result.addons : []
            addonsLoaded.value = true
        })
    }).catch((error) => {
        console.error('Error fetching user addons', error)
    }).finally(() => {
        loadAddonsButtonText.value = 'Load Addons'
    })
}

function syncUserAddons() {
    const key = stremioAuthKey.value
    if (!key) {
        console.error('No auth key provided')
        return
    }
    if (!addonsLoaded.value) {
        // The addon list starts out empty, so syncing before "Load Addons" would
        // overwrite the Stremio account's addons with an empty collection.
        alert('Please click "Load Addons" first - syncing now would overwrite your Stremio addons with an empty list.')
        return
    }

    console.log('Syncing addons...')

    const url = `${stremioAPIBase}addonCollectionSet`
    fetch(url, {
        method: 'POST',
        body: JSON.stringify({
            type: 'AddonCollectionSet',
            authKey: key,
            addons: addons.value,
        })
    }).then((resp) => {
        resp.json().then((data) => {
            if (!("result" in data) || data.result == null) {
                console.error("Sync failed: ", data)
                alert('Sync failed if unknown error')
                return
            } else if (!data.result.success) {
                alert("Failed to sync addons: " + data.result.error)
            } else {
                console.log("Sync complete: + ", data)
                alert('Sync complete!')
            }
        })
    }).catch((error) => {
        alert("Error syncing addons: " + error)
        console.error('Error fetching user addons', error)
    })
}

function removeAddon(idx) {
    addons.value.splice(idx, 1)
}

function getNestedObjectProperty(obj, path, defaultValue = null) {
    try {
        return path.split('.').reduce((acc, part) => acc && acc[part], obj)
    } catch (e) {
        return defaultValue
    }
}

function setAuthKey(authKey) {
    stremioAuthKey.value = authKey
    // A new auth key means a different account/session: require a fresh load before syncing
    addons.value = []
    addonsLoaded.value = false
    console.log('AuthKey set to: ', stremioAuthKey.value)
}


</script>

<template>
    <section id="configure">
        <h2>Configure</h2>
        <form onsubmit="return false;">
            <fieldset>
                <Authentication :stremioAPIBase="stremioAPIBase" @auth-key="setAuthKey" />
            </fieldset>
            <fieldset id="form_step1">
                <legend>Step 1: Load Addons</legend>
                <button class="button primary" @click="loadUserAddons">
                    {{ loadAddonsButtonText }}
                </button>
            </fieldset>
            <fieldset id="form_step2">
                <legend>Step 2: Re-Order Addons</legend>
                <draggable :list="addons" item-key="transportUrl" class="sortable-list" ghost-class="ghost"
                    @start="dragging = true" @end="dragging = false">
                    <template #item="{ element, index }">
                        <AddonItem :name="element.manifest.name" :idx="index" :manifestURL="element.transportUrl"
                            :logoURL="element.manifest.logo"
                            :isDeletable="!getNestedObjectProperty(element, 'flags.protected', false)"
                            :isConfigurable="getNestedObjectProperty(element, 'manifest.behaviorHints.configurable', false)"
                            @delete-addon="removeAddon" />
                    </template>
                </draggable>
            </fieldset>
            <fieldset id="form_step3">
                <legend>Step 3: Sync Addons</legend>
                <button type="button" class="button primary icon" :disabled="!addonsLoaded" @click="syncUserAddons">Sync to Stremio
                    <img src="https://icongr.am/feather/loader.svg?size=16&amp;color=ffffff" alt="icon">
                </button>
                <p v-if="!addonsLoaded">Load your addons in step 1 before syncing.</p>
            </fieldset>
        </form>

    </section>
</template>

<style scoped>
/* sortable list/addon list specifics */
.sortable-list {
    padding: 25px;
    border-radius: 7px;
    padding: 30px 25px 20px;
    box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
}

.item.dragging {
    opacity: 0.6;
}

.item.dragging :where(.details, i) {
    opacity: 0;
}
</style>
