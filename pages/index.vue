<script setup>
const isLoggedIn = ref(false)

onMounted(async () => {
  if (!localStorage.getItem('SinkSiteToken'))
    return
  try {
    await useAPI('/api/verify')
    isLoggedIn.value = true
  }
  catch {
    isLoggedIn.value = false
  }
})
</script>

<template>
  <main class="flex items-center justify-center h-full">
    <template v-if="isLoggedIn">
      <NuxtLink to="/dashboard">
        <Button size="lg">
          Dashboard
        </Button>
      </NuxtLink>
    </template>
    <template v-else>
      <Login />
    </template>
  </main>
</template>
