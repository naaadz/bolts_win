<template>
	<div>
		<h1>Bolts win!</h1>
		<h2>Bolts schedule</h2>
        <table>
            <thead>
                <tr>
                    <th></th>
                    <th>Teams</th>
                    <th>Date</th>
                    <th>Status</th>
                    <th>Home points</th>
                    <th>Away points</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(row, index) in data.y" :key="row.id">
                    <td>{{ index }}</td>
                    <td>{{ row.home.name }} vs {{ row.away.name }}</td>
                    <td>{{ row.scheduled }}</td>
                    <td>{{ row.status }}</td>
                    <td>{{ row.home_points }}</td>
                    <td>{{ row.away_points }}</td>
                </tr>
            </tbody>
        </table>
	</div>
</template>

<script setup>

const data = reactive({
    y: null
})

const result  = await useFetch('/api/getBoltsSchedule').then((x) => {
    //console.log('x', x)
    x.data.value.forEach(game => {
        //format the date
        let thedate = new Date(game.scheduled)
        game.scheduled = thedate.toLocaleString()
    })
    data.y = x.data
})

</script>
