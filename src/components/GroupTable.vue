<script setup lang="ts">
import type { Group } from '@/models/group';
import type { Team } from '@/models/team';

const props = defineProps<{
  group: Group;
  teams: Record<string, Team[]>;
}>();
const get_validated_team_by_id = (id: number) => props.teams.validated_teams.find((team) => team.id === id);

</script>
<template>
  <table :key="group.id" border="1" class="text-bold w-full table-fixed overflow-auto text-3xl">
    <thead class="w-full">
      <tr class="h-0 w-auto">
        <th align="center" class="w-4/6 bg-slate-400 text-black md:w-3/4"/>
        <th align="center" class="w-2/6 bg-slate-400 text-black md:w-1/4"/>
      </tr>
      <tr>
        <th colspan="2" class="bg-slate-400 p-3 text-black">
          {{ group.name }}
        </th>
      </tr>
      <tr class="w-auto">
        <th align="center" class="border-separate border border-slate-500 bg-slate-200 p-4 text-black">
          Equipe
        </th>
        <th align="center" class="m-4 border-separate truncate border border-slate-500 bg-slate-200 p-4 text-black">
          Score
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="team_id in group.teams" :key="team_id">
        <td align="center" class="border-separate truncate border border-slate-500 p-4">
          {{
            get_validated_team_by_id(team_id)?.name }}
        </td>
        <td align="center" class="border-separate border border-slate-500 p-4">
          {{ group.scores[team_id] }}
        </td>
      </tr>
    </tbody>
  </table>
</template>
