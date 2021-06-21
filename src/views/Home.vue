<template lang="pug">
  div
    Header

    ContactTable(
      :list="contacts"
      @create="create"
      @edit="idx => edit(idx)"
      @remove="idx => remove(idx)"
    )

    SlideOver(
      v-if="showForm"
      @close="closeForm"
      :title="isEdit ? 'Edit Contact' : 'New Contact'"
    )
      .md_col-span-2
        .overflow-hidden
          .px-4.py-5.bg-white
            .grid.grid-cols-6.gap-6
              .col-span-6
                label.block.text-sm.font-medium.text-gray-700(for='first_name') Name
                input#first_name.mt-1.block.w-full.shadow-sm.border-gray-300.rounded-md.focus_ring-indigo-500.focus_border-indigo-500.sm_text-sm(
                  type='text'
                  name='first_name'
                  v-model="contact.name"
                )
              .col-span-6
                label.block.text-sm.font-medium.text-gray-700(for='phone') Phone
                input#phone.mt-1.block.w-full.shadow-sm.border-gray-300.rounded-md.focus_ring-indigo-500.focus_border-indigo-500.sm_text-sm(
                  type='phone'
                  name='phone'
                  v-model="contact.phone"
                )
              .col-span-6
                label.block.text-sm.font-medium.text-gray-700(for='email_address') Email address
                input#email_address.mt-1.block.w-full.shadow-sm.border-gray-300.rounded-md.focus_ring-indigo-500.focus_border-indigo-500.sm_text-sm(
                  type='text'
                  name='email_address'
                  v-model="contact.email"
                )
              .col-span-6
                label.block.text-sm.font-medium.text-gray-700(for='occupation') Occupation
                input#occupation.mt-1.block.w-full.shadow-sm.border-gray-300.rounded-md.focus_ring-indigo-500.focus_border-indigo-500.sm_text-sm(
                  type='text'
                  name='occupation'
                  v-model="contact.occupation"
                )
              .col-span-6
                label.block.text-sm.font-medium.text-gray-700(for='company') Company
                input#company.mt-1.block.w-full.shadow-sm.border-gray-300.rounded-md.focus_ring-indigo-500.focus_border-indigo-500.sm_text-sm(
                  type='text'
                  name='company'
                  v-model="contact.company"
                )
              .col-span-6
                .flex.items-center
                  input#remember_me.h-4.w-4.text-indigo-600.border-gray-300.rounded(
                    name='remember_me'
                    type='checkbox'
                    class='focus_ring-indigo-500'
                    v-model="contact.status"
                  )
                  label.ml-2.block.text-sm.text-gray-900(for='remember_me')
                    | Active
          .px-4.py-3.text-right.sm_px-6
            button.inline-flex.justify-center.py-2.px-4.border.border-transparent.shadow-sm.text-sm.font-medium.rounded-md.text-white.bg-indigo-600(
              @click="save"
              class='hover_bg-indigo-700 focus_outline-none focus_ring-2 focus_ring-offset-2 focus_ring-indigo-500')
              | Save
</template>

<script>
import Header from '@/components/Header'
import ContactTable from '@/components/ContactTable'
import SlideOver from '@/components/SlideOver'

export default {
  name: 'Home',
  components: {
    Header,
    ContactTable,
    SlideOver
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
