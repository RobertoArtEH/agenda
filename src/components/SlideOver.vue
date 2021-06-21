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
                | {{ title }}
            .mt-6.relative.flex-1.px-4
              .absolute.inset-0.px-4
                template(v-if="hasDefaultSlot")
                  slot
                template(v-else)
                  .h-full.border-2.border-dashed.border-gray-200(aria-hidden='true')
</template>

<script>
export default {
  name: 'SlideOver',
  props: {
    title: {
      type: String,
      required: true
    }
  },
  data () {
    return {}
  },
  computed: {
    hasDefaultSlot () {
      return !!this.$slots.default
    }
  },
  methods: {
    close () {
      this.$emit('close')
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
