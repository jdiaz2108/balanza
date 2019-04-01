<template>
    <div>
        <div class="container-fluid p-0 shadow">
             <img src="dist/Entregables/up.png" alt="" class="img-fluid p-0 m-0">
        </div>
        <div class="container-fluid" style="background-image: url(dist/Entregables/Fondo.jpg); background-position: cover; /* Center the image */
  background-repeat: repeat; /* Do not repeat the image */
  background-size: cover;">
            <div class="row ">
                <div class="col-5 my-3">
                    <div class="col-11 mx-auto p-2 h5 text-center bg-white" style="border-radius: 15px; ">

                       <p class="m-0">Arrastra las Variables que evalúa el cliente hasta su respectiva posición de la balanza</p>
                    </div>
                    <div class="col-11 mx-auto text-center mt-2 pt-1 border borderbox" id="set">
                        <div v-for="(boton, index) in orderedUsers" v-show="boton.zona == null" class="draggable border btn btn-light col-5 mx-2 my-1 shadow"  @mouseover="mouseOver()"  :style="z1" style="border-radius: 10px;" :id="boton.id">{{boton.title}}</div>

                        <div class="btn col-5 mx-2"  @mouseover="mouseOver()"  :style="z1" style="border-radius: 10px; border: 1px"></div>

                    </div>
                <div class="col-8 my-3 text-center mx-auto">


                 <button v-if="faltan <= botones.length - 1 " type="button" class="btn btn-danger align-self-end" @click="reload()">
                Volver a empezar
                </button>

            <!-- Modal -->
            </div>
                </div>
        <div class="col-7 my-2">
            <div class="row justify-content-around" style="z-index: -1px">
                <div class="col-6 m-0 droppable" v-for="(zona, index) in zonas"  :id="zona.id" style="z-index: -1px; max-width: 100% !important">
                    <div class=" h4 text-center mb-2 text-white droppable" :id="zona.id">{{zona.cont}}</div>

                    <div class="col-12 row border borderbox" style="min-height: 300px;" :id="zona.id">




                        <div v-for="(boton, index) in orderedUsers" v-show="boton.zona == zona.id" class="col-6"  style="z-index: -1px">
                            <div @mouseover="mouseOver()" class="draggable border btn btn-sm btn-light my-1 shadow btn-block" style="z-index: 10; border-radius: 10px;" :id="boton.id">{{boton.title}}</div>
                        </div>
                    </div>
                    
                </div>
            </div>

            <div class="col-8 mx-auto">
                <img :src="'dist/Entregables/0'+this.blnc+'.png'" alt="" class="img-fluid">

                <!-- Button trigger modal -->


            <!-- Modal -->
            </div>

            <div class="col-8 text-center mx-auto">


                <!-- Button trigger modal -->


                <button v-if="faltan == 0" type="button" class="btn btn-pink" @click="validator()">
                Validar
                </button>
                <button v-else type="button" class="btn btn-pink2" disabled>
                Validar
                </button>

            <!-- Modal -->
            </div>


        </div>
                
            </div>
        </div>
      <div class="container-fluid p-0 shadow">
             <img src="dist/Entregables/abajo.png" alt="" class="img-fluid p-0 m-0">
        </div>

<div class="position-fixed" style="display: none">{{$data}}</div>
    </div>
</template>

