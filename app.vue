<script setup lang="ts">
import {getSessionContext} from "@shopware-pwa/api-client";
import {SessionContext} from "@shopware-pwa/types";

useHead({
    title: "Agravis Stele",
    meta: [
        {name: "description", content: "Agravis Stele"},
        {'http-equiv': 'refresh', content: '1800'},
    ],
    htmlAttrs: {
        lang: "de",
    },
});

const {refreshSessionContext} = useSessionContext();
onBeforeMount(async () => {
    await refreshSessionContext();
});

const {apiInstance} = useShopwareContext();
const {data: sessionContextData} = await useAsyncData(
    "sessionContext",
    async () => {
        return await getSessionContext(apiInstance);
    }
);
useSessionContext(sessionContextData.value as SessionContext);

</script>

<template>
    <NuxtLayout>
        <NuxtPage/>
    </NuxtLayout>
</template>

<style>
body {

}
</style>
