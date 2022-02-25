<template>
    <div class="wrapper">
        <Datepicker v-model="selectedDate" placeholder="Select Date" :presetRanges="presetRanges" range multiCalendars/>
    </div>
</template>

<script>
    import { ref } from 'vue';
    import Datepicker from '../src/Vue3DatePicker/Vue3DatePicker.vue';
    import {
        endOfMonth,
        endOfWeek,
        endOfYear,
        startOfMonth,
        startOfWeek,
        startOfYear,
        subMonths,
        subWeeks,
        subYears,
    } from 'date-fns';

    export default {
        components: {
            Datepicker,
        },
        setup() {
            const selectedDate = ref();
            const presetRanges = ref([
                { label: 'Today', range: [new Date(), new Date()] },
                { label: 'This week', range: [startOfWeek(new Date()), endOfWeek(new Date())], default: true },
                {
                    label: 'Last week',
                    range: [startOfWeek(subWeeks(new Date(), 1)), endOfWeek(subWeeks(new Date(), 1))],
                },
                { label: 'This month', range: [startOfMonth(new Date()), endOfMonth(new Date())] },
                {
                    label: 'Last month',
                    range: [startOfMonth(subMonths(new Date(), 1)), endOfMonth(subMonths(new Date(), 1))],
                },
                {
                    label: 'Last 30 days',
                    range: [new Date(new Date().getTime() - 30 * 24 * 60 * 60 * 1000), new Date()],
                },
                {
                    label: 'Last 90 days',
                    range: [new Date(new Date().getTime() - 90 * 24 * 60 * 60 * 1000), new Date()],
                },
                {
                    label: 'Last 12 mths',
                    range: [new Date(new Date().getTime() - 12 * 30 * 24 * 60 * 60 * 1000), new Date()],
                },
                { label: 'This year', range: [startOfYear(new Date()), endOfYear(new Date())] },
                {
                    label: 'Last year',
                    range: [startOfYear(subYears(new Date(), 1)), endOfYear(subYears(new Date(), 1))],
                },
            ]);
            return {
                selectedDate,
                presetRanges,
            };
        },
    };
</script>

<style lang="scss">
    @import 'src/Vue3DatePicker/style/main';

    .wrapper {
        padding: 200px;
    }
</style>