<script>
import Swal from 'sweetalert2'
import _ from 'lodash';
export default {
    computed: {
  orderedUsers: function () {
    return _.orderBy(this.botones,  ['move'], ['desc'])
  },
},
    created() {
        this.addValues();
    },
    mounted() {
        var self = this;
        $( "#set div" ).draggable({ stack: "#set div" });
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
                self.test();
            }
        });
    },
    data() {
        return {
            pasar: false,
            faltan: null,
            peso: null,
            sum: null,
            z1: 0,
            activo: false,
            blnc: 3,
            movimiento: 0,
            zonas: [
                { id: 1, title: 'Zona1', peso: 0, porcentaje: null, cont: 'Beneficio' },
                { id: 2, title: 'Zona2', peso: 0, porcentaje: null, cont: 'Costo' }
            ],
            botones: [
                { title: 'Es Confiable', val: 1 },
                { title: 'Tiene Calidad', val: 1 },
                { title: 'Es Estable', val: 1 },
                { title: 'Es Duradero', val: 1 },
                { title: 'Tiene Respaldo', val: 1 },
                { title: 'Tiene Garantía', val: 1 },
                { title: 'Hay Personalización', val: 1 },
                { title: 'Es Diligente', val: 1 },
                { title: 'Es Negligente', val: 1 },
                { title: 'Es Caro', val: 2 },
                { title: 'Es Barato', val: 2 },
                { title: 'Necesita Recursos', val: 2 },
                { title: 'Necesita Adaptación', val: 2 },
                { title: 'Es Demorado', val: 2 },
                { title: 'Es Rápido', val: 2 },
                { title: 'Hay Traslados', val: 2 },
                { title: 'Hay Desgaste', val: 2 },
                { title: 'Hay  Frustración', val: 2 }
            ],
        };
    },
    methods: {

                mouseOver: function(){
            this.z1 = {'z-index': 10}
        },
        addValues: function() {
            for (var i = 0; i < this.botones.length; i++) {
                this.botones[i].random = Math.random() * 100;
            }
            this.botones.sort(function(a, b) {
                return parseFloat(b.random) - parseFloat(a.random);
            });
            for (var i = 0; i < this.botones.length; i++) {
                this.botones[i].id = i + 1;
                this.botones[i].zona = null;
                this.botones[i].move = 0;
            }
            this.faltan = this.botones.length;
        },
        reload: function() {
            Swal.fire({
              title: 'Volver a empezar',
              html: '¿Está seguro de que desea volver a empezar?',
              showCloseButton: true,
              showCancelButton: true,
              focusConfirm: false,
              customClass: {
                    confirmButton: 'btn btn-danger btn-lg mx-1',
                    cancelButton: 'btn btn-secondary btn-lg mx-1',
                },
                buttonsStyling: false,
              confirmButtonText:
                'Si',
              cancelButtonText:
                'Cancelar',
              preConfirm: () => { location.reload(); }
            })
            // location.reload();
        },
        validator: function() {
            for (var i = 0; i < this.botones.length; i++) {
                console.log(this.botones[i])

                if (this.botones[i].val != this.botones[i].zona) {
                    this.pasar = false;
                    this.validatorError();
                    break
                } else {
                    this.pasar = true;
                }
                }
            if (this.pasar) { this.validatorSuccess() }
            // this.validatorSuccess();
        },
        validatorSuccess: function() {
            Swal.fire({
                title: '¡Muy Bien!',
                text: 'Así se categorizan las variables que evalúa el cliente.',
                confirmButtonText: 'Jugar de nuevo',
                allowOutsideClick: false,
                customClass: {
                    confirmButton: 'btn btn-danger btn-lg'
                },
                buttonsStyling: false,
                preConfirm: () => { location.reload(); }
            })
        },
        validatorError: function() {
            Swal.fire({
                text: 'Así no se categorizan las variables que evalúa el cliente.',
                type: 'warning',
                confirmButtonText: '¡Inténtalo de nuevo!',
                allowOutsideClick: false,
                customClass: {
                    confirmButton: 'btn btn-danger btn-lg',
                },
                buttonsStyling: false,
                preConfirm: () => { location.reload(); }
            })
        },
        test: function() {

            this.peso = 0;
            for (var z = 0; z < this.zonas.length; z++) {
                this.zonas[z].peso = 0;
                this.faltan = 0;
                for (var i = 0; i < this.botones.length; i++) {
                    if (this.botones[i].zona == this.zonas[z].id) { 
                        this.zonas[z].peso = 1 + this.zonas[z].peso;
                    }
                    if (this.botones[i].zona == null) {
                        this.faltan = this.faltan + 1;
                    }
                }
                this.peso = this.peso + this.zonas[z].peso;
            }
            for (var z = 0; z < this.zonas.length; z++) {
                this.zonas[z].porcentaje = (this.zonas[z].peso * 100) / this.peso;
            }
            if (this.zonas[0].porcentaje === 50 && this.zonas[1].porcentaje === 50) {
                this.blnc = 3;
            } else if (this.zonas[0].porcentaje > 50) {
                if (this.zonas[0].porcentaje > 66) { this.blnc = 5; } else { this.blnc = 4}
            } else if (this.zonas[1].porcentaje > 50) {
                if (this.zonas[1].porcentaje > 66) { this.blnc = 1; } else { this.blnc = 2}
            }
        },
        aZona: function(i, b) {
            this.movimiento = this.movimiento + 1;
            var btn = parseInt(b, 10) - 1;
            if (this.botones[btn].zona || this.botones[btn].zona == null) {
                this.botones[btn].zona = i;
                this.botones[btn].move = this.botones[btn].move + this.movimiento;
            };
        },
        Swal: function(type) {
            Swal.fire({
                title: '¡Muy Bien!',
                text: 'Así se categorizan las variables que evalúa el cliente.',
                type: type,
                confirmButtonText: 'Jugar de nuevo',
                allowOutsideClick: true,
                customClass: {
                    confirmButton: 'btn btn-'+type+' btn'
                },
                buttonsStyling: false,
                preConfirm: () => { location.reload(); }
            })
        },
    },
};

</script>

<style>
.swal2-icon.swal2-warning {
    border-color: #ff5454;
    color: #ff5454;
}
.swal2-popup .swal2-title {
    color: #ff5454;
}
.swal2-popup .swal2-content {
    color: #545454;
    font-size: 1.6em;
        font-weight: 500;
    }
.borderbox {
    min-height: 450px;
    border-radius: 10px; 
    background-color: rgba(255,255,255,.3); 
    border-style: dashed !important;
}
.btn-pink {
    color: #fff;
    background-color: #cc91db;
    border-color: #cc91db;
}
.btn-pink2 {
    color: #fff;
    background-color: #cc91db;
    border-color: #cc91db;
}
.btn-pink2:hover { color: #fff }
.btn-pink:hover, .btn-pink:focus, .btn-pink:active, .btn-pink.active, .open > .dropdown-toggle.btn-pink {
    border-color: #b366cc;
    background: #b366cc;
    color: #fff;
}
</style>