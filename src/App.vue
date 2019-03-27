<template>
    <div>
        <div class="container-fluid" style="background-image: url(/dist/Entregables/Fondo.jpg); background-position: center; /* Center the image */
  background-repeat: repeat; /* Do not repeat the image */
  height: 4300px; /* You must set a specified height */
  background-size: cover; min-height: 800px /* Resize the background image to cover the entire container */">
            <div class="row">
                <div class="col-4 p-1">
                    <div class="col-12 my-1">
                        <img src="/dist/Entregables/instrucciones.png" alt="" class="img-fluid">
                    </div>
                    <div class="col-12 px-2 border my-1" style="min-height: 500px">
                        <div v-for="(boton, index) in botones" v-show="boton.zona == null" class="draggable border btn btn-warning  btn-block" style="z-index: 10" :hidden="boton.hidden" :id="boton.id">{{boton.title}}</div>
                    </div>
                </div>
                <div class="col-8">
                    hola2
                    <div class="col-12 my-1">
                        <div class="row">
                            <div class="col-12 col-lg-6 droppable border border-dark" style="min-height: 450px" v-for="(zona, index) in zonas" :id="zona.id">{{zona.title}}
                                <div v-for="(boton, index) in botones" v-show="boton.zona == zona.id" class="draggable border btn btn-warning btn-block" style="z-index: 10" :hidden="boton.hidden" :id="boton.id">{{boton.title}}</div>
                            </div>
                        </div>
                    </div>
                    <div class="col-8 my-1 mx-auto">
                        <img :src="'/dist/Entregables/0'+this.blnc+'.png'" alt="" class="img-fluid">

                        <!-- Button trigger modal -->

                        <button type="button" class="btn btn-primary" @click="reload()">
  reload
</button>

<button type="button" class="btn btn-primary" @click="test()">
  test
</button>

<button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModalCenter">
  Launch demo modal
</button>

<!-- Modal -->

                    </div>
                </div>
                
            </div>
        </div>

        <div class="modal fade" id="exampleModalCenter" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
          <div class="modal-dialog modal-dialog-centered" role="document">
            <div class="modal-content">
              <div class="modal-header">
                <h5 class="modal-title" id="exampleModalCenterTitle">Modal title</h5>
                <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                  <span aria-hidden="true">&times;</span>
                </button>
              </div>
              <div class="modal-body">
                ...
              </div>
              <div class="modal-footer">
                <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
                <button type="button" class="btn btn-primary">Save changes</button>
              </div>
            </div>
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
        sum: null,
        z1: 'zona1',
        activo: false,
        blnc: 3,
        balanza: [ { id: 1, img: '01' },
            { id: 2, img: '02' },
            { id: 3, img: '03' },
            { id: 4, img: '04' },
            { id: 5, img: '05' } ],
        zonas: [
            {
                id: 1,
                title: 'Zona1',
                peso: null
            },
            {
                id: 2,
                title: 'Zona2',
                peso: null
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
        reload: function() {
            location.reload();

        },
        test: function() {
            for (var z = 0; z < this.zonas.length; z++) {
                this.zonas[z].peso = null;
                for (var i = 0; i < this.botones.length; i++) {
                    if (this.botones[i].zona == this.zonas[z].id) { 
                        this.zonas[z].peso = 1 + this.zonas[z].peso; 
                    }
                }
            }
        },
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