<template>
    <div>
        <div class="container-fluid">
            <div class="row">
                <div class="col-12 col-lg-4 droppable border border-dark" v-for="(zona, index) in zonas" :id="zona.id">{{zona.title}}
                    <div v-for="(boton, index) in botones" v-show="boton.zona == zona.id" class="draggable border btn btn-info" style="z-index: 10" :hidden="boton.hidden" :id="boton.id">{{boton.title}}</div>
                </div>
                <div v-for="(boton, index) in botones" v-show="boton.zona == null" class="draggable border btn btn-info" :hidden="boton.hidden" :id="boton.id">{{boton.title}}</div>
            </div>
        </div>
    </div>
</template>

<script>

  export default {
    mounted() {
        var self = this;
        $( ".draggable" ).draggable({ 
                revert: true,
        });
        $(".droppable").droppable({

            drop: function( event, ui) {
                console.log(event.target);
                console.log(event.toElement);
                console.log(ui);
                console.log(event);
                self.aZona(event.target.id, event.toElement.id);
            }
        });
    },
    data() {
      return {
        z1: 'zona1',
        activo: false,
        zonas: [
            {
                id: 1,
                title: 'Zona1'
            },
            {
                id: 2,
                title: 'Zona2'
            },
            {
                id: 3,
                title: 'Zona3'
            },
        ],
        botones: [

            {
                id: 1,
                title: 'prueba',
                hidden: false,
                zona: null,
            },
            {
                id: 2,
                title: 'prueba2',
                hidden: false,
                zona: null,
            },
            {
                id: 3,
                title: 'prueba3',
                hidden: false,
                zona: null,
            }

        ],
      };
    },
    methods: {
    aZona: function(i, b) {
        var btn = parseInt(b, 10) - 1;
        if (this.botones[btn].zona || this.botones[btn].zona == null) {
        this.botones[btn].zona = i;
    };
    },
    draggablexl: function(){
        $forceUpdate();
        },
    },
  };
</script>