<template>
  <div class="wrapper">
    <div class="wrapper-content">

      <section>
        <div class="container">
          <!-- title -->
          <h1 class="title">{{ title }}</h1>


          <!-- Message Error -->

         <message v-if="message" :message="message"/>

          <!-- new note -->

          <newNote :note="note" @addNote="addNote"/>

          <div class="note-header">
            
            <!-- search -->
            
            <search :value="search" placeholder="Find Your Note" @search="search = $event"/>

            <!-- icons controls -->
              <div class="icons">
                <svg :class="{ active: grid }" @click="grid = true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
                <svg :class="{ active: !grid }" @click="grid = false" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
              </div>
          </div>

          <!-- note-list -->

          <notes :notes="notesFilter" :grid="grid" @remove="removeNotes"/>

        </div>
      </section>

    </div>
  </div>
</template>

<script>
import message from '@/components/Message.vue'
import newNote from '@/components/NewNote.vue'
import notes from '@/components/Notes.vue'
import search from '@/components/Search.vue'

export default {
  components: {
    message,
    newNote,
    notes,
    search
  },
  data (){
    return{
      title: "Notes App",
      search: "",
      grid: true,
      message: null,
      note: {
          title: "",
          descr: "",
          priority: "Low priority",
      },
      notes: [
          {
              title: 'First Note',
              descr: 'Description for first note',
              data: new Date(Date.now()).toLocaleString(),
              priority: "Low priority"
          },
          {
              title: 'Second Note',
              descr: 'Description for second note',
              data: new Date(Date.now()).toLocaleString(),
              priority: "Low priority"
          },
          {
              title: 'Third Note',
              descr: 'Description for third note',
              data: new Date(Date.now()).toLocaleString(),
              priority: "Low priority"
          }
      ]
    }
  },
  computed:{
    notesFilter(){
      let array = this.notes,
          search = this.search
      if (!search) return array
      search = search.trim().toLowerCase()
      array = array.filter(function(item) {
        if(item.title.toLowerCase().indexOf(search) !== -1){
          return item
        }
      })
      return array
    }
  },
  methods: {
    addNote(){
            // console.log(this.note);
            let {title, descr, priority} = this.note;
            if (title === "") {
                this.message = "Title can`t be blank";
                return false;
            }
            this.notes.push({
                title,
                descr,
                priority,
                data : new Date(Date.now()).toLocaleString(),
            })

        console.log(this.note.priority)
            this.note.title = "";
            this.note.descr = "";
            this.message = null;
        },
    removeNotes(index){
      this.notes.splice(index, 1)
    },
  }
}
</script>

<style>
  .title{
    font-size: 30px;
  }
</style>
