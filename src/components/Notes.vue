<template>
    <div class="notes">
            <div class="note"
                 v-for="(note, index,) in notes"
                 :class="{ full: !grid,
                           high: note.priority === 'High priority',
                           middle: note.priority === 'Middle priority'}"
                 :key="index">
                <div class="note-header" @click="editNote(index)">
                    <p>
                        {{ note.title }}
                    </p>
                    <p style="cursor: pointer" @click="removeNotes(index)">x</p>
                </div>
                <input type="text" v-model="note.title">
                <div class="note-body">
                    <p>
                        {{ note.descr }}
                    </p>
                    <span>
                        {{ note.data }}
                    </span>
                    <hr>
                </div>
            </div>
        </div>
</template>

<script>
export default {
    data(){
      return{

      }
    },
    props: {
        notes:{
            type: Array ,
            required: true,
        },
        grid:{
          type: Boolean,
          required: true,
        },
    },
    methods: {
        removeNotes(index){
            console.log(`Note id ${index} - removed`);
            this.$emit("remove", index)
        },
        editNote(){
            this.$emit
        }
    }
}
</script>

<style lang="scss">
  .notes{
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    padding: 40px 0;
  }
  .note{
    width: 48%;
    padding: 18px 20px;
    margin-bottom: 20px;
    background-color: #fff;
    &.full{
      width: 100%;
    }
    &.red{
      background-color: red;
    }
    &.yellow{
      background-color: yellow;
    }
  }
  .note-body{
    p{
      margin: 20px 0;
    }
    span{
      font-size: 14px;
      color: #999;
    }
  }
  .note-header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    h1{
      font-size: 32px;
    }
    p{
      font-size: 22px;
      color: #402caf;
    }
    svg{
      color: #999;
      margin-right: 12px;
      cursor: pointer;
      &.active{
        color: #402caf;
      }
      &:last-child{
        margin: 0;
      }
    }
  }

  .high{
      background-color: #f13f3f;
  }

  .middle{
      background-color: rgba(255, 255, 0, 0.54);
  }
</style> 