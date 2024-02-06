<template>
    <div id="assignment-tracker">
        <button @click="toggleCompleted">{{ buttonText }}</button>
        <div id="assignment-container">
            <div v-for="assignment in filteredAssignments" :key="assignment.id" class="assignment"> 
                <h3>{{ assignment.title }}</h3>
                <p>Due Date: {{ assignment.dueDate }}</p>
                <p>Days Remaining: {{ daysRemaining(assignment.dueDate) }}</p>
                <p>Percent Complete: {{ calculatedPercentComplete(assignment.percentComplete) }}%</p>
            </div>
        </div>
    </div>
</template>

<script>
import assignments from '../data/assignments.json';

export default {
    data() {
        return {
            buttonStates: ['Show Complete', 'Show Incomplete', 'Show All'],
            buttonIndex: 0,
            assignments: assignments,
        };
    },
    methods: {
        toggleCompleted() {
            this.buttonIndex = (this.buttonIndex + 1) % this.buttonStates.length;
        },
        daysRemaining(dueDate) {
            const oneDay = 24 * 60 * 60 * 1000;
            const today = new Date();
            const due = new Date(dueDate);
            return Math.round((due - today) / oneDay);
        },
        calculatedPercentComplete(percentComplete) {
            return percentComplete * 100;
        }
    }, 
    computed: {
        filteredAssignments() {
            switch (this.buttonIndex) {
                case 0:
                    return this.assignments;
                case 1:
                    return this.assignments.filter(assignment => assignment.percentComplete === 1);
                case 2:
                    return this.assignments.filter(assignment => assignment.percentComplete < 1);
            }
        },
        buttonText() {
            return this.buttonStates[this.buttonIndex];
        }
    },
};
</script>

<style>
#assignment-tracker {
    height: 32rem;
    display: flex;
    flex-direction: column;
    margin-top: 3rem;
    row-gap: 1rem;
}

button {
    width: 10rem;
    height: 3rem;
    padding: 0.25rem 0.5rem;
    border: 3px solid transparent;
    color: white;
    border-radius: 5rem;
    cursor: pointer;
    background-color: #5fb0b7;
}

button:hover {
    border-color: #5bc8af;
}

#assignment-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    width: 80%;
    min-width: 560px;
}

.assignment {
    background-color: #a14ebf;
    border: 5px solid #af2bbf;
    border-radius: 10px;
    width: 90%;
    height: 10rem;
    margin: 1rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    row-gap: 0.25rem;
}

</style>