<template lang="pug">
  nav.bg-indigo-900
    .mx-auto.px-10(class='sm:px-6 lg:px-8')
      .flex.items-center.justify-between.h-16
        .flex.items-center
          .flex-shrink-0
            img.h-8.w-8(src='https://tailwindui.com/img/logos/workflow-mark-white.svg' alt='Workflow')
          .md_block
            .ml-10.flex.items-baseline.space-x-4
              a.bg-indigo-600.text-white.px-3.py-2.rounded-md.text-sm.font-medium(href='#') Home

        .md_block
          .ml-4.flex.items-center(class='md:ml-6')
            .ml-3.relative
              button#user-menu-button.max-w-xs.bg-indigo-800.rounded-full.flex.items-center.text-sm(type='button' class='focus_outline-none focus_ring-2 focus_ring-offset-2 focus_ring-offset-gray-800 focus_ring-white' aria-expanded='false' aria-haspopup='true')
                span.sr-only Open user menu
                img.h-8.w-8.rounded-full(src='https://image.flaticon.com/icons/png/512/848/848006.png' alt='')
</template>

<script>
export default {
  name: 'Header'
}
</script>
