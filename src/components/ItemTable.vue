<template>
    <div class=" px-20 flex justify-center">
        <table class="w-full bg-gray-300 border-2 border-black">
            <thead>
                <tr>
                    <th class="p-3 border-2 border-black" v-for="column in columns" :key="column">
                        {{ column.title }}
                    </th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="item,index in items" :key="item+index">
                    <td v-for="stat,index2 in item" :key="stat+index2">
                        {{ index }}
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name: 'HelloWorld',
    props:{
        items: Object
    },
    data(){
        return{
            columns:[
                {name: "id", title: "Class ID"},
                {name: "name", title: "Name"},
                {name: "quantity", title: "Quantity"},
            ]
        }
    }
}
</script>