<template>
    <div>
        <div class="form-group">
            <label for="firstName">First Name</label>
            <!-- We bind the value to the computed property firstName and lastName respectively
                These computed properties will look at the value the userData.fullName contains, coming from App.Vue
                and split them by the " " and store them in the respective properties separately.
                Then we add an input event listener that executes a function called nameChanged, 
                which takes 2 arguments: true, if it's the firstName and false if it's the lastName, and the $event variable.
                Then in the nameChanged function, we check if it's the firstName or lastName and add the values that the user put in
                to the already existing value for the other name.
                Once that's done, we need to emit an input event, as App.vue will be listening for that - this is needed anytime we want to
                split up our form controls into components. -->
            <input
                    type="text"
                    id="firstName"
                    class="form-control"
                    :value="firstName"
                    @input="nameChanged(true, $event)"
                    >
        </div>
        <div class="form-group">
            <label for="lastName">Last Name</label>
            <input
                    type="text"
                    id="lastName"
                    class="form-control"
                    :value="lastName"
                    @input="nameChanged(false, $event)"
                    >

        </div>
    </div>
    
</template>

<script>
export default {
    props: ["value"],
    methods: {
        nameChanged(isFirst, event) {
            let name = ""
            if(isFirst) {
                name = event.target.value + " " + this.lastName;
            } else {
                name = this.firstName + " " + event.target.value;
            }
             this.$emit("input", name);

        }
    },
    computed: {
        firstName() {
            return this.value.split(" ")[0]
        },
        lastName() {
            return this.value.split(" ")[1]
        }
    }
}
</script>

<style>

</style>


