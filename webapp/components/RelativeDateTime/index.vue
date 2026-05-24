<template>
  <span>{{ relativeDateTime }}</span>
</template>

<script>
import { getDateFnsLocale } from '~/locales'
import differenceInCalendarDays from 'date-fns/differenceInCalendarDays'
import format from 'date-fns/format'
import formatRelative from 'date-fns/formatRelative'

const RELATIVE_DATE_WINDOW_DAYS = 6

export default {
  name: 'HcRelativeDateTime',
  props: {
    dateTime: {
      type: [Date, String],
      required: true,
    },
  },
  computed: {
    relativeDateTime() {
      const date = new Date(this.dateTime)
      const locale = getDateFnsLocale(this)
      const calendarDayDistance = Math.abs(differenceInCalendarDays(date, new Date()))

      if (calendarDayDistance > RELATIVE_DATE_WINDOW_DAYS) {
        return format(date, 'Pp', { locale })
      }

      return formatRelative(date, new Date(), { locale })
    },
  },
}
</script>
