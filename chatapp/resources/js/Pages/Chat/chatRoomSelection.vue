<template>
    <div class="grid grid-cols-2">
        <h2 class="font-semibold text-xl text-gray-800 leading-tight">
            {{ selected.name }} Chat
        </h2>
        <div>
            <select v-model="selected" @change="$emit( 'roomChanged', selected )" class="float-right leading-3">
                <option v-for="(room, index) in rooms" :key="index" :value="room">
                    {{ room.name }}
                </option>
            </select>
        </div>
    </div>
</template>

<script>
export default {
    props: ['rooms', 'currentRoom'],
    data: function () {
        return {
            selected: ''
        }
    },
    created() {
        this.selected = this.currentRoom;
    }
}
</script>