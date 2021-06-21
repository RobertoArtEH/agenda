<template lang="pug">
  .flex.flex-col.p-12
    .-my-2.overflow-x-auto.sm_-mx-6.lg_-mx-8
      .py-2.align-middle.inline-block.min-w-full.sm_px-6.lg_px-8
        .text-right.mb-4
          button.inline-flex.justify-center.py-2.px-4.border.border-transparent.shadow-sm.text-sm.font-medium.rounded-md.text-white.bg-indigo-600(
            @click="create"
            class='hover_bg-indigo-700 focus_outline-none focus_ring-2 focus_ring-offset-2 focus_ring-indigo-500')
            | New

        .shadow.overflow-hidden.border-b.border-gray-200.sm_rounded-lg
          table.min-w-full.divide-y.divide-gray-200
            thead.bg-gray-50
              tr
                th.px-6.py-3.text-left.text-xs.font-medium.text-gray-500.uppercase.tracking-wider(scope='col')
                  | Name
                th.px-6.py-3.text-left.text-xs.font-medium.text-gray-500.uppercase.tracking-wider(scope='col')
                  | Work Info
                th.px-6.py-3.text-left.text-xs.font-medium.text-gray-500.uppercase.tracking-wider(scope='col')
                  | Status
                th.px-6.py-3.text-left.text-xs.font-medium.text-gray-500.uppercase.tracking-wider(scope='col')
                  | Phone
                th.relative.px-6.py-3(scope='col')
                  span.sr-only Edit
                th.relative.px-6.py-3(scope='col')
                  span.sr-only Delete

            tbody.bg-white.divide-y.divide-gray-200
              template(v-if="list.length")
                tr(v-for="(item, idx) in list")
                  //- Name column
                  td.px-6.py-4.whitespace-nowrap
                    .flex.items-center
                      .flex-shrink-0.h-10.w-10
                        img.h-10.w-10.rounded-full(src='https://image.flaticon.com/icons/png/512/848/848006.png' alt='')
                      .ml-4
                        .text-sm.font-medium.text-gray-900
                          | {{ item.name }}
                        .text-sm.text-gray-500
                          | {{ item.email }}

                  //- Work column
                  td.px-6.py-4.whitespace-nowrap
                    .text-sm.text-gray-900 {{ item.occupation }}
                    .text-sm.text-gray-500 {{ item.company }}

                  //- Status column
                  td.px-6.py-4.whitespace-nowrap
                    span.px-2.inline-flex.text-xs.leading-5.font-semibold.rounded-full(
                      :class="{ 'bg-green-100 text-green-800': item.status, 'bg-red-100 text-red-800': !item.status }"
                    )
                      | {{ item.status ? 'Active' : 'Inactive' }}

                  //- Phone column
                  td.px-6.py-4.whitespace-nowrap.text-sm.text-gray-500
                    | {{ item.phone }}

                  //- Actions column
                  td.px-6.py-4.whitespace-nowrap.text-right.text-sm.font-medium
                    .text-indigo-600.hover_text-indigo-900(@click="edit(idx)") Edit
                  td.px-6.py-4.whitespace-nowrap.text-right.text-sm.font-medium
                    .text-indigo-600.hover_text-indigo-900(@click="remove(idx)") Delete
              template(v-else)
                p.text-gray-500.p-6 No records
</template>

<script>
export default {
  name: 'ContactTable',
  props: {
    list: {
      type: Array,
      required: true
    }
  },
  data () {
    return {}
  },
  methods: {
    create () {
      this.$emit('create')
    },
    edit (idx) {
      this.$emit('edit', idx)
    },
    remove (idx) {
      this.$emit('remove', idx)
    }
  }
}
</script>
