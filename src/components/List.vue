<template>
    <div>
        <h1>Hi list</h1>
        <ul>
            <li v-for="work in works">
                <h2>Nombre Trabajo: <small>{{work.nameWork}}</small></h2>
                <p>Descripción: {{work.description}}</p>
                <p>Fecha: {{work.day}}/{{work.mounth}}/{{work.year}}</p>
                <p>Valor: {{work.cost}}</p>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    mounted(){
        this.listWorks();
    },
    data (){
        return{
            works: []
        }
    },
    methods:{
        listWorks(){
            
            this.axios.get('https://easyworkback.herokuapp.com/easyWork/user/get-works')
            .then(res => {
                const getWorks = [];
                
                res.data.trabajos.map((trabajo) => {
                    trabajo.map((valor) => {
                        var help = valor.year;

                        if(help != 1){
                            getWorks.push({
                                idWork:      valor._id,
                                nameWork:    valor.nombre,
                                description: valor.descripcion,
                                file:        valor.archivo,
                                day:         valor.dia,
                                mounth:      valor.mes,
                                year:        valor.year,
                                cost:        valor.pago
                            });
                        }



                    })
                });

                this.works = getWorks;
            })
        }
    }
}
</script>