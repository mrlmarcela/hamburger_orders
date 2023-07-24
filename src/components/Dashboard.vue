<template>
    <div>
        <div>
            <Message :msg="msg" v-show="msg"/>
        </div>
        <table class="table table-hover">
            <thead>
                <tr>
                <th scope="col" width="5%">#</th>
                <th scope="col" width="20%">Client</th>
                <th scope="col" width="10%">Bread</th>
                <th scope="col" width="10%">Meat</th>
                <th scope="col" width="10%">Optionals</th>
                <th scope="col" width="15%">Actions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="burger in burgers" :key="burger.id">
                    <td>{{burger.id}}</td>
                    <td>{{burger.name}}</td>
                    <td>{{burger.bread}}</td>
                    <td>{{burger.meat}}</td>
                    <td>
                        <ul>
                            <li v-for="(optional, index) in burger.optional" :key="index">{{ optional }}</li>
                        </ul>
                    </td>
                    <td>
                        <div class="row">
                            <div class="col-8">
                                <select class="form-select" @change="UpdateStatusBurger($event, burger.id)">
                                    <option v-for="s in status" :key="s.id" :value="s.type" :selected="burger.status == s.type">{{ s.type }}</option>
                                </select>
                            </div>
                            <div class="col-4">
                                <button type="button" class="btn btn-danger" @click="deleteBurger(burger.id)">Cancel</button>
                            </div>
                        </div>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import Message from './Message.vue';

@Options({
  components: {
   Message,
  },
})

export default class Dashboard extends Vue {

    public burgers: Array<any>;
    public burger_id: number;
    public status: Array<any>;
    public msg: String;
    public statusMsg: boolean;

    data(){
        return{
            burger_id: null,
            burgers: [],
            status: [],
            msg: ""
        }
    }


    async getBurgers() {
        const request = await fetch("http://localhost:3000/burgers"); 
        const data = await request.json();
        this.burgers = data;
        this.getStatus();
    }


    async getStatus() {
        const request = await fetch("http://localhost:3000/status"); 
        const data = await request.json();
        this.status = data;
    }


    async deleteBurger(id) {
        const request = await fetch(`http://localhost:3000/burgers/${id}`, {
            method: "DELETE"
        }); 

        const data = await request.json();

        this.getBurgers();
        this.msg = `Order Nº ${id} successfully deleted!`;
        setTimeout(() => this.msg = "", 3000);
        this.statusMsg = true;
    }


    async UpdateStatusBurger(event, id) {
        
        const option = event.target.value;
        const dataJson = JSON.stringify({status: option});
        const request = await fetch(`http://localhost:3000/burgers/${id}`, {
            method: "PATCH",
            headers: {"Content-type": "application/json"},
            body: dataJson
        }); 
        const data = await request.json();
        this.getBurgers();

        this.msg = `Order status #${id} has been successfully updated to ${data.status}!`;
        setTimeout(() => this.msg = "", 3000);
        this.statusMsg = true;
    }


    mounted(){
        this.getBurgers();
    }
}
</script>