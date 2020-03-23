<template>
  <div id="farm-table">
    <table>
      <!-- ...thead... -->
      <tbody>
        <tr v-for="farm in farms" :key="farm.id">
          <td>{{ farm.name }}</td>
          <td>{{ farm.email }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  export default {
    name: 'farm-table',
    props: {
        farms: Array,
    },
  }
</script>

<style scoped></style>