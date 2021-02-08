<template>
  <div class="wrapper">
    <!-- <header></header> -->
    <div class="wrapper-content">
      <section>
        <div class="container">
          <div
            class="note-header"
            style="margin: 36px 0; justify-content: center;"
          >
            <p>{{ title }}</p>
          </div>
          <!-- message -->
          <Message v-if="message" :message="message" />
          <!-- new note -->
          <NewNote
            :note="note"
            :colorPalette="colorPalette"
            @addNote="addNote"
          />
          <div class="note-header" style="margin: 36px 0">
            <!-- title -->
            <h1>{{ title }}</h1>
            <!-- search -->
            <Search
              :value="search"
              placeholder="Find your note"
              @search="search = $event"
            />
            <!-- control icons -->
            <div class="icons">
              <svg
                :class="{active: grid}"
                @click="grid = true"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <rect x="3" y="3" width="7" height="7"></rect>
                <rect x="14" y="3" width="7" height="7"></rect>
                <rect x="14" y="14" width="7" height="7"></rect>
                <rect x="3" y="14" width="7" height="7"></rect>
              </svg>
              <svg
                :class="{active: !grid}"
                @click="grid = false"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <line x1="8" y1="6" x2="21" y2="6"></line>
                <line x1="8" y1="12" x2="21" y2="12"></line>
                <line x1="8" y1="18" x2="21" y2="18"></line>
                <line x1="3" y1="6" x2="3" y2="6"></line>
                <line x1="3" y1="12" x2="3" y2="12"></line>
                <line x1="3" y1="18" x2="3" y2="18"></line>
              </svg>
            </div>
          </div>
          <!-- note list -->
          <Notes :notes="notesFilter" :grid="grid" @remove="removeNote" />
        </div>
      </section>
    </div>
    <!-- <footer></footer> -->
  </div>
</template>

<script>
import Message from '@/components/Message'
import NewNote from '@/components/NewNote'
import Notes from '@/components/Notes'
import Search from '@/components/Search'
export default {
  components: {
    Message,
    NewNote,
    Notes,
    Search
  },
  data() {
    return {
      title: 'Notes App',
      search: '',
      message: null,
      grid: true,
      colorPalette: [
        '#ffffff',
        '#C6E6AC',
        '#DFF8EB',
        '#FFA400',
        '#B59DA4',
        '#FFA8A9'
      ],
      note: {
        title: '',
        descr: '',
        color: '#fff',
        isImportant: false,
        isDone: false
      },
      notes: [
        {
          title: 'First Note',
          descr: 'Description for first note',
          color: '#DFF8EB',
          isImportant: true,
          isDone: true,
          date: new Date(Date.now()).toLocaleString()
        },
        {
          title: 'Second Note',
          descr: 'Description for second note',
          color: '#B59DA4',
          date: new Date(Date.now()).toLocaleString()
        },
        {
          title: 'Third Note',
          descr: 'Description for third note',
          color: '#FFA8A9',
          date: new Date(Date.now()).toLocaleString()
        }
      ]
    }
  },
  computed: {
    notesFilter() {
      let arr = this.notes,
        search = this.search
      if (!search) return arr
      // small
      search = search.trim().toLowerCase()
      // filter
      arr = arr.filter(function(item) {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item
        }
      })
      // error
      return arr
    }
  },
  methods: {
    addNote() {
      console.log(this.note)
      let {title, descr, color, isImportant} = this.note

      if (title === '') {
        this.message = 'title can`t be blank!'
        return false
      }

      this.notes.push({
        title,
        descr,
        color,
        isImportant,
        date: new Date(Date.now()).toLocaleString()
      })
      this.message = null
      this.note.title = ''
      this.note.descr = ''
      this.note.color = '#fff'
      this.note.isImportant = false
      this.note.isDone = false
    },
    removeNote(index) {
      this.notes.splice(index, 1)
    }
  }
}
</script>

<style scoped>
.container {
  max-width: 800px;
}
</style>
