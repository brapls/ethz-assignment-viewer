<!-- Copyright 2023 Ziad Malik -->

<template>
    <!-- @vue-ignore -->
    <div v-for="lecture in Object.keys(lecturesToAssignments)" class="py-4 space-y-4">
        <span class="px-2 text-xl font-semibold text-primary-500">{{ lecture }}</span>
        <div class="flex gap-2 px-2">
            <!-- @vue-ignore -->
            <UButton color="gray" icon="i-heroicons-globe-alt" label="Website" :to="lecturesToAssignments[lecture].website" target="_blank" />
            <!-- @vue-ignore -->
            <UButton color="gray" icon="i-heroicons-video-camera" label="Video Lectures" :to="lecturesToAssignments[lecture].video" target="_blank" />
            <!-- @vue-ignore -->
            <UButton color="gray" icon="i-heroicons-video-camera" label="VVZ" :to="lecturesToAssignments[lecture].vvz" target="_blank" />
        </div>
        <div class="flex gap-3 overflow-auto px-2 py-2">
            <!-- @vue-ignore -->
            <AssignmentCard v-for="assignment in lecturesToAssignments[lecture].exercises" :assignment="assignment" />
        </div>
    </div>
</template>

<script setup lang="ts">
const { data: lecturesToAssignments } = await useFetch("/api/assignments", {
    transform: (data) => {
        const obj = data;
        Object.keys(data).forEach((key) => {
            // @ts-ignore
            obj[key].exercises = obj[key].exercises.reverse();
        });

        return obj;
    },
});
</script>
