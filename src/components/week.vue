<template>
    <tr>
        <td style="color: rgb(0, 125, 184) ;">{{WeekInformation.weekinfo.Q}}</td>
        <td style="color: rgb(0, 125, 184) ;">{{WeekInformation.weekinfo.W}}</td>
        <td v-bind:style="{backgroundColor : WeekInformation.weekDates[0].c}">{{WeekInformation.weekDates[0].d}}</td>
        <td v-bind:style="{backgroundColor : WeekInformation.weekDates[1].c}">{{WeekInformation.weekDates[1].d}}</td>
        <td v-bind:style="{backgroundColor : WeekInformation.weekDates[2].c}">{{WeekInformation.weekDates[2].d}}</td>
        <td v-bind:style="{backgroundColor : WeekInformation.weekDates[3].c}">{{WeekInformation.weekDates[3].d}}</td>
        <td v-bind:style="{backgroundColor : WeekInformation.weekDates[4].c}">{{WeekInformation.weekDates[4].d}}</td>
        <td v-bind:style="{backgroundColor : WeekInformation.weekDates[5].c}">{{WeekInformation.weekDates[5].d}}</td>
        <td v-bind:style="{backgroundColor : WeekInformation.weekDates[6].c}">{{WeekInformation.weekDates[6].d}}</td>
    </tr>
</template>
<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import { ArrayPropsDefinition } from "vue/types/options";


@Component({})
export default class week extends Vue {
   @Prop() private WeekInformation!: any;
   constructor(){
       super()
   }
}
</script>
<style scoped>
td,th {
    background-color:  rgb(49, 49, 49);
    text-align: center;
    padding: 3px;
    color: aliceblue;
    border:rgb(49, 49, 49) solid;
    border-radius: 15px;
}
</style>
