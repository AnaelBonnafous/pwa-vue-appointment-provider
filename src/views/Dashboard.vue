<script setup lang="ts">
import { collection, query, where } from "@firebase/firestore";
import { firestore } from "@/plugins/firebase";
import { useCollection, useCurrentUser } from "vuefire";

const user = useCurrentUser();

const appointmentRef = collection(firestore, "appointment");
const appointments = useCollection(
  query(appointmentRef, where("provider_uid", "==", user.value?.uid))
);
</script>

<template>
  <h1>Dashboard</h1>

  <div class="mt-10">
    <p class="text-h6">Next appointments</p>
    <v-table>
      <thead>
        <tr>
          <th>Date</th>
          <th>Client</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="appointment in appointments">
          <td>{{ appointment.date }}</td>
          <td>{{ appointment.client_uid }}</td>
          <td>{{ appointment.description }}</td>
        </tr>
      </tbody>
    </v-table>
  </div>
</template>
