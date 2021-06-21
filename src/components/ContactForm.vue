<template lang="pug">
  .fixed.inset-0.overflow-hidden(aria-labelledby='slide-over-title' role='dialog' aria-modal='true')
    .absolute.inset-0.overflow-hidden
      .absolute.inset-0.bg-black.bg-opacity-75.transition-opacity(aria-hidden='true' @click="close")

      .fixed.inset-y-0.right-0.pl-10.max-w-full.flex
        .relative.w-screen.max-w-xl
          .absolute.top-0.left-0.-ml-8.pt-4.pr-2.flex(class='sm:-ml-10 sm:pr-4')
            button.rounded-md.text-gray-300(class='hover:text-white focus:outline-none focus:ring-2 focus:ring-white' @click='close')
              span.sr-only Close panel
              svg.h-6.w-6(xmlns='http://www.w3.org/2000/svg' fill='none' viewBox='0 0 24 24' stroke='currentColor' aria-hidden='true')
                path(stroke-linecap='round' stroke-linejoin='round' stroke-width='2' d='M6 18L18 6M6 6l12 12')

          .h-full.flex.flex-col.py-6.bg-white.shadow-xl.overflow-y-scroll
            .px-4(class='sm:px-6')
              h2#slide-over-title.text-lg.font-medium.text-gray-900
                | {{ isEdit ? 'Edit Contact' : 'New Contact' }}
            .mt-6.relative.flex-1.px-4
              .absolute.inset-0.px-4
                //- .h-full.border-2.border-dashed.border-gray-200(aria-hidden='true')
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
export default {
  name: 'ContactForm',
  props: {
    isEdit: {
      type: Boolean,
      required: true
    },
    contact: {
      type: Object,
      required: true
    }
  },
  data () {
    return {}
  },
  methods: {
    close () {
      this.$emit('close')
    },
    save () {
      this.$emit('save', this.contact)
    }
  }
}
</script>

<style lang="scss" scoped>
  input {
    border-width: 1px;
    padding: .5rem .75rem;
  }
</style>
