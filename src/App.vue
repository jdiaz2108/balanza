<template>



<div>
    <div id="droppable" class="droppable">Drop here</div>
 <div class="draggable">Drag me</div>
    <div class="container-fluid bg-success">
        <div class="row">
            <div class="col-12 col-lg-6 droppable">
                zona 1
            </div>
            <div class="col-12 col-lg-6 bg-danger droppable">
               zona 2
            </div>
        </div>
    </div>
<div class="draggable border btn btn-info" :style="{ 'opacity': opacity, 'position': 'relative' }">prueba</div>

<div class="draggable border btn btn-info" :style="{ 'opacity': opacity, 'position': 'relative' }">prueba2</div>

</div>
</template>

<script>

  export default {
    mounted() {
    var self = this;
        $( ".draggable" ).draggable({ 
    revert: true,

     }).data(self.sotado, false);
        $( ".droppable" ).droppable({
            hoverClass: "boxHover",
          drop: function() {
            console.log(self.alertini('holi'));
          }
        }).data(self.sotado, false);

    },
    data() {
      return {
        activo: false,
        lists: [
          [],
          ['A', 'B', 'C'],
          ['D', 'Educative esta es una prueba aspera', 'F'],
        ],
        zona1: [],
        zona2: [],
        origXPos: [],
        origYPos: [],
        attempts: 0,
        correct: 0,
        array: null,
        hold: null,
        opacity: 1,
        soltado: true,
      };
    },
    methods: {
    alertini: function(a) { alert(a) },
        log: function(e) { console.log(e);
        console.log(e.type) },
    },
  };
</script>

<style scoped>
  /* Prevent the text contents of draggable elements from being selectable. */
[draggable] {
  -moz-user-select: none;
  -khtml-user-select: none;
  -webkit-user-select: none;
  user-select: none;
  /* Required to make elements draggable in old WebKit */
  -khtml-user-drag: element;
  -webkit-user-drag: element;
}
</style>