<template lang="pug">
  div
    Header

    ContactTable(
      :list="contacts"
      @create="create"
      @edit="idx => edit(idx)"
      @remove="idx => remove(idx)"
    )

    ContactForm(
      v-if="showForm"
      :isEdit="isEdit"
      :contact="contact"
      @close="closeForm"
      @save="save"
    )
</template>

<script>
import Header from '@/components/Header'
import ContactTable from '@/components/ContactTable'
import ContactForm from '@/components/ContactForm'

export default {
  name: 'Home',
  components: {
    Header,
    ContactTable,
    ContactForm
  },
  data () {
    return {
      contacts: [],
      contact: {
        name: null,
        email: null,
        phone: null,
        company: null,
        occupation: null,
        status: true
      },
      showForm: false,
      isEdit: false,
      currentIndex: null
    }
  },
  methods: {
    create () {
      this.showForm = true
      this.isEdit = false
    },
    edit (idx) {
      this.isEdit = true
      this.showForm = true
      this.currentIndex = idx

      this.contact = Object.assign({}, this.contacts[idx])
    },
    remove (idx) {
      this.contacts.splice(idx, 1)
    },
    save () {
      if (this.currentIndex !== null) {
        this.$set(this.contacts, this.currentIndex, this.contact)
        this.currentIndex = null

        return this.closeForm()
      }

      this.contacts.push(Object.assign({}, this.contact))
      this.closeForm()
    },
    closeForm () {
      this.showForm = false
      this.cleanForm()
    },
    cleanForm () {
      this.contact = {
        name: null,
        email: null,
        phone: null,
        company: null,
        occupation: null,
        status: true
      }
    }
  }
}
</script>
