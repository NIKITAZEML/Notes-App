<template>
    <div class="new-note">
            <label>Title</label>
            <div class="input_select">
                <input type="text" v-model="note.title"> 
                <select v-model="note.priority">
                    <option selected>Low priority</option>
                    <option>Middle priority</option>
                    <option>High priority</option>
                </select>
            </div>
            <label>Descriptions</label>
            <textarea v-model="note.descr"></textarea>
            <button @click="addNote()" class="btn btnPrimary">New Note</button>
        </div>
</template>

<script>
export default {
    props: {
        note:{
            type: Object,
            required: true,
        },
    },
    methods: {
        addNote(){
            this.$emit("addNote", this.note)
        },
    }
}
</script>

<style lang="scss" scoped>
    .new-note{
        text-align: center;
    }
    .input_select{
        display: flex;
        select{
            margin-left:3.7vw;
            height: 60px;
        }
    }
</style>