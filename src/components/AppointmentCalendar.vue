<script setup lang="ts">
import { reactive, watch } from "vue";

import "@fullcalendar/core/vdom";
import FullCalendar from "@fullcalendar/vue3";
import dayGridPlugin from "@fullcalendar/daygrid";

import { collection } from "@firebase/firestore";
import { firestore } from "@/plugins/firebase";
import { useCollection } from "vuefire";

const appointments = useCollection(collection(firestore, "appointment"));

const calendarOptions = reactive<{
  plugins: any[];
  initialView: string;
  events: Object[];
}>({
  plugins: [dayGridPlugin],
  initialView: "dayGridMonth",
  events: [],
});

watch(appointments, (value) => {
  calendarOptions.events = value.map((appointment) => ({
    title: appointment.description,
    date: appointment.date,
  }));
});
</script>

<template>
  <FullCalendar :options="calendarOptions" />
</template>
