<template>
  <div class="overflow-x-auto p-5 ">
    <table class="min-w-full divide-y divide-gray-200">
      <thead class="border-b-2 border-black">
      <tr class="">
        <th scope="col" class="pl-4 py-3  text-left text-md font-medium   ">
          Team
        </th>
        <th scope="col" class=" py-3 text-left text-md font-medium   ">
          Day
        </th>
        <th scope="col" class="pl-14 py-3 text-left text-md font-medium   ">
          Time
        </th>
        <th scope="col" class=" py-3 text-left text-md font-medium   ">
          Hall
        </th>
      </tr>
      </thead>
      <tbody class="divide-y divide-gray-200">
      <tr v-for="(group, index) in groupedSchedule" :key="index" class="odd:bg-gray-200 even:bg-gray-100 ">
        <td class="  pl-4 text-sm font-bold text-gray-900">{{ group.team }}</td>
        <td class="   text-sm text-gray-900">
          <div v-for="(time, i) in group.times" :key="i" class="flex items-center space-x-2">
            <span
                class="py-2  flex-1"
                :class="{
                  'border-b border-gray-300': i === 0 && group.times.length > 1,
                  'last:border-0': i === group.times.length - 1,
                }"
            >
      {{ time.day }}
    </span>
          </div>
        </td>
        <td class="  text-sm text-gray-900 ">
          <div
              v-for="(time, i) in group.times"
              :key="i"
              class="flex space-x-1 py-2  "
              :class="{
      'border-b border-gray-300': i === 0 && group.times.length > 1, // Apply border to the first item if there are multiple entries
      'last:border-0': i === group.times.length - 1, // Remove border from the last item
    }"
          >
            <span class="bg-slate-600 text-white px-4 py-1 rounded-full">{{ time.startTime }}</span>
            <span>-</span>
            <span class="bg-slate-600 text-white px-4 py-1 rounded-full">{{ time.endTime }}</span>
          </div>
        </td>
        <td class="  text-sm text-gray-900">
          <div
              v-for="(time, i) in group.times"
              :key="i"
              :class="{
               'border-b border-gray-300 py-2': i === 0 && group.times.length > 1,
                'last:border-0 py-2': i === group.times.length - 1,
               }"
          >
            <span>{{ time.hall }}</span>
          </div>
        </td>

      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      schedule: [
        {team: 'U8 mix', day: 'Friday', startTime: '15:30', endTime: '16:45', hall: 'Deusterschule Kitzingen'},
        {team: 'U10 mix', day: 'Friday', startTime: '17:00', endTime: '18:30', hall: 'Deusterschule Kitzingen'},
        {team: 'U10 mix', day: 'Friday', startTime: '16:45', endTime: '18:15', hall: 'Deusterschule Kitzingen'},
        {team: 'U12 mix', day: 'Thursday', startTime: '17:35', endTime: '18:45', hall: 'Mainstockheim'},
        {team: 'U12 mix', day: 'Thursday', startTime: '11:00', endTime: '12:30', hall: 'Mainstockheim'},
        {team: 'U14 m', day: 'Thursday', startTime: '16:30', endTime: '18:30', hall: 'Arena Kitzingen'},
        {team: 'U14 m', day: 'Thursday', startTime: '17:00', endTime: '18:30', hall: 'Arena Kitzingen'},
        {team: 'U14 w', day: 'Thursday', startTime: '17:00', endTime: '18:30', hall: 'Arena Kitzingen'},
        {team: 'U14 w', day: 'Thursday', startTime: '18:30', endTime: '20:30', hall: 'Arena Kitzingen'},
        {team: 'U16 m', day: 'Thursday', startTime: '16:30', endTime: '18:30', hall: 'Arena Kitzingen'},
        {team: 'U16 m', day: 'Thursday', startTime: '18:30', endTime: '20:00', hall: 'Arena Kitzingen'},
        {team: 'U18/20 Damon', day: 'Thursday', startTime: '18:30', endTime: '20:00', hall: 'Arena Kitzingen'},
        {team: 'U18/20 Damon', day: 'Thursday', startTime: '18:30', endTime: '20:30', hall: 'Arena Kitzingen'},
        {team: 'U18 m', day: 'Thursday', startTime: '20:30', endTime: '22:00', hall: 'Arena Kitzingen'},
        {team: 'U18 m', day: 'Thursday', startTime: '18:30', endTime: '20:00', hall: 'Arena Kitzingen'},
        {team: 'U20 / Men', day: 'Sunday', startTime: '20:30', endTime: '22:00', hall: 'Arena Kitzingen'},
        {team: 'U20 / Men', day: 'Sunday', startTime: '20:00', endTime: '21:30', hall: 'Arena Kitzingen'},
        {team: 'OPEN COURT', day: 'Sunday', startTime: '15:00', endTime: '16:00', hall: 'Arena Kitzingen'},
      ],
    };
  },
  computed: {
    groupedSchedule() {
      const grouped = this.schedule.reduce((acc, curr) => {
        const existing = acc.find((item) => item.team === curr.team);
        if (existing) {
          existing.times.push({
            day: curr.day,
            startTime: curr.startTime,
            endTime: curr.endTime,
            hall: curr.hall,
          });
        } else {
          acc.push({
            team: curr.team,
            times: [
              {
                day: curr.day,
                startTime: curr.startTime,
                endTime: curr.endTime,
                hall: curr.hall,
              },
            ],
          });
        }
        return acc;
      }, []);
      return grouped;
    },
  },
}
</script>

<style scoped>
/* Add any additional styling here */
</style>
