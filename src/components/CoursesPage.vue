<template>    
    <div class="">
        <span>from</span>
        <input type="number" v-model="startNumber" @input='startFilter'>
        <span>to</span>
        <input type="number" v-model="endNumber" @input='startFilter'>
        <button @click.prevent="sortCurses">sort</button>      

        <ul>
            <li v-for="item in coursesTmp" :key="item.id">
                {{ item }}
            </li>
        </ul> 
    </div>
</template>

<script>
import {ref} from 'vue';
export default {
    name: 'CorsesPage',

    props: {
        courses: {
            type: Array,
            require: true,
        }
    },  
    setup(props) {
        let coursesTmp = ref(props.courses);
        let startNumber = ref(null);
        let endNumber = ref(null);
        const keyDict = 'prices';
        
        const startFilter = () => {
            coursesTmp.value = [...props.courses].filter(item => {
                if(startNumber.value > endNumber.value && (startNumber.value !== null && startNumber.value !== '') && (endNumber.value !== null && endNumber.value !== '')) return false;

                if(item[keyDict][0] === null && item[keyDict][1] === null) return true;

                if(startNumber.value > item[keyDict][1] && item[keyDict][1] !== null ) {
                    if(startNumber.value === null || startNumber.value === '') return true;
                    return false;
                }
                if(endNumber.value < item[keyDict][0] && item[keyDict][0] !== null) {
                    if(endNumber.value === null || endNumber.value === '') return true;
                    return false;
                }
                
                if(startNumber.value === null || startNumber.value === '') return true;
                return true;
            })
        }
        let aTure = -1;
        let bTrue = 1;
        function sortCurses() {
            let tmp = aTure;
            aTure = bTrue;
            bTrue = tmp;
            coursesTmp.value =  coursesTmp.value.sort((a,b) => {
                return a[keyDict][0] < b[keyDict][0] ? aTure : bTrue;
            })
        }

        return {
            startNumber,
            endNumber,
            coursesTmp,
            startFilter,
            sortCurses,
        }
    },
}
</script>

